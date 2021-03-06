---
title: Azure Security Center と Azure Kubernetes Service
description: Azure Security Center と Azure Kubernetes Service の統合について説明します。
services: security-center
documentationcenter: na
author: memildin
manager: rkarlin
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/04/2019
ms.author: memildin
ms.openlocfilehash: d5c74ac760b5746d37468d692c2a46d5aedbee72
ms.sourcegitcommit: ced98c83ed25ad2062cc95bab3a666b99b92db58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80436173"
---
# <a name="azure-kubernetes-services-integration-with-security-center"></a>Azure Kubernetes Service と Security Center の統合

Azure Kubernetes Service (AKS) は、コンテナー化されたアプリケーションを開発、デプロイ、管理するための Microsoft のマネージド サービスです。 

Azure Security Center の Standard レベル ([価格](security-center-pricing.md)に関するページを参照) と AKS を組み合わせて使用すると、AKS ノード、クラウド トラフィック、セキュリティ制御を詳細に可視化できます。

Security Center は、AKS マスター ノードで既に収集済みのデータを使用して、AKS クラスターにセキュリティ上の利点をもたらします。 

![Azure Security Center と Azure Kubernetes Service (AKS) の概要](./media/azure-kubernetes-service-integration/aks-asc-integration-overview.png)

この 2 つのツールを組み合わせることで、最高レベルのクラウドネイティブな Kubernetes セキュリティ オファリングが形成されます。 

## <a name="benefits-of-integration"></a>統合の利点

2 つのサービスを組み合わせて使用すると、次の利点が得られます。

* **セキュリティに関する推奨事項** - Security Center では、クラスターから個々の仮想マシンまで、AKS リソースが識別され、分類されます。 これにより、セキュリティに関する推奨事項をリソースごとに表示できます。 詳細については、[推奨事項の参照一覧](recommendations-reference.md#recs-containers)にあるコンテナーの推奨事項を確認してください。 

* **環境の強化機能** - Security Center では、Kubernetes クラスターの構成および Docker 構成を常に監視します。 また、業界標準を反映したセキュリティの推奨事項を生成します。

* **実行時の保護** - Security Center では、次の AKS ソースの継続的な分析によって、ホスト "*および*" AKS クラスター レベルで検出された脅威や悪意のあるアクティビティについてアラートを通知します。
    * 未加工のセキュリティ イベント (ネットワーク データやプロセスの作成など)
    * Kubernetes 監査ログ

    詳細については、「[Azure コンテナーの脅威保護](threat-protection.md#azure-containers)」を参照してください

    発生する可能性があるアラートの一覧については、アラートの参照表で次のセクションを確認してください。[AKS クラスター レベルのアラート](alerts-reference.md#alerts-akscluster)と[コンテナーのホスト レベルのアラート](alerts-reference.md#alerts-containerhost)です。  

![Azure Security Center と Azure Kubernetes Service (AKS) の詳細](./media/azure-kubernetes-service-integration/aks-asc-integration-detailed.png)

> [!NOTE]
> Kubernetes 環境から Azure Security Center によってスキャンされたデータには、機密情報が含まれている場合があります。


## <a name="next-steps"></a>次のステップ

Security Center のコンテナーのセキュリティ機能の詳細については、以下をご覧ください。

* [Azure Security Center とコンテナーのセキュリティ](container-security.md)

* [Azure Container Registry との統合](azure-container-registry-integration.md)

* [Microsoft でのデータ管理](https://www.microsoft.com/trust-center/privacy/data-management) - Microsoft サービス (Azure、Intune、Office 365 など) のデータ ポリシー、Microsoft のデータ管理の詳細、お客様のデータに影響する保持ポリシーについて説明します。
