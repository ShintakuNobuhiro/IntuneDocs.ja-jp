---
title: "REST クライアントを使用してデータ ウェアハウス API からデータを取得する"
description: "RESTful API を使用し、Intune データ ウェアハウスからデータを取得します。"
keywords: 
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: D6D15039-4036-446C-A58F-A5E18175720A
ms.reviewer: jeffgilb
ms.suite: ems
ms.custom: intune-classic
ms.openlocfilehash: 1bbb0e8ba84e221df3a434da79c513939267648b
ms.sourcegitcommit: b8ef9d8387b4d9b2ea4e6ce937635304771e6532
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/11/2017
---
# <a name="get-data-from-the-intune-data-warehouse-api-with-a-rest-client"></a>REST クライアントを使用して Intune データ ウェアハウス API からデータを取得する

RESTful エンドポイント経由で Intune データ ウェアハウスのデータ モデルにアクセスします。 データにアクセスするには、OAuth 2.0 を利用し、Microsoft Azure Active Directory (Azure AD) でクライアントを認証する必要があります。 アクセスを有効にするには、最初に Azure でネイティブ アプリを設定し、Microsoft Intune API へのアクセス許可を与えます。 ローカル クライアントに許可が与えられます。そのクライアントはネイティブ アプリ経由でデータ ウェアハウス エンドポイントと通信できます。

データ ウェアハウス API からデータを取得するようにクライアントを設定する手順では、次の作業が必要になります。

1. Azure でネイティブ アプリとしてクライアント アプリを作成する
3. Microsoft Intune API へのアクセスをクライアント アプリに与える
3. データを取得するための REST クライアントを作成する

