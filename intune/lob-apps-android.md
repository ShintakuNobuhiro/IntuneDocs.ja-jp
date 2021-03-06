---
title: Android の基幹業務アプリを Microsoft Intune に追加する方法
titlesuffix: ''
description: Microsoft Intune への Android の基幹業務 (LOB) アプリの追加について説明します。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/19/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.assetid: 061d793c-c724-4cd9-9240-adb0cbda5661
ms.reviewer: mghadial
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: a5b09f855b6da65edf3c560725b339528f2bcfaa
ms.sourcegitcommit: df60d03a0ed54964e91879f56c4ef0a7507c17d4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="how-to-add-android-line-of-business-lob-apps-to-microsoft-intune"></a>Android の基幹業務 (LOB) アプリを Microsoft Intune に追加する方法

[!INCLUDE[azure_portal](./includes/azure_portal.md)]

基幹業務 (LOB) アプリとは、アプリのインストール ファイルから Intune に追加するアプリのことです。 この種のアプリは、通常、社内で作成されます。 Intune によって、ユーザーのデバイス上に LOB アプリがインストールされます。 

> [!Note]
> Google Play for Work ストアの基幹業務 (LOB) アプリの詳細については、「[Google Play for Work ストアの基幹業務アプリを使用する](apps-add-android-for-work.md?#working-with-a-line-of-business-app-from-the-google-play-for-work-store)」を参照してください。 

## <a name="step-1---specify-the-software-setup-file"></a>手順 1 - ソフトウェアのセットアップ ファイルを指定する

1. サインイン、 [Azure ポータル](https://portal.azure.com)します。
2. **[すべてのサービス]**、**[Intune]** の順に選択します。 Intune は **[監視 + 管理]** セクションにあります。
3. **[Intune]** ウィンドウで、**[モバイル アプリ]** を選択します。
4. **[モバイル アプリ]** ワークロードで、**[管理]** > **[アプリ]** の順に選択します。
5. アプリの一覧の上にある **[追加]** を選択します。
6. **[アプリの追加]** ウィンドウで、**[基幹業務アプリ]** を選択します。

## <a name="step-2---configure-the-app-package-file"></a>手順 2 - アプリのパッケージ ファイルを構成する

1. **[アプリの追加]** ウィンドウで、**[アプリのパッケージ ファイル]** を選択します。
2. **[アプリのパッケージ ファイル]** ウィンドウで参照ボタンを選択し、拡張子が **.apk** の Android インストール ファイルを選択します。
3. 終了したら **[OK]** を選択します。


## <a name="step-3---configure-app-information"></a>手順 3 - アプリ情報を構成する

1. **[アプリの追加]** ウィンドウで、**[アプリのパッケージ ファイル]** を選択します。
2. **[アプリ情報]** ウィンドウで、アプリの詳細を追加します。 選択したアプリによっては、このウィンドウ内の一部の値が自動的に入力されている場合があります。
    - **[名前]** - ポータル サイトに表示するアプリの名前を入力します。 使用するアプリ名はすべて一意にします。 同じアプリ名が 2 つ存在する場合、会社のポータルではそのいずれかのみがユーザーに表示されます。
    - **説明** - ポータル サイトでユーザーに表示するアプリの説明を入力します。
    - **[発行元]** - アプリの発行元の名前を入力します。
    - **[オペレーティング システムの最小要件]** - アプリをインストールできる最小限のオペレーティング システム バージョンを一覧から選択します。 これよりも前のオペレーティング システムがアプリの割り当て先デバイスにインストールされている場合、そのアプリはインストールされません。
    - **[アプリのバージョンを無視する]** - アプリがアプリ開発者によって自動的に更新される場合は、**[はい]** に設定します。
    - **[カテゴリ]** - 1 つまたは複数の組み込みアプリ カテゴリ、または作成したカテゴリを選択します。 この操作を行うと、会社のポータルを閲覧するときに、ユーザーがアプリを探しやすくなります。
    - **[会社のポータルでおすすめアプリとして表示します]** - ユーザーがアプリを探す際に、会社のポータルのメイン ページでアプリを目立つように表示します。
    - **[情報 URL]** - 必要に応じて、このアプリに関する情報が含まれる Web サイトの URL を入力します。 この URL は会社のポータルでユーザーに表示されます。
    - **[プライバシー URL]** - 必要に応じて、このアプリのプライバシー情報が含まれる Web サイトの URL を入力します。 この URL は会社のポータルでユーザーに表示されます。
    - **[開発者]** - 必要に応じて、アプリ開発者の名前を入力します。
    - **[所有者]** - 必要に応じて、このアプリの所有者の名前 ("**人事部**" など) を入力します。
    - **[メモ]** - このアプリに関連付けるメモを入力します。
    - **[ロゴ]** - アプリに関連付けるアイコンをアップロードします。 ユーザーが会社のポータルを参照するとき、アプリにこのアイコンが表示されます。
3. 終了したら **[OK]** を選択します。

## <a name="step-4---finish-up"></a>手順 4. - 完了

1. **[アプリの追加]** ウィンドウで、アプリの詳細を確認します。
2. **[追加]** を選択して、アプリを Intune にアップロードします。

作成したアプリはアプリの一覧に表示され、選択したグループに割り当てることができるようになります。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。

## <a name="step-5---update-a-line-of-business-app"></a>手順 5 - 基幹業務アプリの更新

[!INCLUDE[shared-proc-lob-updateapp](./includes/shared-proc-lob-updateapp.md)]

> [!Note]
> Intune サービスで新しい APK ファイルをデバイスへ正常に展開するには、APK パッケージの AndroidManifest.xml ファイルの android:versionCode 文字列をインクリメントする必要があります。

## <a name="next-steps"></a>次の手順

- 作成したアプリがアプリの一覧に表示されます。 選択したグループにアプリを割り当てることができます。 詳細については、[アプリをグループに割り当てる方法](apps-deploy.md)に関するページを参照してください。

- アプリのプロパティと割り当てを監視する方法について説明します。 詳細については、「[アプリ情報と割り当てを監視する方法](apps-monitor.md)」を参照してください。

- Intune におけるアプリのコンテキストについて説明します。 詳細については、「[デバイスとアプリのライフサイクルの概要](introduction-device-app-lifecycles.md)」を参照してください。
