---
title: Azure Monitor ブックとカスタム パラメーター
description: 作成済みのブックやパラメーター化されたカスタム ブックを使用して複雑なレポート作成を簡素化します。
services: azure-monitor
author: mrbullwinkle
manager: carmonm
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 10/23/2019
ms.author: mbullwin
ms.openlocfilehash: 4d9f6e48722f01970a90a3a1d8d8b58b5d939774
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2020
ms.locfileid: "77658270"
---
# <a name="interactive-workbooks"></a>対話型ブック

ブックでは、作成者が利用者向けに対話型のレポートやエクスペリエンスを作成できます。 対話機能は、さまざまな方法でサポートされています。

## <a name="parameter-changes"></a>パラメーターの変更
ブックのユーザーがパラメーターを更新すると、そのパラメーターが使用されているすべてのコントロールが自動的に更新および再描画され、新しい状態が反映されます。 ほとんどの Azure portal レポートでは、このように対話機能がサポートされます。 ブックでは、ユーザーの労力を最小限に抑えながら、非常に簡単な方法でこれを実現できます。

[ブックのパラメーター](workbooks-parameters.md)について詳しくご確認ください

## <a name="grid-row-clicks"></a>グリッド行のクリック
ブックでは、グリッド内の行をクリックするとその行の内容に基づいて後続のグラフが更新されるシナリオを作成者が構築できます。 

たとえば、要求の一覧と統計情報 (失敗数など) を表示するグリッドをユーザーに用意できます。 要求に対応する行をクリックすると、下にある詳細なグラフが更新され、その要求のみがフィルター選択されるように設定できます。

### <a name="setting-up-interactivity-on-grid-row-click"></a>グリッド行をクリックしたときの対話機能の設定
1. _[編集]_ ツール バー項目をクリックして、ブックを編集モードに切り替えます。
2. _[クエリの追加]_ リンクを使用して、ログ クエリ コントロールをブックに追加します。 
3. クエリの種類として _[ログ]_ を選択し、リソースの種類 (たとえば、Application Insights) と、ターゲットにするリソースを選択します。
4. クエリ エディターを使用して、分析用の KQL を入力します
    ```kusto
    requests
    | summarize AllRequests = count(), FailedRequests = countif(success == false) by Request = name
    | order by AllRequests desc    
    ```
5. [クエリの実行] を選択して結果を確認します
6. クエリのフッターの _[詳細設定]_ アイコン (歯車アイコン) をクリックします。 これにより、[詳細設定] ペインが開きます 
7. [項目が選択されている場合、パラメーターをエクスポートします] という設定をオンにします
    1. [エクスポートするフィールド]\: [要求]
    2. Parameter name: `SelectedRequest` (パラメーター名: {2})
    3. 既定値:`All requests`
    
    ![フィールドをパラメーターとしてエクスポートするための設定を備えた詳細エディターを示す画像](./media/workbooks-interactive/advanced-settings.png)

8. [`Done Editing`] をクリックします。
9. 手順 2 と 3 を使用して、別のクエリ コントロールを追加します。
10. クエリ エディターを使用して、分析用の KQL を入力します
    ```kusto
    requests
    | where name == '{SelectedRequest}' or 'All Requests' == '{SelectedRequest}'
    | summarize ['{SelectedRequest}'] = count() by bin(timestamp, 1h)
    ```
11. [クエリの実行] を選択して結果を確認します。
12. _[視覚化]_ を [面グラフ] に変更します
12. 最初のグリッドの行をクリックします。 下にある面グラフで、選択した要求がどのようにフィルターされるかに注目してください。

結果のレポートは、編集モードではこのようになります。

