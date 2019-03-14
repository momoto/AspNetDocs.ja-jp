---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: メンバーシップ |Microsoft Docs
author: microsoft
description: ASP.NET から ASP.NET メンバーシップが、成功すると、フォーム認証モデルのビルド 1.x します。 ASP.NET フォーム認証では、incorp する便利な手段を提供しています.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: d7fa3cb61608ea089141931cb9362359cdc92619
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57031469"
---
<a name="membership"></a><span data-ttu-id="6f55a-104">メンバーシップ</span><span class="sxs-lookup"><span data-stu-id="6f55a-104">Membership</span></span>
====================
<span data-ttu-id="6f55a-105">によって[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="6f55a-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="6f55a-106">ASP.NET から ASP.NET メンバーシップが、成功すると、フォーム認証モデルのビルド 1.x します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-106">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="6f55a-107">ASP.NET フォーム認証では、ログイン フォームを ASP.NET アプリケーションに組み込むし、データベースまたは他のデータ ストアに対してユーザーを検証する便利な手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-107">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span>


<span data-ttu-id="6f55a-108">ASP.NET から ASP.NET メンバーシップが、成功すると、フォーム認証モデルのビルド 1.x します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-108">ASP.NET Membership builds on the success of the Forms authentication model from ASP.NET 1.x.</span></span> <span data-ttu-id="6f55a-109">ASP.NET フォーム認証では、ログイン フォームを ASP.NET アプリケーションに組み込むし、データベースまたは他のデータ ストアに対してユーザーを検証する便利な手段を提供します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-109">ASP.NET Forms authentication provides a convenient way to incorporate a login form into your ASP.NET application and validate users against a database or other data store.</span></span> <span data-ttu-id="6f55a-110">FormsAuthentication クラスのメンバーでは、認証 cookie の処理、有効なログインを確認、ユーザーをサインアウトなどのログできるようにします。ただし、ASP.NET 1.x アプリケーションでフォーム認証を実装すると、大量のコードを要求できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-110">The members of the FormsAuthentication class make it possible to handle cookies for authentication, check for a valid login, log a user out etc. However, implementing Forms authentication in an ASP.NET 1.x application can require a fair amount of code.</span></span>

<span data-ttu-id="6f55a-111">ASP.NET 2.0 メンバーシップは、だけでフォーム認証を使用する場合より大きく進歩しています。</span><span class="sxs-lookup"><span data-stu-id="6f55a-111">Membership in ASP.NET 2.0 is a major advancement over using Forms authentication alone.</span></span> <span data-ttu-id="6f55a-112">(メンバーシップは、フォーム認証と組み合わせると、最も堅牢ながフォーム認証の使用は必須ではありません)。すぐにわかるよう、多くのコードをまったく記述しなくても、強力なメンバーシップ システムを実装するために ASP.NET 2.0 の ASP.NET メンバーシップと login コントロールを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-112">(Membership is most robust when coupled with Forms authentication, but using Forms authentication is not a requirement.) As you'll soon see, you can use ASP.NET Membership and the login controls in ASP.NET 2.0 to implement a powerful membership system without writing much code at all.</span></span>

## <a name="implementing-membership-in-aspnet-20"></a><span data-ttu-id="6f55a-113">ASP.NET 2.0 のメンバーシップを実装します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-113">Implementing Membership in ASP.NET 2.0</span></span>

<span data-ttu-id="6f55a-114">メンバーシップは、次の 4 つの手順によって実装されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-114">Membership is implemented by following four steps.</span></span> <span data-ttu-id="6f55a-115">同様に実装できるオプションの構成と関連する多くのサブ手順があることに留意してください。</span><span class="sxs-lookup"><span data-stu-id="6f55a-115">Keep in mind that there are many sub-steps that are involved as well as optional configuration that can be implemented as well.</span></span> <span data-ttu-id="6f55a-116">次の手順は、メンバーシップの構成の全体像を説明するものです。</span><span class="sxs-lookup"><span data-stu-id="6f55a-116">These steps are meant to illustrate the big picture of configuring membership.</span></span>

1. <span data-ttu-id="6f55a-117">メンバーシップ データベースを作成 (SQL Server として使用する場合、メンバーシップ ストアです。)</span><span class="sxs-lookup"><span data-stu-id="6f55a-117">Create your membership database (if SQL Server is used as the membership store.)</span></span>
2. <span data-ttu-id="6f55a-118">アプリケーション構成ファイルでのメンバーシップ オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-118">Specify the membership options in your applications configuration files.</span></span> <span data-ttu-id="6f55a-119">(メンバーシップは既定で有効です)。</span><span class="sxs-lookup"><span data-stu-id="6f55a-119">(Membership is enabled by default.)</span></span>
3. <span data-ttu-id="6f55a-120">使用するメンバーシップ ストアの種類を決定します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-120">Determine the type of membership store you want to use.</span></span> <span data-ttu-id="6f55a-121">オプション:</span><span class="sxs-lookup"><span data-stu-id="6f55a-121">Options are:</span></span> 

    - <span data-ttu-id="6f55a-122">Microsoft SQL Server (バージョン 7.0 以降)</span><span class="sxs-lookup"><span data-stu-id="6f55a-122">Microsoft SQL Server (version 7.0 or later)</span></span>
    - <span data-ttu-id="6f55a-123">Active Directory ストア</span><span class="sxs-lookup"><span data-stu-id="6f55a-123">Active Directory Store</span></span>
    - <span data-ttu-id="6f55a-124">カスタム メンバーシップ プロバイダー</span><span class="sxs-lookup"><span data-stu-id="6f55a-124">Custom membership provider</span></span>
4. <span data-ttu-id="6f55a-125">ASP.NET フォーム認証用のアプリケーションを構成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-125">Configure the application for ASP.NET Forms authentication.</span></span> <span data-ttu-id="6f55a-126">もう一度、メンバーシップは、フォーム認証を活用するために設計されていますが、フォーム認証の使用は必須ではありません。</span><span class="sxs-lookup"><span data-stu-id="6f55a-126">Once again, Membership is designed to take advantage of Forms authentication, but using Forms authentication is not a requirement.</span></span>
5. <span data-ttu-id="6f55a-127">メンバーシップのユーザー アカウントを定義し、必要な場合は、ロールを構成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-127">Define user accounts for membership and configure roles if desired.</span></span>

## <a name="creating-the-membership-database"></a><span data-ttu-id="6f55a-128">メンバーシップ データベースを作成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-128">Creating the Membership Database</span></span>

<span data-ttu-id="6f55a-129">場合は SQL Server 7.0 を使用しているか、後で、メンバーシップ ストアとして aspnet を使用することができます\_regsql ユーティリティ (使用可能な最も簡単に、Visual Studio .NET 2005 コマンド プロンプトから)、データベースを構成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-129">If youre using SQL Server 7.0 or later as your membership store, you can use the aspnet\_regsql utility (available most easily from the Visual Studio .NET 2005 Command Prompt) to configure your database.</span></span> <span data-ttu-id="6f55a-130">Aspnet\_としてコマンド プロンプト ツールまたは GUI ウィザードを使用して、regsql ユーティリティを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-130">The aspnet\_regsql utility can be used as a command prompt tool or via a GUI wizard.</span></span> <span data-ttu-id="6f55a-131">ウィザード メソッドは、データベースを構成する最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="6f55a-131">The wizard method is the easiest way to configure your database.</span></span> <span data-ttu-id="6f55a-132">ウィザードにアクセスするには、次のコマンドを実行だけです。</span><span class="sxs-lookup"><span data-stu-id="6f55a-132">To access the wizard, simply run the following command:</span></span>

`aspnet_regsql W`

<span data-ttu-id="6f55a-133">そのコマンドを実行すると次に示す ASP.NET SQL Server セットアップ ウィザードに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-133">Once you run that command, you will be presented with the ASP.NET SQL Server Setup Wizard as shown below.</span></span>


![](membership/_static/image1.jpg)

<span data-ttu-id="6f55a-134">**図 1**</span><span class="sxs-lookup"><span data-stu-id="6f55a-134">**Figure 1**</span></span>


<span data-ttu-id="6f55a-135">ASP.NET SQL Server セットアップ ウィザードは、ウィザードで指定したインスタンスで、Web サイトを作成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-135">The ASP.NET SQL Server Setup Wizard creates the Web site in the instance you specify in the wizard.</span></span> <span data-ttu-id="6f55a-136">ただし、ASP.NET は、データベースに接続する、machine.config ファイルで接続文字列が使用されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-136">However, ASP.NET will use the connection string in the machine.config file to connect to your database.</span></span> <span data-ttu-id="6f55a-137">既定では、この接続文字列は、SQL Server 2005 のインスタンスをポイントは、SQL Server 2000 または SQL Server 7.0 のインスタンスを使用している、machine.config ファイルで接続文字列を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-137">By default, this connection string will point to a SQL Server 2005 instance, so if you are using a SQL Server 2000 or SQL Server 7.0 instance, you will need to modify the connection string in the machine.config file.</span></span> <span data-ttu-id="6f55a-138">その接続文字列は、ここに配置できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-138">That connection string can be located here:</span></span>

[!code-xml[Main](membership/samples/sample1.xml)]

<span data-ttu-id="6f55a-139">残念ながら、接続文字列を変更しない場合は、ASP.NET は与えない記述的なエラー。</span><span class="sxs-lookup"><span data-stu-id="6f55a-139">Unfortunately, if you dont modify the connection string, ASP.NET will not give you a descriptive error.</span></span> <span data-ttu-id="6f55a-140">データベースを作成するいないと答えるから不満があがるは引き続きだけです。</span><span class="sxs-lookup"><span data-stu-id="6f55a-140">It will just continue to complain saying that you havent created the database.</span></span> <span data-ttu-id="6f55a-141">上記の例で、ローカルの SQL Server 2000 インスタンスを指す接続文字列を変更しました。</span><span class="sxs-lookup"><span data-stu-id="6f55a-141">In the case above, I have modified the connection string to point to my local SQL Server 2000 instance.</span></span>

## <a name="specifying-configuration-and-adding-users-and-roles"></a><span data-ttu-id="6f55a-142">構成および追加のユーザーとロールを指定します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-142">Specifying Configuration and Adding Users and Roles</span></span>

<span data-ttu-id="6f55a-143">メンバーシップの構成では、次の手順では、アプリケーションの web.config ファイルに必要な情報を追加します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-143">The next step in configuring Membership is to add the necessary information to the web.config file of the application.</span></span> <span data-ttu-id="6f55a-144">Asp.net 1.x では、web.config ファイルを変更することがありますは困難でした lowerCamelCase の使用と Intellisense の欠如のため。</span><span class="sxs-lookup"><span data-stu-id="6f55a-144">In ASP.NET 1.x, modifying the web.config file was sometimes difficult because of the use of lowerCamelCase and the lack of Intellisense.</span></span> <span data-ttu-id="6f55a-145">Visual Studio .NET 2005 により、タスクが構成ファイルでは、Intellisense を備えた非常に簡単ですが、ASP.NET 2.0 は、構成ファイルを編集するための Web インターフェイスを提供することでさらに、1 つのステップを移動します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-145">Visual Studio .NET 2005 makes the task much easier with Intellisense for configuration files, but ASP.NET 2.0 goes one step further by providing a Web interface for editing configuration files.</span></span>

<span data-ttu-id="6f55a-146">Web インターフェイスを起動するには、次に示すように、ソリューション エクスプ ローラー ツールバーで [ASP.NET 構成] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-146">You can launch the Web interface by clicking the ASP.NET Configuration button on the Solution Explorer toolbar as shown below.</span></span> <span data-ttu-id="6f55a-147">ログイン コントロールを挿入するときに表示されるポップアップを使用して、Web インターフェイスを起動することもできます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-147">You can also launch the Web interface via pop-ups that are displayed when Login controls are inserted.</span></span>


![](membership/_static/image2.jpg)

<span data-ttu-id="6f55a-148">**図 2**</span><span class="sxs-lookup"><span data-stu-id="6f55a-148">**Figure 2**</span></span>


<span data-ttu-id="6f55a-149">これは、次に示す ASP.NET Web サイト管理ツールを起動します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-149">This launches the ASP.NET Web Site Administration Tool shown below.</span></span> <span data-ttu-id="6f55a-150">ASP.NET Web サイトの管理は、アプリケーション設定を管理しやすく 4 タブ インターフェイスです。</span><span class="sxs-lookup"><span data-stu-id="6f55a-150">The ASP.NET Web Site Administration is a four-tab interface that makes it easy to manage application settings.</span></span> <span data-ttu-id="6f55a-151">次のタブを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-151">The following tabs are available:</span></span>

- <span data-ttu-id="6f55a-152">**Home**</span><span class="sxs-lookup"><span data-stu-id="6f55a-152">**Home**</span></span>
- <span data-ttu-id="6f55a-153">**セキュリティ**ユーザー、ロール、およびアクセスを構成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-153">**Security** Configure users, roles, and access.</span></span>
- <span data-ttu-id="6f55a-154">**アプリケーション**アプリケーション設定を構成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-154">**Application** Configure application settings.</span></span>
- <span data-ttu-id="6f55a-155">**プロバイダー**構成して、アプリケーションのメンバーシップ プロバイダーをテストします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-155">**Provider** Configure and test your applications membership provider.</span></span>

<span data-ttu-id="6f55a-156">Web サイトの管理ツールでは、簡単に新しいユーザーを作成、新しいロールを作成して、ユーザーとロールを管理できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-156">The Web Site Administration Tool allows you to easily create new users, create new roles, and to manage users and roles.</span></span> <span data-ttu-id="6f55a-157">Windows インターフェイスでは、この機能を使用できません。</span><span class="sxs-lookup"><span data-stu-id="6f55a-157">This ability is not available in the Windows interface.</span></span> <span data-ttu-id="6f55a-158">Windows インターフェイスでは承認の設定を簡単に定義と追加、削除、およびプロバイダー、Web サイト管理ツールではない機能の管理を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-158">The Windows interface allows you to easily define authorization settings and to add, delete, and manage providers, capabilities that are not in the Web Site Administration Tool.</span></span>

<span data-ttu-id="6f55a-159">Windows インターフェイスを起動するには、インターネット インフォメーション サービス スナップインを開く、アプリケーションを右クリックし、プロパティを選択します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-159">To launch the Windows interface, open the Internet Information Services snap-in, right-click on your application, and choose Properties.</span></span> <span data-ttu-id="6f55a-160">ASP.NET タブをクリックし、構成の編集 ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-160">Click the ASP.NET tab and then click the Edit Configuration button.</span></span> <span data-ttu-id="6f55a-161">(有効にする構成の編集 ボタンの ASP.NET 2.0 では、アプリケーションを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-161">(The application must be running under ASP.NET 2.0 for the Edit Configuration button to be enabled.</span></span> <span data-ttu-id="6f55a-162">構成できます ASP.NET のバージョン ASP.NET ダイアログ。)次に示すように、ASP.NET 構成の設定 ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-162">You can configure the ASP.NET version in the ASP.NET dialog as well.) The ASP.NET Configuration Settings dialog is displayed as shown below.</span></span>


![](membership/_static/image3.jpg)

<span data-ttu-id="6f55a-163">**図 3**</span><span class="sxs-lookup"><span data-stu-id="6f55a-163">**Figure 3**</span></span>


<span data-ttu-id="6f55a-164">[全般] タブで、接続文字列とアプリケーションの設定が一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-164">On the General tab, connection strings and application settings are listed.</span></span> <span data-ttu-id="6f55a-165">斜体の設定は親構成ファイル (machine.config ファイルまたは高いレベルの web.config) で定義され、斜体ではなく設定は、アプリケーション構成ファイルから。</span><span class="sxs-lookup"><span data-stu-id="6f55a-165">Any settings in italics are defined in a parent configuration file (either the machine.config or a web.config at a higher level) and settings not in italics are from the applications configuration file.</span></span> <span data-ttu-id="6f55a-166">場合は、設定を追加すると、削除、またはアプリケーション レベルでは、編集 ASP.NET は追加、削除、または継承元となる構成ファイルから設定を削除する代わりに、アプリケーション レベルの web.config で設定を変更します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-166">If a setting is added, removed, or edited at the application level, ASP.NET will add, remove, or modify the setting at the application levels web.config instead of removing the setting from the configuration file from which it is inherited.</span></span>

<span data-ttu-id="6f55a-167">[認証] タブは、以下に示します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-167">The Authentication tab is shown below.</span></span> <span data-ttu-id="6f55a-168">これは、メンバーシップの設定を構成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-168">This is where you will configure your membership settings.</span></span> <span data-ttu-id="6f55a-169">メンバーシップ プロバイダーでの認証設定を作成し、ロール プロバイダーをここで構成できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-169">Forms authentication settings, membership providers, and role providers can be configured here.</span></span>


![](membership/_static/image4.jpg)

<span data-ttu-id="6f55a-170">**図 4**</span><span class="sxs-lookup"><span data-stu-id="6f55a-170">**Figure 4**</span></span>


## <a name="implementing-membership-in-your-application"></a><span data-ttu-id="6f55a-171">アプリケーションでのメンバーシップの実装</span><span class="sxs-lookup"><span data-stu-id="6f55a-171">Implementing Membership in Your Application</span></span>

<span data-ttu-id="6f55a-172">指定されたログオン コントロールを使用すること、アプリケーションで ASP.NET 2.0 メンバーシップを実装する最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="6f55a-172">The easiest way to implement ASP.NET 2.0 membership in your application is to use the provided Logon controls.</span></span> <span data-ttu-id="6f55a-173">このメソッド コードをまったく記述せずに ASP.NET 2.0 メンバーシップの基本を実装することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-173">This method allows you to implement the basics of ASP.NET 2.0 membership without writing any code at all.</span></span>

<span data-ttu-id="6f55a-174">次のログオン コントロールは ASP.NET 2.0 です。</span><span class="sxs-lookup"><span data-stu-id="6f55a-174">The following Logon controls are available in ASP.NET 2.0:</span></span>

## <a name="login-control"></a><span data-ttu-id="6f55a-175">Login コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-175">Login Control</span></span>

<span data-ttu-id="6f55a-176">Login コントロールは、他のユーザーがメンバーシップ システムにログインするためのインターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-176">The Login control provides an interface for someone to log into your membership system.</span></span> <span data-ttu-id="6f55a-177">ユーザー名とパスワード textboxt とログイン ボタンに提供します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-177">It provides you with a username and password textboxt and a login button.</span></span> <span data-ttu-id="6f55a-178">他の一般的ななど多くの機能をまだ行っていないため、アクセスする際に自動的にログインにユーザーにより、チェック ボックスをユーザーに登録リンクをパスワード関連語句などへのリンク。Login コントロールのすべての機能は、コントロールのプロパティを使用してカスタマイズできます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-178">Many other common features such as a link to register for people who have not yet done so, a checkbox that allows the user to automatically login on subsequent visits, a link for a password reminder, etc. All features of the Login control are customizable via the properties of the control.</span></span>

<span data-ttu-id="6f55a-179">Asp.net 1.x では、開発者は、かなりのフォーム認証を使用する場合は、ルックアップを実行するためのコードを記述する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-179">In ASP.NET 1.x, developers had to write a fair amount of code to do a lookup when using Forms authentication.</span></span> <span data-ttu-id="6f55a-180">ASP.NET 2.0 のメンバーシップを持つ任意のコードをまったく記述しなくてもユーザーを検証できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-180">With ASP.NET 2.0 membership, you can validate users without writing any code at all.</span></span> <span data-ttu-id="6f55a-181">ASP.NET は自動的にユーザーの検索処理を実行します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-181">ASP.NET will automatically do the look-up of the user for you.</span></span> <span data-ttu-id="6f55a-182">(ASP.NET メンバーシップを使用せず、Login コントロールを使用する場合は、使用、 **OnAuthenticate**ユーザーを検証するメソッド)。</span><span class="sxs-lookup"><span data-stu-id="6f55a-182">(If you are using the Login control without using ASP.NET membership, you can use the **OnAuthenticate** method to validate the user.)</span></span>

## <a name="loginview-control"></a><span data-ttu-id="6f55a-183">LoginView コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-183">LoginView Control</span></span>

<span data-ttu-id="6f55a-184">LoginView コントロールが既定では 2 つのテンプレートを提供するテンプレート コントロールです。AnonymousTemplate し、LoggedInTemplate します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-184">The LoginView control is a templated control that provides two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="6f55a-185">表示されるテンプレートは、ユーザーがメンバーシップ システムにログインするかどうかによって決まります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-185">The template that is displayed is determined by whether or not the user is logged into your membership system.</span></span> <span data-ttu-id="6f55a-186">このコントロールは通常、ユーザー ログインしているときに、ユーザーがまだログインしていないときのログイン コントロール、LoginStatus コントロールやその他のログイン コントロールを表示する使用されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-186">This control is typically used to display a Login control when a user has not yet logged in and a LoginStatus control and/or other login controls when the user has logged in.</span></span> <span data-ttu-id="6f55a-187">ASP.NET アプリケーションでロールの管理を使用する場合、LoginView コントロールは、ユーザー ロールに基づいて、特定のテンプレートを表示できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-187">If you are using role management in your ASP.NET application, the LoginView control can display a specific template based upon the users role.</span></span> <span data-ttu-id="6f55a-188">(より ASP.NET のロール管理については、後ほど。)</span><span class="sxs-lookup"><span data-stu-id="6f55a-188">(More on ASP.NET role management will be covered later.)</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="6f55a-189">PasswordRecovery コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-189">PasswordRecovery Control</span></span>

<span data-ttu-id="6f55a-190">PasswordRecovery コントロールでは、現在のパスワードを自分で電子メールを受信するか、自分のパスワードをリセットできます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-190">The PasswordRecovery control allows users to receive an email with his or her current password or reset his or her password.</span></span> <span data-ttu-id="6f55a-191">クリア テキストと暗号化されたパスワードを回復およびユーザーに電子メールで送信します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-191">Clear text and encrypted passwords can be recovered and emailed to users.</span></span> <span data-ttu-id="6f55a-192">パスワードがハッシュされる場合は回復できません。</span><span class="sxs-lookup"><span data-stu-id="6f55a-192">If the password is hashed, it cannot be recovered.</span></span> <span data-ttu-id="6f55a-193">代わりに、ユーザーは、パスワード リセットを実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-193">Instead the user will be required to perform a password reset.</span></span>

## <a name="loginstatus-control"></a><span data-ttu-id="6f55a-194">LoginStatus コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-194">LoginStatus Control</span></span>

<span data-ttu-id="6f55a-195">現在ログオンしているユーザーにログインしていないユーザーにログイン インジケーターとログアウト インジケーターを表示する、LoginStatus コントロールが使用されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-195">The LoginStatus control is used to display a login indicator to users who are not logged in and a logout indicator to users who are currently logged in.</span></span> <span data-ttu-id="6f55a-196">Request.IsAuthenticated プロパティは、表示するインジケーターの決定に使用されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-196">The Request.IsAuthenticated property is used to determine which indicator to display.</span></span> <span data-ttu-id="6f55a-197">LoginStatus コントロールによって表示されるインジケーターは、テキストを指定できます (を使用して実装、 **LoginText**と**LogoutText**プロパティ) やイメージ (を使用して実装、 **LoginImageUrl**と**LogoutImageUrl**プロパティです)。</span><span class="sxs-lookup"><span data-stu-id="6f55a-197">The indicator displayed by the LoginStatus control can be text (implemented via the **LoginText** and **LogoutText** properties) or images (implemented via the **LoginImageUrl** and **LogoutImageUrl** properties.)</span></span>

<span data-ttu-id="6f55a-198">によって指定された URL にそのユーザーをリダイレクトする、LoginStatus コントロールを使用して、ユーザーがログアウト、 **LogoutPageUrl**プロパティ。</span><span class="sxs-lookup"><span data-stu-id="6f55a-198">When a user logs out via the LoginStatus control, he or she is redirected to the URL specified by the **LogoutPageUrl** property.</span></span> <span data-ttu-id="6f55a-199">そのプロパティが設定されていない場合は、現在のページが更新されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-199">If that property is not set, the current page is refreshed.</span></span> <span data-ttu-id="6f55a-200">サイトはフォーム認証で保護されている可能性があります、ために、現在のページの更新は、ユーザーをサイトのログイン ページにリダイレクトされます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-200">Since the site is likely protected by Forms authentication, the refresh of the current page will redirect the user to the login page for the site.</span></span>

## <a name="loginname-control"></a><span data-ttu-id="6f55a-201">LoginName コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-201">LoginName Control</span></span>

<span data-ttu-id="6f55a-202">LoginName コントロールは、現在、サイトにログインしてユーザーのユーザー名を表示します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-202">The LoginName control displays the username of the user currently logged into the site.</span></span>

## <a name="createuserwizard-control"></a><span data-ttu-id="6f55a-203">CreateUserWizard コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-203">CreateUserWizard Control</span></span>

<span data-ttu-id="6f55a-204">CreateUserWizard コントロールは、メンバーシップ システムに登録する便利な方法でユーザーを提供します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-204">The CreateUserWizard control provides users with a convenient way to register for your membership system.</span></span> <span data-ttu-id="6f55a-205">次に示すインターフェイスを使用して、(WizardSteps のコレクションとして実装) ステップを追加することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-205">You can add steps (implemented as a collection of WizardSteps) via the interface shown below.</span></span>


![](membership/_static/image5.jpg)

<span data-ttu-id="6f55a-206">**図 5**</span><span class="sxs-lookup"><span data-stu-id="6f55a-206">**Figure 5**</span></span>


<span data-ttu-id="6f55a-207">CreateUserWizard は、ウィザード クラスから派生し、次のテンプレートを提供します、template 宣言されたコントロールを示します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-207">The CreateUserWizard is a templated control that derives from the Wizard class and provides the following templates:</span></span>

- <span data-ttu-id="6f55a-208">**Header テンプレート**このテンプレートは、ウィザードのヘッダーの外観を制御します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-208">**HeaderTemplate** This template controls the appearance of the header of the wizard.</span></span>
- <span data-ttu-id="6f55a-209">**SidebarTemplate**このテンプレートは、ウィザードのサイド バーの外観を制御します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-209">**SidebarTemplate** This template controls the appearance of the sidebar of the wizard.</span></span>
- <span data-ttu-id="6f55a-210">**StartNavigationTemplate**スタートの手順で、ウィザードのナビゲーションの外観が、このテンプレートを制御します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-210">**StartNavigationTemplate** This template controls the appearance of the navigation are of the wizard at the start step.</span></span>
- <span data-ttu-id="6f55a-211">**StepNavigationTemplate**このテンプレートは、開始日または終了の手順ではないときのナビゲーション領域の外観を制御します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-211">**StepNavigationTemplate** This template controls the appearance of the navigation area when not in the start or finish step.</span></span>
- <span data-ttu-id="6f55a-212">**FinishNavigationTemplate**このテンプレートは、[完了] 手順でのナビゲーション領域の外観を制御します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-212">**FinishNavigationTemplate** This template controls the appearance of the navigation area when on the finish step.</span></span>

<span data-ttu-id="6f55a-213">さらに、ウィザードに追加する各手順では、ASP.NET では、ContentTemplate とそのステップの CustomNavigationTemplate の両方を含むカスタム テンプレート作成されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-213">Additionally, for each step that you add to the Wizard, ASP.NET will create a custom template that contains both a ContentTemplate and a CustomNavigationTemplate for that step.</span></span> <span data-ttu-id="6f55a-214">CreateUserWizard をカスタマイズする方法の詳細については、VS.NET 2005 のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6f55a-214">For full details on customizing the CreateUserWizard, see the VS.NET 2005 documentation:</span></span>

## <a name="changepassword-control"></a><span data-ttu-id="6f55a-215">ChangePassword コントロール</span><span class="sxs-lookup"><span data-stu-id="6f55a-215">ChangePassword Control</span></span>

<span data-ttu-id="6f55a-216">ChangePassword コントロールでは、自分のパスワードを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-216">The ChangePassword control allows users to change his or her password.</span></span> <span data-ttu-id="6f55a-217">DisplayUserName プロパティが true (既定では false です) ログインしていないときに、ユーザーは自分のパスワードを変更できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-217">If the DisplayUserName property is true (it is false by default), the user can change his or her password when they are not logged in.</span></span> <span data-ttu-id="6f55a-218">場合、ユーザー*は*既にログインして DisplayUserName プロパティが true をユーザーがそのユーザーのユーザー ID を知っているが提供するためにログインしていない別のユーザーのパスワードを変更できるようなります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-218">If the user *is* already logged in and the DisplayUserName property is true, the user will be able to change the password of another user that is not logged in providing they know the user ID of that user.</span></span>

<span data-ttu-id="6f55a-219">ユーザーにログインすることがなくパスワードを変更できるようにする場合が必要で、ChangePassword コントロールが表示されるページは匿名アクセスを許可することに留意してください。</span><span class="sxs-lookup"><span data-stu-id="6f55a-219">Keep in mind that if you want users to be able to change passwords without having to log in, you will need to ensure that the page on which the ChangePassword control is displayed allows anonymous access.</span></span> <span data-ttu-id="6f55a-220">当然ながら、ユーザーが自分のパスワードを変更するには、古いパスワードを提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-220">Obviously, users will have to provide their old password in order to change their password.</span></span>

## <a name="role-management"></a><span data-ttu-id="6f55a-221">ロール管理</span><span class="sxs-lookup"><span data-stu-id="6f55a-221">Role Management</span></span>

<span data-ttu-id="6f55a-222">ロール管理を使用すると、特定のロールにユーザーを割り当てるし、特定のファイルまたはそのロールに基づいたフォルダーへのアクセスを制限できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-222">Role management allows you to assign users to a particular role and then restrict access to certain file or folders based on that role.</span></span> <span data-ttu-id="6f55a-223">ロール管理では、プログラムによって使いのロールを確認または特定のロールのすべてのユーザーを確認して適宜応答できるように、API も提供します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-223">Role management also provides an API so that you can programmatically determine someones role or determine all users in a particular role and respond accordingly.</span></span>

<span data-ttu-id="6f55a-224">ロール管理は、ASP.NET メンバーシップの要件ではありませんもはメンバーシップ ロール管理を使用するために必要になります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-224">Role management is not a requirement in ASP.NET membership, nor is membership a requirement in order to use role management.</span></span> <span data-ttu-id="6f55a-225">ただし、2 つは、互いを適切に補完し、場合、開発者は相互に組み合わせてそれらに使用します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-225">However, the two supplement each other nicely and it is likely that developers will use them in conjunction with each other.</span></span>

<span data-ttu-id="6f55a-226">アプリケーションでロールの管理を有効にするには、web.config ファイルで、次の変更を行います。</span><span class="sxs-lookup"><span data-stu-id="6f55a-226">To enable role management in your application, make the following change in your web.config file:</span></span>

[!code-xml[Main](membership/samples/sample2.xml)]

<span data-ttu-id="6f55a-227">ときに、 **cacheRolesInCookie**属性に設定されて true の場合、ASP.NET キャッシュ クライアントの cookie にユーザー ロールのメンバーシップ。</span><span class="sxs-lookup"><span data-stu-id="6f55a-227">When the **cacheRolesInCookie** attribute is set to true, ASP.NET caches a users role membership in a cookie on the client.</span></span> <span data-ttu-id="6f55a-228">これにより、ロール プロバイダーへの呼び出しなしに行われるロールの参照です。</span><span class="sxs-lookup"><span data-stu-id="6f55a-228">This allows role lookups to occur without calls into the RoleProvider.</span></span> <span data-ttu-id="6f55a-229">いることを確認する開発者はこの属性を使用する場合、 **cookieProtection**属性がすべてに設定します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-229">When using this attribute, developers are encouraged to ensure that the **cookieProtection** attribute is set to All.</span></span> <span data-ttu-id="6f55a-230">(これは、既定の設定です)。これにより、cookie のデータが暗号化され、cookie の内容が変更されていないことを確認するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-230">(This is the default setting.) This ensures that the cookie data are encrypted and helps to ensure that the cookies contents havent been altered.</span></span> <span data-ttu-id="6f55a-231">Web サイトの管理ツールを使用して、ロールを追加できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-231">Roles can be added using the Web Site Administration Tool.</span></span> <span data-ttu-id="6f55a-232">簡単にロールを定義し、これらの役割に基づいた、サイトの部分へのアクセスを構成し、ユーザー ロールを割り当てることができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-232">It allows you to easily define roles, configure access to parts of the site based on those roles, and assign users to roles.</span></span>


![](membership/_static/image6.jpg)

<span data-ttu-id="6f55a-233">**図 6**</span><span class="sxs-lookup"><span data-stu-id="6f55a-233">**Figure 6**</span></span>


<span data-ttu-id="6f55a-234">上記のように、ロールの名前を入力するだけ、[役割の追加] をクリックして新しいロールを追加できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-234">As shown above, new roles can be added by simply entering the name of the role and then clicking Add Role.</span></span> <span data-ttu-id="6f55a-235">既存のロールを管理または既存のロールの一覧で、適切なリンクをクリックして削除できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-235">Existing roles can be managed or deleted by clicking the appropriate link in the list of existing roles.</span></span>

<span data-ttu-id="6f55a-236">ロールを管理する場合は、追加または次に示すようにユーザーを削除できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-236">When you manage a role, you can add or remove users as shown below.</span></span>


![](membership/_static/image7.jpg)

<span data-ttu-id="6f55a-237">**図 7**</span><span class="sxs-lookup"><span data-stu-id="6f55a-237">**Figure 7**</span></span>


<span data-ttu-id="6f55a-238">ロールのユーザーは、チェック ボックスをチェックして、特定のロールにユーザーを簡単に追加できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-238">By checking the User Is In Role checkbox, you can easily add a user to a specific role.</span></span> <span data-ttu-id="6f55a-239">ASP.NET は、適切なエントリで、メンバーシップ データベースを自動的に更新されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-239">ASP.NET will automatically update your membership database with the appropriate entries.</span></span> <span data-ttu-id="6f55a-240">アプリケーションのアクセス規則を構成するされます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-240">You will also want to configure access rules for your application.</span></span> <span data-ttu-id="6f55a-241">ASP.NET 1.x の開発者が使用してこれを行う使い慣れて、&lt;承認&gt;内の要素、web.config ファイルおよびそのオプションは、ASP.NET 2.0 で引き続き使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-241">ASP.NET 1.x developers are familiar with doing this via the &lt;authorization&gt; element in the web.config file, and that option is still available in ASP.NET 2.0.</span></span> <span data-ttu-id="6f55a-242">ただし、ツールを使用して、Web サイトの管理に示すように以下をアクセスを管理する方が簡単にルールします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-242">However, its easier to manage access rules using the Web Site Administration Tool as shown below.</span></span>


![](membership/_static/image8.jpg)

<span data-ttu-id="6f55a-243">**図 8**</span><span class="sxs-lookup"><span data-stu-id="6f55a-243">**Figure 8**</span></span>


<span data-ttu-id="6f55a-244">この場合は、管理フォルダーが強調表示されます (そのがわかりにくく、ツールが淡い灰色でそれを強調するため) と、管理者ロールにアクセスが許可されています。</span><span class="sxs-lookup"><span data-stu-id="6f55a-244">In this case, the Administration folder is highlighted (its difficult to see because the tool highlights it in light gray) and the Administrators role has been granted access.</span></span> <span data-ttu-id="6f55a-245">その他のすべてのユーザーが拒否されました。</span><span class="sxs-lookup"><span data-stu-id="6f55a-245">All other users are denied.</span></span> <span data-ttu-id="6f55a-246">ルールを選択し、上へ移動し、下へ移動 ボタンを使用してルールを並べ替えますヘッドのアイコンをクリックすることができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-246">You can click on the head icon to select a rule and then use the Move Up and Move Down buttons to arrange the rules.</span></span> <span data-ttu-id="6f55a-247">ASP.NET と同様&lt;承認&gt;要素、規則が表示される順序で処理されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-247">As with the ASP.NET &lt;authorization&gt; element, rules are processed in the order in which they appear.</span></span> <span data-ttu-id="6f55a-248">つまり、ショット上記の規則の順序を反転させた場合だれする必要がありますアクセス管理フォルダー ASP.NET が発生する最初の規則がフォルダーにすべてのユーザーを拒否する規則になるためです。</span><span class="sxs-lookup"><span data-stu-id="6f55a-248">In other words, if the order of rules in the shot above were reversed, no one would have access to the Administration folder because the first rule that ASP.NET would encounter would be the rule that denies everyone to the folder.</span></span>

<span data-ttu-id="6f55a-249">ASP.NET 2.0 では、アクセス規則を指定するフォルダーに web.config ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-249">ASP.NET 2.0 adds a web.config file to the folder for which you are specifying an access rule.</span></span> <span data-ttu-id="6f55a-250">構成ファイルを使用して、または Web サイトの管理ツールを使用して、アクセス規則を編集できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-250">Access rules can be edited via the configuration file or via the Web Site Administration Tool.</span></span> <span data-ttu-id="6f55a-251">つまり、Web サイトの管理ツールでは、使いやすい環境で使用される構成ファイルを編集できますインターフェイスだけです。</span><span class="sxs-lookup"><span data-stu-id="6f55a-251">In other words, the Web Site Administration Tool is simply an interface through which the configuration file can be edited in a user-friendly environment.</span></span>

## <a name="using-roles-in-code"></a><span data-ttu-id="6f55a-252">コードでロールの使用</span><span class="sxs-lookup"><span data-stu-id="6f55a-252">Using Roles in Code</span></span>

<span data-ttu-id="6f55a-253">ロール管理用の API がバージョン以降変更されていない 1.x します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-253">The API for role management has not changed since version 1.x.</span></span> <span data-ttu-id="6f55a-254">**IsInRole**メソッドを使用して、ユーザーが特定のロールがあるか判断します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-254">The **IsInRole** method is used to determine if a user is in a particular role.</span></span>

[!code-csharp[Main](membership/samples/sample3.cs)]

<span data-ttu-id="6f55a-255">ASP.NET では、現在のコンテキストのメンバーとして RolePrincipal インスタンスも作成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-255">ASP.NET also creates a RolePrincipal instance as a member of the current context.</span></span> <span data-ttu-id="6f55a-256">すべてのユーザーが次のように所属するロールを取得する RolePrincipal オブジェクトを使用できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-256">The RolePrincipal object can be used to obtain all of the roles to which the user belongs as follows:</span></span>

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a><span data-ttu-id="6f55a-257">LoginView コントロールで Rolegroup の使用</span><span class="sxs-lookup"><span data-stu-id="6f55a-257">Using RoleGroups with the LoginView Control</span></span>

<span data-ttu-id="6f55a-258">ロールの管理とメンバーシップについて理解したら、LoginView コントロールが ASP.NET 2.0 でこの機能を活用を受け取る方法について簡単に説明することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-258">Now that you have an understanding of role management and membership, lets discuss briefly how the LoginView control takes advantage of this capability in ASP.NET 2.0.</span></span> <span data-ttu-id="6f55a-259">既に説明したように、LoginView コントロールには既定では 2 つのテンプレートを含むテンプレート コントロールです。AnonymousTemplate し、LoggedInTemplate します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-259">As previously discussed, the LoginView control is a templated control that contains two templates by default; the AnonymousTemplate and the LoggedInTemplate.</span></span> <span data-ttu-id="6f55a-260">内の LoginView タスク ダイアログ (下図参照) のリンクは、RoleGroups を編集することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-260">Within the LoginView Tasks dialog is a link (shown below) that allows you to edit RoleGroups.</span></span>


![](membership/_static/image9.jpg)

<span data-ttu-id="6f55a-261">**図 9**</span><span class="sxs-lookup"><span data-stu-id="6f55a-261">**Figure 9**</span></span>


<span data-ttu-id="6f55a-262">各 RoleGroup オブジェクトには、RoleGroup が適用されるロールを定義する文字列の配列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="6f55a-262">Each RoleGroup object contains an array of strings that defines which roles that RoleGroup applies to.</span></span> <span data-ttu-id="6f55a-263">新しい RoleGroup を LoginView コントロールを追加するには、Rolegroup の編集リンクをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-263">To add a new RoleGroup to the LoginView control, click the Edit RoleGroups link.</span></span> <span data-ttu-id="6f55a-264">上記の図では、管理者用の新しい RoleGroup を追加することがわかります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-264">In the image above, you can see that I have added a new RoleGroup for Administrators.</span></span> <span data-ttu-id="6f55a-265">その RoleGroup を選択して (RoleGroup[0]) ビュー ドロップダウン リストから、構成できます管理者ロールのメンバーにのみ表示されるテンプレート。</span><span class="sxs-lookup"><span data-stu-id="6f55a-265">By selecting that RoleGroup (RoleGroup[0]) from the Views dropdown, I can configure a template that will only be displayed to members of the Administrators role.</span></span> <span data-ttu-id="6f55a-266">次の図に、Sales ロールおよび配布ロールのメンバーに適用される新しい RoleGroup を追加しました。</span><span class="sxs-lookup"><span data-stu-id="6f55a-266">In the image below, I have added a new RoleGroup that applies to members of the Sales role and the Distribution role.</span></span> <span data-ttu-id="6f55a-267">2 番目の RoleGroup LoginView タスク ダイアログ ボックスで、ビューのドロップダウン リストに追加され、そのテンプレートに追加されたものは、販売またはディストリビューション内のユーザーが表示されますロール。</span><span class="sxs-lookup"><span data-stu-id="6f55a-267">This adds a second RoleGroup to the Views dropdown in the LoginView Tasks dialog and anything added to that template will be visible by any user in either the Sales or Distribution role.</span></span>


![](membership/_static/image10.jpg)

<span data-ttu-id="6f55a-268">**図 10**</span><span class="sxs-lookup"><span data-stu-id="6f55a-268">**Figure 10**</span></span>


## <a name="overriding-the-existing-membership-provider"></a><span data-ttu-id="6f55a-269">既存のメンバーシップ プロバイダーをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-269">Overriding the Existing Membership Provider</span></span>

<span data-ttu-id="6f55a-270">いくつかの ASP.NET メンバーシップの機能を拡張する方法があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-270">There are a couple of ways that you can extend the functionality of ASP.NET membership.</span></span> <span data-ttu-id="6f55a-271">まず、それを継承し、そのメソッドをオーバーライドして SqlMembershipProvider クラスの既存の機能を明らかに変更できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-271">First of all, you can obviously change the existing functionality of the SqlMembershipProvider class by inheriting from it and overriding its methods.</span></span> <span data-ttu-id="6f55a-272">たとえば、ユーザーの作成時に、独自の機能を実装する場合は、SqlMembershipProvider から次のように継承するクラスを作成することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-272">For example, if you want to implement your own functionality when users are created, you can create your own class that inherits from SqlMembershipProvider as follows:</span></span>

[!code-csharp[Main](membership/samples/sample5.cs)]

<span data-ttu-id="6f55a-273">その一方で、(たとえば、Access データベースにメンバーシップ情報の保存) を独自のプロバイダーを作成する場合、独自のプロバイダーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-273">If, on the other hand, you want to create your own provider (to store your membership information in an Access database, for example), you can create your own provider.</span></span>

## <a name="creating-your-own-membership-provider"></a><span data-ttu-id="6f55a-274">独自のメンバーシップ プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-274">Creating Your Own Membership Provider</span></span>

<span data-ttu-id="6f55a-275">独自のメンバーシップ プロバイダーを作成するには、MembershipProvider クラスから継承するクラスを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-275">To create your own membership provider, you will first need to create a class that inherits from the MembershipProvider class.</span></span> <span data-ttu-id="6f55a-276">VB.NET を使用している場合、Visual Studio 2005 はすべてのメソッドをオーバーライドする必要のあるスタブを追加します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-276">If you are using VB.NET, Visual Studio 2005 will add the stubs for all of the methods that you need to override.</span></span> <span data-ttu-id="6f55a-277">C#、スタブを追加することに使用している場合します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-277">If you are using C#, its up to you to add the stubs.</span></span>

<span data-ttu-id="6f55a-278">次をオーバーライドする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-278">You will need to override the following:</span></span>

- <span data-ttu-id="6f55a-279">ApplicationName プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-279">ApplicationName property</span></span>
- <span data-ttu-id="6f55a-280">ChangePassword 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-280">ChangePassword function</span></span>
- <span data-ttu-id="6f55a-281">ChangePasswordQuestionAndAnswer 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-281">ChangePasswordQuestionAndAnswer function</span></span>
- <span data-ttu-id="6f55a-282">CreateUser 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-282">CreateUser function</span></span>
- <span data-ttu-id="6f55a-283">DeleteUser 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-283">DeleteUser function</span></span>
- <span data-ttu-id="6f55a-284">EnablePasswordReset プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-284">EnablePasswordReset property</span></span>
- <span data-ttu-id="6f55a-285">EnablePasswordRetrieval プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-285">EnablePasswordRetrieval property</span></span>
- <span data-ttu-id="6f55a-286">FindUsersByEmail 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-286">FindUsersByEmail function</span></span>
- <span data-ttu-id="6f55a-287">FindUsersByName 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-287">FindUsersByName function</span></span>
- <span data-ttu-id="6f55a-288">GetAllUsers 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-288">GetAllUsers function</span></span>
- <span data-ttu-id="6f55a-289">GetNumberOfUsersOnline 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-289">GetNumberOfUsersOnline function</span></span>
- <span data-ttu-id="6f55a-290">GetPassword 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-290">GetPassword function</span></span>
- <span data-ttu-id="6f55a-291">GetUser 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-291">GetUser function</span></span>
- <span data-ttu-id="6f55a-292">GetUserNameByEmail 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-292">GetUserNameByEmail function</span></span>
- <span data-ttu-id="6f55a-293">MaxInvalidPasswordAttempts プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-293">MaxInvalidPasswordAttempts property</span></span>
- <span data-ttu-id="6f55a-294">MinRequiredNonAlphanumericCharacters プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-294">MinRequiredNonAlphanumericCharacters property</span></span>
- <span data-ttu-id="6f55a-295">MinRequiredPasswordLength プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-295">MinRequiredPasswordLength property</span></span>
- <span data-ttu-id="6f55a-296">PasswordAttemptWindow プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-296">PasswordAttemptWindow property</span></span>
- <span data-ttu-id="6f55a-297">PasswordFormat プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-297">PasswordFormat property</span></span>
- <span data-ttu-id="6f55a-298">PasswordStrengthRegularExpression プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-298">PasswordStrengthRegularExpression property</span></span>
- <span data-ttu-id="6f55a-299">RequiresQuestionAndAnswer プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-299">RequiresQuestionAndAnswer property</span></span>
- <span data-ttu-id="6f55a-300">RequiresUniqueEmail プロパティ</span><span class="sxs-lookup"><span data-stu-id="6f55a-300">RequiresUniqueEmail property</span></span>
- <span data-ttu-id="6f55a-301">ResetPassword 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-301">ResetPassword function</span></span>
- <span data-ttu-id="6f55a-302">ユーザー関数のロックを解除します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-302">Unlock user function</span></span>
- <span data-ttu-id="6f55a-303">UpdateUser 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-303">UpdateUser function</span></span>
- <span data-ttu-id="6f55a-304">ValidateUser 関数</span><span class="sxs-lookup"><span data-stu-id="6f55a-304">ValidateUser function</span></span>

<span data-ttu-id="6f55a-305">これを c# 開発者として実装する非常にリストします。</span><span class="sxs-lookup"><span data-stu-id="6f55a-305">Thats quite a list to implement as a C# developer.</span></span> <span data-ttu-id="6f55a-306">簡単に実装は一切 VB.NET でクラスを作成して、コードを c# に変換する .NET Reflector などのツールを使用することもあります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-306">You may find it easier to create the class in VB.NET without any implementation and then use .NET Reflector or a similar tool to convert the code to C#.</span></span>

<span data-ttu-id="6f55a-307">接続文字列とその他のプロパティを Initialize メソッドの既定値に設定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-307">The connection string and other properties should be set to their defaults in the Initialize method.</span></span> <span data-ttu-id="6f55a-308">(Initialize メソッドは、プロバイダーが実行時に読み込まれたときに発生した)。Initialize メソッドの 2 番目のパラメーターは、型 System.Collections.Specialized.NameValueCollection がありへの参照、&lt;追加&gt;web.config ファイルで、カスタム プロバイダーに関連付けられている要素。</span><span class="sxs-lookup"><span data-stu-id="6f55a-308">(The Initialize method is fired when the provider is loaded at runtime.) The second parameter to the Initialize method is of type System.Collections.Specialized.NameValueCollection and is a reference to the &lt;add&gt; element that is associated with your custom provider in the web.config file.</span></span> <span data-ttu-id="6f55a-309">そのエントリは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-309">That entry looks like the following:</span></span>

[!code-xml[Main](membership/samples/sample6.xml)]

<span data-ttu-id="6f55a-310">Initialize メソッドの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-310">Here is an example of the Initialize method.</span></span>

[!code-csharp[Main](membership/samples/sample7.cs)]

<span data-ttu-id="6f55a-311">ログイン フォームを提出するとき、ユーザーを検証するためには、ValidateUser メソッドを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="6f55a-311">In order to validate the user when they submit your login form, you will need to use the ValidateUser method.</span></span> <span data-ttu-id="6f55a-312">このメソッドは、ログイン コントロールでのログイン ボタンをクリックすると発生します。</span><span class="sxs-lookup"><span data-stu-id="6f55a-312">This method fires when the user clicks the login button in the Login control.</span></span> <span data-ttu-id="6f55a-313">このメソッドでユーザーの検索を行うコードが配置されます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-313">You will place your code that does the user lookup in this method.</span></span>

<span data-ttu-id="6f55a-314">ご覧のように、独自のメンバーシップ プロバイダーの作成は難しくなく、ASP.NET 2.0 のこの強力な機能を拡張することができます。</span><span class="sxs-lookup"><span data-stu-id="6f55a-314">As you can see, writing your own membership provider is not difficult and allows you to extend this powerful functionality of ASP.NET 2.0.</span></span>