次の手順で、Postman をクライアントとして認証し、使用する方法を学習してください。 Postman は、API と連動する REST クライアントを開発およびトラブルシューティングするために一般的に利用されているツールです。 Postman の詳細については、「[Postman](https://www.getpostman.com)」のサイトをご覧ください。 このトピックには、C# コード サンプルも含まれます。 そのサンプルは、クライアントを認証し、API からデータを取得するコードの例を提供します。

## <a name="create-a-native-app-in-azure"></a>Azure でネイティブ アプリを作成する

Azure でネイティブ アプリを作成します。 このネイティブ アプリはクライアント アプリです。 ローカル コンピューターで実行されるクライアントは、ローカル クライアントが資格情報を要求するとき、Intune データ ウェアハウス API を参照します。 

1. テナントの Azure Portal にサインインします。 **[Azure Active Directory]** > **[アプリの登録]** の順に選択し、**[アプリの登録]** ブレードを開きます。
2. **[New app registration]\(新しいアプリの登録\)** をクリックします。
3. アプリの詳細を入力します。
    1.  「Intune データ ウェアハウス クライアント」など、わかりやすい名前を **[名前]** に入力します。
    2.  **[アプリケーションの種類]** の **[ネイティブ]** を選択します。
    3.  **[サインオン URL]** に URL を入力します。 サインオン URL は特定のシナリオによって代わります。ただし、Postman を利用する予定の場合、「`https://www.getpostman.com/oauth2/callback`」と入力してください。 Azure AD に認証するとき、クライアント認証手順のコールバックを利用します。
4.  **[作成]** をクリックします。

     ![Intune データ ウェアハウス API](media\reports-get_rest_data_client_overview.png)

5. このアプリの **[アプリケーション ID]** をメモします。 この ID は次のセクションで使用します。
6. Postman を使用する予定であれば、キーを追加します。 このキーは Azure AD 認証でクライアント シークレットとして使用されます。 キーを追加するには:
    1.  アプリの [設定] ブレードの **[API アクセス]** で **[キー]** をクリックします。
    2.  Client-Secret など、キーの名前を **[説明]** に入力します。
    3.  期間には **[1 年]** を選択します。
    4.  **[Save]**(保存) をクリックします。 
    5.  キーの値をコピーします。 キーの **[設定]** ブレードを閉じた後は、キーを取得できなくなります。

## <a name="grant-the-native-app-access-to-the-microsoft-intune-api"></a>Microsoft Intune API へのアクセスをネイティブ アプリに与える

これでアプリが Azure に定義されました。 ネイティブ アプリから Microsoft Intune API にアクセスするための許可を与えます。

1.  ネイティブ アプリをクリックします。 アプリには Intune Data Warehouse Client などの名前が付けてあります。
2.  **[設定]** ブレードで **[必要なアクセス許可]** をクリックします。
3.  **[必要なアクセス許可]** ブレードで **[追加]** をクリックします。
4.  **[API を選択します]** をクリックします。
5.  Web アプリ名を検索します。 **Microsoft Intune API** という名前です。
6.  一覧のアプリをクリックします。
7.  **[選択]** をクリックします。
8.  **[委任されたアクセス許可]** ボックスにチェックマークを入れ、**[Get data warehouse information from Microsoft Intune]\(Microsoft Intune からデータ ウェアハウス情報を取得する\)** を追加します。

    ![アクセスを有効にする](media\reports-get_rest_data_client_access.png)

9.  **[選択]** をクリックします。
10.  **[完了]** をクリックします。
11.  必要に応じて、[必要なアクセス許可] ブレードで **[アクセス許可の付与]** をクリックします。 これで、現在のディレクトリのすべてのアカウントへのアクセスが与えられます。 テナントのすべてのユーザーに対して同意を求めるダイアログ ボックスが表示されなくなります。 詳細については、「[Azure Active Directory とアプリケーションの統合](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)」を参照してください。
12.  **[はい]** をクリックします。

## <a name="get-data-from-the-microsoft-intune-api-with-postman"></a>Microsoft Intune API と Postman からデータを取得する

Intune データ ウェアハウス API と、Postman など、汎用 REST クライアントを連動させることができます。 Postman を利用することで、API の機能、つまり、基礎となる OData データ モデルを詳しく理解できます。また、API リソースへの接続で発生した問題を解決できます。 このセクションでは、ローカル クライアントに Auth2.0 トークンを生成する方法を紹介します。 クライアントが Azure AD で認証したり、API リソースにアクセスしたりするには、トークンが必要です。

### <a name="information-you-will-need-to-make-the-call"></a>呼び出しに必要な情報

Postman を使用して REST 呼び出しを行うには、次の情報が必要です。

| 属性        | 説明                                                                                                                                                                          | 例                                                                                       |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| コールバック URL     | アプリ設定ページでこれをコールバック URL として設定します。                                                                                                                              | https://www.getpostman.com/oauth2/callback                                                    |
| トークン名       | Azure アプリに資格情報を渡すために使用する文字列。 この過程で生成されたトークンにより、データ ウェアハウス API を呼び出すことができます。                          | Bearer                                                                                        |
| 認証 URL         | これは認証に使用する URL です。 | https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com |
| アクセス トークン URL | これはトークンの付与に使用する URL です。                                                                                                                                              | https://login.microsoftonline.com/common/oauth2/token |
| クライアント ID        | Azure でネイティブ アプリを作成したとき、これを作成し、メモしました。                                                                                               | 4184c61a-e324-4f51-83d7-022b6a81b991                                                          |
| クライアント シークレット    | Azure でクライアント アプリにキーを追加したとき、これを作成し、メモしました。                                                                                              | JZoRZGPmN9xwsUnfX9UW877dkV5Fn/qQClhr7SuyMUQ=                                                  |
| スコープ (省略可能) | 新規                                                                                                                                                                               | このフィールドは空白にできます。                                                                     |
| 付与タイプ       | このトークンは認証コードです。                                                                                                                                                  | 認証コード                                                                            |

エンドポイントが必要です。 この例では、**dates** エントリからデータを取得します。 **dates** エンティティの形式は次のようになっています。`https://fef.{aus}.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=beta` テナント管理 URL を使用します。 Web アプリを作成したとき、テナント管理 URL を使用しました。

### <a name="make-the-rest-call"></a>REST 呼び出しを行う

Postman のために新しいアクセス トークンを取得するには、Azure AD 認証 URL、クライアント ID、クライアント シークレットを追加する必要があります。 Postman は、資格情報が入力された認証ページを読み込みます。

#### <a name="add-the-information-used-to-request-the-token"></a>トークンの要求に必要な情報を追加する

1.  まだインストールしていない場合、Postman をダウンロードします。 Postman をダウンロードする方法は、[www.getpostman](https://www.getpostman.com) でご確認ください。
2.  Postman を開きます。 HTTP 操作の **GET** を選択します。
3.  アドレスにエンドポイント URL を貼り付けます。 次のようになります。  

    `https://fef.msua06.manage.microsoft.com/ReportingService/DataWarehouseFEService/dates?api-version=beta`
4.  **[認証]** タブを選択し、**[種類]** 一覧から **[OAuth 2.0]** を選択します。
5.  **[Get New Access Token]\(新しいアクセス トークンを取得する\)** をクリックします。
6.  Azure でアプリにコールバック URL が追加されていることを確認します。 コールバック URL は `https://www.getpostman.com/oauth2/callback` です。
7.  **[トークン名]** のベアラーを入力します。
8.  **[認証 URL]** を追加します。 次のようになります。  

    `https://login.microsoftonline.com/common/oauth2/authorize?resource=https://api.manage.microsoft.com`
9.  **[アクセス トークン URL]** を追加します。 次のようになります。  

     `https://login.microsoftonline.com/common/oauth2/token`

10. Azure で作成し、`Intune Data Warehouse Client` という名前を付けたネイティブ アプリから **[クライアント ID]** を追加します。 次のようになります。  

     `4184c61a-e324-4f51-83d7-022b6a81b991`

11. Azure でネイティブ アプリを作成したときにキーとして定義した **[クライアント シークレット]** を追加します。 次のようになります。 

     `F360R69M0MS72OB6YAqTyXO9MsXZx/OJTgAE2HB4k2k=`

12. **[認証コード]** を選択し、アクセス トークンをローカルで要求します。

13. **[Request Token]\(トークンの要求\)** をクリックします。

    ![トークンの情報](media\reports-postman_getnewtoken.png)

14. アクティブな AD 認証ページで資格情報を入力します。 これで、Postman の既存トークン一覧に `Bearer` という名前のトークンが含まれます。
16. このトークンを選択します。 トークンの追加先として **[ヘッダー]** を選択します。
17. **[Use Token]\(トークンの使用\)** をクリックします。 ヘッダーの一覧には、認証の新しいキー値と値 `Bearer <your-authorization-token>` が含まれます。

#### <a name="send-the-call-to-the-endpoint-using-postman"></a>Postman を使用し、エンドポイントへの呼び出しを送信します。

1.  **[送信]** をクリックします。
2.  返されるデータは Postman の応答本文に表示されます。

    ![Postman 200OK](media\reports-postman_200OK.png)

## <a name="create-a-rest-client-c-to-get-data-from-the-intune-data-warehouse"></a>Intune データ ウェアハウスからデータを取得する REST クライアント (C#) を作成する

次のサンプルには、単純な REST クライアントが含まれています。 このコードでは、.Net ライブラリの **httpClient** クラスが使用されています。 クライアントが Azure AD の資格情報を得ると、GET REST 呼び出しを構築し、データ ウェアハウス API から日付エンティティを取得します。

> [!Note]  
> 次のコード [サンプルは GitHub](https://github.com/Microsoft/Intune-Data-Warehouse/blob/master/Samples/CSharp/Program.cs) にあります。 サンプルの最新の変更と更新については、GitHub リポジトリを参照してください。

1.  **Microsoft Visual Studio** を起動します。
2.  **[ファイル]** > **[新しいプロジェクト]** の順に選択します。 **[Visual C#]** を展開し、**[コンソール アプリ (.Net Framework)]** を選択します。 
3.  プロジェクトに ` IntuneDataWarehouseSamples` という名前を付け、プロジェクトを保存する場所に進み、**[OK]** をクリックします。
3.  ソリューション エクスプローラーでソリューションの名前を右クリックし、**[ソリューションの NuGet パッケージの管理]** を選択します。 **[参照]** をクリックし、検索ボックスに `Microsoft.IdentityModel.Clients.ActiveDirectory' と入力します。
4. パッケージを選択し、ソリューションの [Manage Packages for Your Solution]\(ソリューションのパッケージ管理\) で **IntuneDataWarehouseSamples** プロジェクトを選択し、**[インストール]** をクリックします。 
5. **[同意する]** をクリックし、NuGet パッケージ ライセンスに同意します。
6. ソリューション エクスプローラーから `Program.cs` を開きます。

    ![Visual Studio のプロジェクト](media\reports-get_rest_data_in.png)

7.  Program.cs のコードを次のコードに置き換えます。  
    ```csharp
namespace IntuneDataWarehouseSamples
{
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    class Program
    {
     static void Main(string[] args)
  {
   /**
    * TODO: Replace the below values with your own.
    * emailAddress - The email address of the user that you will authenticate as.
    *
    * password  - The password for the above email address.
    *    This is inline only for simplicity in this sample. We do not 
    *    recommend storing passwords in plaintext.
    *
    * applicationId - The application ID of the native app that was created in AAD.
    *
    * warehouseUrl   - The data warehouse URL for your tenant. This can be found in 
    *      the Azure portal.
    * 
    * collectionName - The name of the warehouse entity collection you would like to 
    *      access.
    */
   var emailAddress = "intuneadmin@yourcompany.com";
   var password = "password_of(intuneadmin@yourcompany.com)";
   var applicationId = "<Application ID>";
   var warehouseUrl = "https://fef.{yourinfo}.manage.microsoft.com/ReportingService/DataWarehouseFEService?api-version=beta";
   var collectionName = "dates";

   var adalContext = new AuthenticationContext("https://login.windows.net/common/oauth2/token");
   AuthenticationResult authResult = adalContext.AcquireTokenAsync(
    resource: "https://api.manage.microsoft.com/",
    clientId: applicationId,
    userCredential: new UserPasswordCredential(emailAddress, password)).Result;

   var httpClient = new HttpClient();
   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);

   var uriBuilder = new UriBuilder(warehouseUrl);
   uriBuilder.Path += "/" + collectionName;

   HttpResponseMessage response = httpClient.GetAsync(uriBuilder.Uri).Result;

   Console.Write(response.Content.ReadAsStringAsync().Result);
   Console.ReadKey();
  }
    }
    ```

8.  コード サンプルの `TODO` を更新します。
9.  **Ctrl + F5** を押し、デバッグ モードで Intune.DataWarehouseAPIClient クライアントをビルドし、実行します。

    ![JSON 形式で取得された日付エンティティ。](media\reports-get_rest_data_output.png)

10.  コンソールの出力を確認します。 出力には、JSON 形式のデータが含まれています。これは Intune テナントの **dates** エンティティから引き出されたものです。

## <a name="next-steps"></a>次のステップ

認証、API URL 構造、OData エンドポイントの詳細は、「[Intune データ ウェアハウス API を使用する](reports-api-url.md)」にあります。 

「Intune データ ウェアハウスのデータ モデル」にも、API に含まれるデータ エンティティがあります。 詳細については、「[Intune データ ウェアハウス API データ モデル](reports-ref-data-model.md)」を参照してください。