---
title: カスタム Linux コンテナーへの CI/CD
description: Azure App Service でカスタム Linux コンテナーへの継続的配置を設定する方法について説明します。 継続的配置は、Docker Hub と ACR でサポートされています。
keywords: Azure App Service, Linux, Docker, acr, oss
author: msangapu-msft
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.topic: article
ms.date: 11/08/2018
ms.author: msangapu
ms.custom: seodec18
ms.openlocfilehash: d43491de7500204ed470757a1b744017a8180b57
ms.sourcegitcommit: 2ec4b3d0bad7dc0071400c2a2264399e4fe34897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "74687630"
---
# <a name="continuous-deployment-with-web-app-for-containers"></a>Web App for Containers での継続的デプロイ

このチュートリアルでは、管理された [Azure Container Registry](https://azure.microsoft.com/services/container-registry/) リポジトリまたは [Docker Hub](https://hub.docker.com) からのカスタム コンテナー イメージの継続的なデプロイを構成します。

## <a name="enable-continuous-deployment-with-acr"></a>ACR で継続的デプロイを有効にする

![ACR Webhook のスクリーンショット](./media/app-service-webapp-service-linux-ci-cd/ci-cd-acr-02.png)

1. [Azure portal](https://portal.azure.com) にサインインする
2. ページの左側にある **[App Service]** オプションを選択します。
3. 継続的デプロイを構成するアプリの名前を選択します。
4. **[コンテナーの設定]** ページで、 **[単一コンテナー]** を選択します
5. **[Azure Container Registry]** を選択します
6. **[継続的なデプロイ] > [オン]** を選択します
7. **[保存]** を選択して、継続的デプロイを有効にします。

## <a name="use-the-acr-webhook"></a>ACR Webhook を使用する

継続的デプロイを有効にした後は、Azure Container Registry の Webhook ページで、新しく作成した Webhook を表示できます。

![ACR Webhook のスクリーンショット](./media/app-service-webapp-service-linux-ci-cd/ci-cd-acr-03.png)

Container Registry で、[Webhooks] をクリックすると現在の Webhook が表示されます。

## <a name="enable-continuous-deployment-with-docker-hub-optional"></a>Docker Hub で継続的デプロイを有効にする (省略可能)

1. [Azure portal](https://portal.azure.com) にサインインする
2. ページの左側にある **[App Service]** オプションを選択します。
3. 継続的デプロイを構成するアプリの名前を選択します。
4. **[コンテナーの設定]** ページで、 **[単一コンテナー]** を選択します
5. **[Docker Hub]** を選択します
6. **[継続的なデプロイ] > [オン]** を選択します
7. **[保存]** を選択して、継続的デプロイを有効にします。

![アプリ設定のスクリーンショット](./media/app-service-webapp-service-linux-ci-cd/ci-cd-docker-02.png)

Webhook URL をコピーします。 Docker Hub に対する Webhook を追加するには、<a href="https://docs.docker.com/docker-hub/webhooks/" target="_blank">Docker Hub に対する Webhook</a> の説明に従ってください。

## <a name="next-steps"></a>次のステップ

* [Azure App Service on Linux の概要](./app-service-linux-intro.md)
* [Azure Container Registry](https://azure.microsoft.com/services/container-registry/)
* [App Service on Linux での .NET Core Web アプリの作成](quickstart-dotnetcore.md)
* [App Service on Linux で Ruby Web アプリを作成する](quickstart-ruby.md)
* [Web App for Containers で Docker/Go Web アプリをデプロイする](quickstart-docker-go.md)
* [Azure App Service on Linux の FAQ](./app-service-linux-faq.md)
* [Azure CLI を使用して Web App for Containers を管理する](./app-service-linux-cli.md)
