---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 05/05/2020
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: da0e26e0739711082baa4609e2382692c0a68a00
ms.sourcegitcommit: 11572a869ef8dbec8e7c721bc7744e2859b79962
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82838233"
---
|名前 |説明 |効果 |Version |GitHub |
|---|---|---|---|---|
|[仮想マシンに対して Azure Backup を有効にする必要がある](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F013e242c-8828-4970-87b3-ab247555486d) |このポリシーは、すべての仮想マシンで Azure Backup サービスが有効になっているかどうかを監査するのに役立ちます。 Azure Backup は、コスト効果の高いワンクリック バックアップ ソリューションで、データの回復を簡略化し、他のクラウド バックアップ サービスよりも簡単に有効にできます。 |AuditIfNotExists、Disabled |1.0.0 |[リンク](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/VirtualMachines_EnableAzureBackup_Audit.json) |
|[特定の場所の VM を同じ場所にある既存の中央コンテナーにバックアップするように構成する](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F09ce66bc-1220-4153-8104-e3f51c936913) |このポリシーは、特定の場所の VM を同じ場所にある既存の中央コンテナーにバックアップするように Azure Backup 保護を構成します。 これは、まだバックアップ用に構成されていない VM にのみ適用されます。 このポリシーは、200 を超える VM に割り当てないようにすることをお勧めします。 ポリシーが 200 を超える VM に割り当てられていると、指定したスケジュールの数時間後にバックアップがトリガーされることがあります。 このポリシーは、より多くの VM イメージをサポートするように強化される予定です。 |deployIfNotExists、auditIfNotExists、disabled |1.0.0 |[リンク](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/VirtualMachineBackup_Backup_DeployIfNotExists.json) |