![グリッド行のクリックを使用した対話型エクスペリエンスの作成を示す画像](./media/workbooks-interactive//grid-click-create.png)

次の画像は、同じ原則に基づく読み取りモードでのより複雑な対話型レポートを示しています。 このレポートでは、グリッドのクリックを使用してパラメーターをエクスポートします。それがさらに、2 つのグラフと 1 つのテキスト ブロックで使用されます。

![グリッド行のクリックを使用した対話型エクスペリエンスの作成を示す画像](./media/workbooks-interactive/grid-click-read-mode.png)

### <a name="exporting-the-contents-of-an-entire-row"></a>行全体の内容のエクスポート
特定の列だけではなく、選択した行の内容全体をエクスポートすることが望ましい場合があります。 そのような場合は、上記の手順 7.1 で [エクスポートするフィールド] プロパティを設定しないでおきます。 ブックにより、行の内容全体が json としてパラメーターにエクスポートされます。 

参照している KQL コントロールで、`todynamic` 関数を使用して json を解析し、個々の列にアクセスします。

 ## <a name="grid-cell-clicks"></a>グリッド セルのクリック
ブックでは、リンク レンダラーと呼ばれる特別な種類のグリッド列レンダラーを介して作成者が対話機能を追加できます。 リンク レンダラーは、セルの内容に基づいてグリッド セルをハイパーリンクに変換します。 ブックでは、さまざまな種類のリンク レンダラーがサポートされています。これには、リソースの概要ブレード、プロパティ バッグ ビューアー、App Insights の検索、使用状況、トランザクション トレースなどを開くことができるものが含まれます。

### <a name="setting-up-interactivity-using-grid-cell-clicks"></a>グリッド セルのクリックを使用した対話機能の設定
1. _[編集]_ ツール バー項目をクリックして、ブックを編集モードに切り替えます。
2. _[クエリの追加]_ リンクを使用して、ログ クエリ コントロールをブックに追加します。 
3. クエリの種類として _[ログ]_ を選択し、リソースの種類 (たとえば、Application Insights) と、ターゲットにするリソースを選択します。
4. クエリ エディターを使用して、分析用の KQL を入力します
    ```kusto
    requests
    | summarize Count = count(), Sample = any(pack_all()) by Request = name
    | order by Count desc
    ```
5. [クエリの実行] を選択して結果を確認します
6. _[列の設定]_ をクリックして設定ペインを開きます。
7. _[列]_ セクションで設定を行います。
    1. _[サンプル]_ - [列レンダラー]: [リンク]、[開くビュー]: [セルの詳細]、[リンク ラベル]: `Sample`
    2. _[カウント]_ - [列レンダラー]: [横棒]、[カラー パレット]: [青]、[最小値]: `0`
    3. _[要求]_ - [列レンダラー]: [自動]
    4. _[保存して閉じる]_ をクリックして、変更を適用します
8. グリッド内のいずれかの `Sample` リンクをクリックします。 これにより、サンプリングされた要求の詳細が記載されたプロパティ ペインが開きます。

    ![グリッド セルのクリックを使用した対話型エクスペリエンスの作成を示す画像](./media/workbooks-interactive/grid-cell-click-create.png)

### <a name="link-renderer-actions"></a>リンク レンダラーのアクション
| リンク アクション | クリック時のアクション |
|:------------- |:-------------|
| `Generic Details` | プロパティ グリッドのコンテキスト ブレードに含まれる行の値を表示します |
| `Cell Details` | プロパティ グリッドのコンテキスト ブレードに含まれるセルの値を表示します。 情報を含む動的な型がセルに含まれている場合に便利です (たとえば、場所、ロール インスタンスなどの要求プロパティを含む json)。 |
| `Cell Details` | プロパティ グリッドのコンテキスト ブレードに含まれるセルの値を表示します。 情報を含む動的な型がセルに含まれている場合に便利です (たとえば、場所、ロール インスタンスなどの要求プロパティを含む json)。 |
| `Custom Event Details` | セル内のカスタム イベント ID (itemId) を使用して Application Insights 検索の詳細を開きます |
| `* Details` | 依存関係、例外、ページ ビュー、要求、トレースを除き、[カスタム イベントの詳細] に似ています。 |
| `Custom Event User Flows` | セル内のカスタム イベント名に基づいてピボットされた Application Insights User Flows エクスペリエンスを開きます |
| `* User Flows` | 例外、ページ ビュー、要求を除き、カスタム イベント User Flows に似ています |
| `User Timeline` | セル内のユーザー ID (user_Id) を使用してユーザー タイムラインを開きます |
| `Session Timeline` | セル内の値に対して Application Insights 検索エクスペリエンスを開きます (たとえば、セル内の値が abc であればテキスト "abc" を検索します) |
| `Resource overview` | セルのリソース ID 値に基づいて、ポータルでリソースの概要を開きます |

## <a name="conditional-visibility"></a>条件付きの可視性
ブックでは、ユーザーがパラメーターの値に基づいて特定のコントロールを表示したり非表示にしたりできます。 これにより、作成者はユーザー入力またはテレメトリ状態に基づいてレポートの外観を変えることができます。 たとえば、状況が良好なときは利用者に概要だけを表示し、何か問題が発生したときは完全な詳細を表示することができます。

### <a name="setting-up-interactivity-using-conditional-visibility"></a>条件付きの可視性を使用した対話機能の設定
1. 「グリッド行をクリックしたときの対話機能の設定」の手順に従って、2 つの対話型コントロールを設定します。
2. 新しいパラメーターを先頭に追加します。
    1. 名前: `ShowDetails`
    2. [パラメーターの種類]\: [`Drop down`ドロップ ダウン]
    3. [必須ですか?]\: `checked`オン
    4. [データの取得元]\: [クエリ]`JSON`
    5. [JSON 入力]\: `["Yes", "No"]`
    6. 保存して変更をコミットします。
3. パラメーター値を [`Yes`] に設定します
4. 面グラフが含まれているクエリ コントロールで、 _[詳細設定]_ アイコン (歯車アイコン) をクリックします
5. [この項目を条件付きで表示する] という設定をオンにします
    1. この項目は、`ShowDetails` パラメーター値が `equals` `Yes` の場合に表示されます
6. _[編集完了]_ をクリックして変更をコミットします。
7. ブックのツール バーの _[編集完了]_ をクリックして読み取りモードに移行します。
8. [`ShowDetails`] パラメーターの値を [`No`] に切り替えます。 下のグラフが表示されなくなることに注目してください。

次の画像は、[`ShowDetails`] が [`Yes`] である、グラフが表示されるケースを示しています

![グラフが表示される条件付きの可視性を示す画像](./media/workbooks-interactive/conditional-visibility.png)

次の画像は、[`ShowDetails`] が [`No`] である、グラフが表示されないケースを示しています

![グラフが表示されない条件付きの可視性を示す画像](./media/workbooks-interactive/conditional-invisible.png)

## <a name="next-steps"></a>次のステップ


* ブックの豊富な視覚化オプションの学習を[開始](workbooks-visualizations.md)します。
* ブック リソースへのアクセスを[制御](workbooks-access-control.md)し、共有します。
