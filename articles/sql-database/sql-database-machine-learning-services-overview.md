---
title: Machine Learning Services と R (プレビュー)
description: この記事では、Azure SQL Database の Machine Learning Services と R およびそのしくみについて説明します。
services: sql-database
ms.service: sql-database
ms.subservice: machine-learning
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: carlrab
manager: cgronlun
ms.date: 11/20/2019
ROBOTS: NOINDEX
ms.openlocfilehash: 46ca4661d06b52c861431a680a69297575ac99b0
ms.sourcegitcommit: b55d7c87dc645d8e5eb1e8f05f5afa38d7574846
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81461414"
---
# <a name="azure-sql-database-machine-learning-services-with-r-preview"></a>Azure SQL Database Machine Learning Services と R (プレビュー)

Machine Learning Services は、データベース内の R スクリプトを実行するために使用される、Azure SQL Database の機能です。 その機能には、高パフォーマンスの予測分析と機械学習のための Microsoft R パッケージが含まれています。 ストアド プロシージャ、R ステートメントを含む T-SQL、または T-SQL を含む R コードにより、R スクリプトでリレーショナル データを使用できます。

[!INCLUDE[ml-preview-note](../../includes/sql-database-ml-preview-note.md)]

## <a name="what-you-can-do-with-r"></a>R でできること

R 言語の機能を使用して、データベース内で高度な分析と機械学習を提供します。 この機能を使用すると、データが存在する場所で計算と処理を行うことができ、ネットワーク経由でデータをプルする必要がありません。 また、エンタープライズ R パッケージの機能を利用して、大規模で高度な分析を提供できます。

Machine Learning Services には、R の基本ディストリビューションに、Microsoft 提供のエンタープライズ R パッケージがオーバーレイされたものが含まれます。 Microsoft の R 関数とアルゴリズムはスケールと実用性の両方を考慮して設計されており、予測分析、統計モデリング、データの視覚化、および最先端の機械学習アルゴリズムが提供されます。

### <a name="r-packages"></a>R パッケージ

最も一般的なオープン ソースの R パッケージが、Machine Learning Services にプレインストールされています。 Microsoft の次の R パッケージも含まれています。

| R パッケージ | 説明|
|-|-|
| [Microsoft R Open](https://mran.microsoft.com/rro) | Microsoft R Open は、Microsoft が提供する R の強化されたディストリビューションです。 これは、統計分析とデータ サイエンスの機能が一式そろったオープンソース プラットフォームです。 R に基づき、100% の互換性があり、パフォーマンスと再現性を向上させる追加機能が含まれています。 |
| [RevoScaleR](https://docs.microsoft.com/sql/advanced-analytics/r/ref-r-revoscaler) | RevoScaleR は、スケーラブルな R のためのプライマリ ライブラリです。このライブラリの関数は最も広く使用されています。 データの変換と操作、統計の要約、視覚化、およびモデリングと分析の多くのフォームが、これらのライブラリに収められています。 さらに、これらのライブラリの関数は、並列処理のためにワークロードを使用可能なコア間に自動的に分散させ、計算エンジンによって調整および管理されるデータのチャンクを処理する機能を備えています。 |
| [MicrosoftML (R)](https://docs.microsoft.com/sql/advanced-analytics/r/ref-r-microsoftml) | MicrosoftML では、テキスト分析、画像分析、およびセンチメント分析用のカスタム モデルを作成するための機械学習アルゴリズムが追加されます。 |

プレインストールされたパッケージだけでなく、[追加パッケージをインストールする](sql-database-machine-learning-services-add-r-packages.md)ことができます。

<a name="signup"></a>

## <a name="sign-up-for-the-preview-closed"></a>プレビューのサインアップ (クローズ)

> [!IMPORTANT]
> Azure SQL Database Machine Learning Services (プレビュー) のサインアップは現在**クローズ**されています。

## <a name="next-steps"></a>次のステップ

- [SQL Server Machine Learning Services との重要な違い](sql-database-machine-learning-services-differences.md)に関する記事を参照してください。
- Azure SQL Database Machine Learning Services (プレビュー) を R で照会する方法について、「[クイック スタート ガイド](sql-database-connect-query-r.md)」を参照してください。
- シンプルな R スクリプトから始めるには、「[Azure SQL Database Machine Learning Services (プレビュー) で簡単な R スクリプトを作成して実行する](sql-database-quickstart-r-create-script.md)」を参照してください。
