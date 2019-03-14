---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
title: ユーザーとロール、運用環境の web サイト (c#) |Microsoft Docs
author: rick-anderson
description: ASP.NET web サイト管理ツール (WSAT) は、メンバーシップとロールの設定を構成して、作成するために web ベースのユーザー インターフェイスを提供、編集、.
ms.author: riande
ms.date: 06/09/2009
ms.assetid: dbc54313-5d05-4285-98b3-726edea6d0c9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs
msc.type: authoredcontent
ms.openlocfilehash: f08afe5f4ab379d1532f50267299892829c95dcc
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57048849"
---
<a name="users-and-roles-on-the-production-website-c"></a><span data-ttu-id="9b975-103">ユーザーとロール、運用環境の web サイト (c#)</span><span class="sxs-lookup"><span data-stu-id="9b975-103">Users and Roles On The Production Website (C#)</span></span>
====================
<span data-ttu-id="9b975-104">によって[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="9b975-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

[<span data-ttu-id="9b975-105">PDF のダウンロード</span><span class="sxs-lookup"><span data-stu-id="9b975-105">Download PDF</span></span>](http://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_cs.pdf)

> <span data-ttu-id="9b975-106">ASP.NET web サイト管理ツール (WSAT) は、メンバーシップとロールの設定を構成して作成、編集、およびユーザーとロールを削除するための web ベースのユーザー インターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="9b975-106">The ASP.NET Website Administration Tool (WSAT) provides a web-based user interface for configuring Membership and Roles settings and for creating, editing, and deleting users and roles.</span></span> <span data-ttu-id="9b975-107">残念ながら、WSAT のみ機能、localhost からアクセスすると、ブラウザーから、実稼働 web サイトの管理ツールにアクセスできないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="9b975-107">Unfortunately, the WSAT only works when visited from localhost, meaning that you cannot reach the production website's Administration Tool through your browser.</span></span> <span data-ttu-id="9b975-108">良い知らせは、ユーザーと運用上の役割を管理できるようにするための回避策があることです。</span><span class="sxs-lookup"><span data-stu-id="9b975-108">The good news is that there are workarounds that make it possible to manage users and roles on production.</span></span> <span data-ttu-id="9b975-109">このチュートリアルでは、これらの回避策や他のユーザーで検索します。</span><span class="sxs-lookup"><span data-stu-id="9b975-109">This tutorial looks at these workarounds and others.</span></span>


## <a name="introduction"></a><span data-ttu-id="9b975-110">はじめに</span><span class="sxs-lookup"><span data-stu-id="9b975-110">Introduction</span></span>

<span data-ttu-id="9b975-111">ASP.NET 2.0 の多くを導入する*アプリケーション サービス*、これは、一連の構成要素サービス、web アプリケーションに追加することができます。</span><span class="sxs-lookup"><span data-stu-id="9b975-111">ASP.NET 2.0 introduced a number of *application services*, which are a suite of building block services that you can add to your web application.</span></span> <span data-ttu-id="9b975-112">書籍レビューの web サイトにメンバーシップとロール サービスのバックアップを追加しました、 [*サービスを構成する、web サイトを使用してアプリケーション*チュートリアル](configuring-a-website-that-uses-application-services-cs.md)します。</span><span class="sxs-lookup"><span data-stu-id="9b975-112">We added the Membership and Roles services to the Book Reviews website back in the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-cs.md).</span></span> <span data-ttu-id="9b975-113">メンバーシップ サービス作成および管理するユーザー アカウントを使用します。ロール サービスは、ユーザーをグループに分類するための API を提供します。</span><span class="sxs-lookup"><span data-stu-id="9b975-113">The Membership service facilitates creating and managing user accounts; the Roles service offers an API for categorizing users into groups.</span></span> <span data-ttu-id="9b975-114">ブック_レビュー サイトには、3 つのユーザー アカウント、および Scott、Jisun、および Alice - 管理者は、Scott と Jisun 管理者の役割で、1 つの役割があります。</span><span class="sxs-lookup"><span data-stu-id="9b975-114">The Book Reviews site has three user accounts - Scott, Jisun, and Alice - and a single role, Admin, with Scott and Jisun in the Admin role.</span></span>

<span data-ttu-id="9b975-115">ASP します。NET のアプリケーション サービスは特定の実装に関連付けられていません。</span><span class="sxs-lookup"><span data-stu-id="9b975-115">ASP.NET's application services are not tied to a specific implementation.</span></span> <span data-ttu-id="9b975-116">使用して、特定のアプリケーション サービスに指示する代わりに、*プロバイダー*、し、そのプロバイダーが特定のテクノロジを使用してサービスを実装します。</span><span class="sxs-lookup"><span data-stu-id="9b975-116">Instead, you instruct the application services to use a particular *provider*, and that provider implements the service using a particular technology.</span></span> <span data-ttu-id="9b975-117">使用する、書籍レビューの web アプリケーションを構成した、`SqlMembershipProvider`と`SqlRoleProvider`メンバーシップとロール サービスのプロバイダー。</span><span class="sxs-lookup"><span data-stu-id="9b975-117">We configured the Book Reviews web application to use the `SqlMembershipProvider` and `SqlRoleProvider` providers for the Membership and Roles services.</span></span> <span data-ttu-id="9b975-118">これら 2 つのプロバイダーは、SQL Server データベースにユーザー アカウントとロールの情報を格納、web ホスト会社でホストされているインターネット ベースの web アプリケーションの最もよく使用されるプロバイダーです。</span><span class="sxs-lookup"><span data-stu-id="9b975-118">These two providers store user account and role information in a SQL Server database and are the most commonly used providers for Internet-based web applications hosted at a web hosting company.</span></span>

<span data-ttu-id="9b975-119">メンバーシップとロール サービスを使用する開発者向けの一般的な課題は、ユーザーおよびロール、運用環境の管理です。</span><span class="sxs-lookup"><span data-stu-id="9b975-119">A common challenge for developers using the Membership and Roles services is managing the users and roles on the production environment.</span></span> <span data-ttu-id="9b975-120">実稼働 web サイトからユーザー アカウントを削除、新しいロールを追加または既存のロールに、既存のユーザーを追加する方法</span><span class="sxs-lookup"><span data-stu-id="9b975-120">How do you delete a user account from the production website, add a new role, or add an existing user to an existing role?</span></span> <span data-ttu-id="9b975-121">このチュートリアルでは、ユーザーと実稼働 web サイト ロールを管理するためのさまざまな手法について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b975-121">This tutorial explores different techniques for managing users and roles on the production website.</span></span>

## <a name="using-the-aspnet-web-site-administration-tool"></a><span data-ttu-id="9b975-122">ASP.NET Web サイトの管理ツールを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b975-122">Using the ASP.NET Web Site Administration Tool</span></span>

<span data-ttu-id="9b975-123">ASP.NET には、 [Web サイト管理ツール](https://msdn.microsoft.com/library/yy40ytx0.aspx)(WSAT) を簡単に作成してユーザー アカウントとロールを管理し、ユーザーとロール ベースの承認規則を指定します。</span><span class="sxs-lookup"><span data-stu-id="9b975-123">ASP.NET includes a [Web Site Administration Tool](https://msdn.microsoft.com/library/yy40ytx0.aspx) (WSAT) that makes it easy to create and manage user accounts and roles and to specify user- and role-based authorization rules.</span></span> <span data-ttu-id="9b975-124">WSAT を使用するには、ソリューション エクスプ ローラーで ASP.NET の構成アイコンをクリックしてまたは web サイトまたはプロジェクト メニューに移動し、ASP.NET 構成オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="9b975-124">To use the WSAT, click the ASP.NET Configuration icon in the Solution Explorer, or go to the Website or Project menu and choose the ASP.NET Configuration option.</span></span> <span data-ttu-id="9b975-125">どちらの方法では、web ブラウザーを起動し、ようなアドレスで WSAT を指します。 `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`</span><span class="sxs-lookup"><span data-stu-id="9b975-125">Either approach launches a web browser and points it to the WSAT at an address like: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`</span></span>

<span data-ttu-id="9b975-126">WSAT は、3 つのセクションに分かれています。</span><span class="sxs-lookup"><span data-stu-id="9b975-126">The WSAT is divided into three sections:</span></span>

- <span data-ttu-id="9b975-127">**セキュリティ**-ユーザー、ロール、および承認規則を管理します。</span><span class="sxs-lookup"><span data-stu-id="9b975-127">**Security** - manage users, roles, and authorization rules.</span></span>
- <span data-ttu-id="9b975-128">**「アプリケーション構成」** -管理、 &lt;appSettings&gt;とここでは、SMTP 設定します。</span><span class="sxs-lookup"><span data-stu-id="9b975-128">**ApplicationConfiguration** - manage the &lt;appSettings&gt; and SMTP settings from here.</span></span> <span data-ttu-id="9b975-129">ことができますも、アプリケーションをオフラインにしてデバッグ出力およびトレースここでは、設定の管理だけでなく既定のカスタム エラー ページを指定します。</span><span class="sxs-lookup"><span data-stu-id="9b975-129">You can also take the application offline and manage debugging and tracing settings from here, as well as specify the default custom error page.</span></span>
- <span data-ttu-id="9b975-130">**ProviderConfiguration** -アプリケーションのサービスによって使用されるプロバイダを構成します。</span><span class="sxs-lookup"><span data-stu-id="9b975-130">**ProviderConfiguration** - configure the providers used by the application services.</span></span>

<span data-ttu-id="9b975-131">[セキュリティ] セクション (に示すように**図 1**) へのリンクには新しいユーザーを作成する、ユーザーの管理、作成やの役割の管理し作成と管理のアクセス規則が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b975-131">The Security section (shown in **Figure 1**) includes links for creating new users, managing users, creating and managing roles, and creating and managing access rules.</span></span> <span data-ttu-id="9b975-132">ここからするシステムに新しいロールを追加、既存のユーザーを削除または追加したり、特定のユーザー アカウントからロールを削除できます。</span><span class="sxs-lookup"><span data-stu-id="9b975-132">From here you can add a new role to the system, delete an existing user, or add or remove roles from a particular user account.</span></span>

[![](users-and-roles-on-the-production-website-cs/_static/image2.png)](users-and-roles-on-the-production-website-cs/_static/image1.png)

<span data-ttu-id="9b975-133">**図 1**:WSAT セキュリティ セクションには、管理ユーザーおよびロールのオプションが含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b975-133">**Figure 1**: The WSAT Security Section Includes Options for Managing Users and Roles</span></span>  
<span data-ttu-id="9b975-134">([フルサイズの画像を表示する をクリックします](users-and-roles-on-the-production-website-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="9b975-134">([Click to view full-size image](users-and-roles-on-the-production-website-cs/_static/image3.png))</span></span>

<span data-ttu-id="9b975-135">残念ながら、WSAT はのみアクセスできるローカルです。</span><span class="sxs-lookup"><span data-stu-id="9b975-135">Unfortunately, the WSAT is only accessible locally.</span></span> <span data-ttu-id="9b975-136">リモート運用 web サイトで、WSAT をアクセスすることはできませんアクセスした場合`www.yoursite.com/asp.netwebadminfiles/default.aspx`404 Not Found 応答を取得します。</span><span class="sxs-lookup"><span data-stu-id="9b975-136">You cannot visit the WSAT on your remote production website; if you visit `www.yoursite.com/asp.netwebadminfiles/default.aspx` you get a 404 Not Found response.</span></span> <span data-ttu-id="9b975-137">WSAT を実行するコードを`Membership`と`Roles`を作成する .NET Framework のクラスは、編集、およびユーザーとロールを削除します。</span><span class="sxs-lookup"><span data-stu-id="9b975-137">The code that powers the WSAT uses the `Membership` and `Roles` classes in the .NET Framework to create, edit, and delete users and roles.</span></span> <span data-ttu-id="9b975-138">これらのクラスは、使用するには、どのようなプロバイダーを決定する web アプリケーションの構成情報を参照してください。戻り、 [*サービスを構成する、web サイトを使用してアプリケーション*チュートリアル](configuring-a-website-that-uses-application-services-cs.md)、書籍レビューの web サイトを使用する設定、`SqlMembershipProvider`と`SqlRoleProvider`プロバイダー。</span><span class="sxs-lookup"><span data-stu-id="9b975-138">These classes consult the web application's configuration information to determine what provider to use; back in the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-cs.md) we setup the Book Reviews website to use the `SqlMembershipProvider` and `SqlRoleProvider` providers.</span></span> <span data-ttu-id="9b975-139">これに含まれる追加`<membership>`と`<roleManager>`にセクション`Web.config`します。</span><span class="sxs-lookup"><span data-stu-id="9b975-139">This entailed adding `<membership>` and `<roleManager>` sections to `Web.config`.</span></span>

[!code-xml[Main](users-and-roles-on-the-production-website-cs/samples/sample1.xml)]

<span data-ttu-id="9b975-140">なお、`<membership>`と`<roleManager>`セクションを参照、`SqlMembershipProvider`と`SqlRoleProvider`でプロバイダー、`type`属性は、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="9b975-140">Note that the `<membership>` and `<roleManager>` sections reference the `SqlMembershipProvider` and `SqlRoleProvider` providers in their `type` attribute, respectively.</span></span> <span data-ttu-id="9b975-141">これらのプロバイダーは、指定した SQL Server データベースのユーザーとロール情報を格納します。</span><span class="sxs-lookup"><span data-stu-id="9b975-141">These providers store the user and role information in a specified SQL Server database.</span></span> <span data-ttu-id="9b975-142">これらのプロバイダーによって使用されるデータベースがで指定された、`connectionStringName`属性、 `ReviewsConnectionString`、定義されている、`~/ConfigSections/databaseConnectionStrings.config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="9b975-142">The database used by these providers is specified by the `connectionStringName` attribute, `ReviewsConnectionString`, which is defined in the `~/ConfigSections/databaseConnectionStrings.config` file.</span></span> <span data-ttu-id="9b975-143">いることを思い出してください、`databaseConnectionStrings.config`一方、開発環境でのファイルが開発用データベースへの接続文字列を含む、`databaseConnectionStrings.config`運用上のファイルには、実稼働データベースへの接続文字列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b975-143">Recall that the `databaseConnectionStrings.config` file in the development environment contains the connection string to the development database whereas the `databaseConnectionStrings.config` file on production contains the connection string to the production database.</span></span>

<span data-ttu-id="9b975-144">簡単に言うと、開発環境を介して、WSAT をローカルにアクセスする必要がありで指定されたデータベースでユーザーおよびロールについては、連携、`databaseConnectionStrings.config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="9b975-144">In a nutshell, the WSAT must be accessed locally through the development environment, and it works with the user and role information in the database specified in the `databaseConnectionStrings.config` file.</span></span> <span data-ttu-id="9b975-145">その結果、内の接続文字列情報を変更する場合、`databaseConnectionStrings.config`ファイル開発環境で使用できます、WSAT ローカル ユーザーと運用環境でロールを管理します。</span><span class="sxs-lookup"><span data-stu-id="9b975-145">Consequently, if we change the connection string information in the `databaseConnectionStrings.config` file on the development environment we can use the WSAT locally to manage users and roles in the production environment.</span></span>

<span data-ttu-id="9b975-146">この機能を示すためには、開く、`databaseConnectionStrings.config`開発環境で Visual Studio でファイルし、開発データベースの接続文字列を実稼働データベースの接続文字列に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="9b975-146">To illustrate this functionality, open the `databaseConnectionStrings.config` file in Visual Studio on the development environment and replace the development database connection string with the production database connection string.</span></span> <span data-ttu-id="9b975-147">WSAT を起動し、[セキュリティ] タブを移動し、でパスワードが"password!"Sam をという名前の新しいユーザーを追加</span><span class="sxs-lookup"><span data-stu-id="9b975-147">Then launch the WSAT, go the Security tab, and add a new user named Sam with password "password!"</span></span> <span data-ttu-id="9b975-148">(以下、引用符)。</span><span class="sxs-lookup"><span data-stu-id="9b975-148">(less the quotation marks).</span></span> <span data-ttu-id="9b975-149">**図 2**このアカウントを作成するときに、WSAT 画面を示しています。</span><span class="sxs-lookup"><span data-stu-id="9b975-149">**Figure 2** shows the WSAT screen when creating this account.</span></span>

[![](users-and-roles-on-the-production-website-cs/_static/image5.png)](users-and-roles-on-the-production-website-cs/_static/image4.png)

<span data-ttu-id="9b975-150">**図 2**:運用環境での Sam をという名前の新しいユーザーを作成します。</span><span class="sxs-lookup"><span data-stu-id="9b975-150">**Figure 2**: Create a New User Named Sam In the Production Environment</span></span>  
<span data-ttu-id="9b975-151">([フルサイズの画像を表示する をクリックします](users-and-roles-on-the-production-website-cs/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="9b975-151">([Click to view full-size image](users-and-roles-on-the-production-website-cs/_static/image6.png))</span></span>

<span data-ttu-id="9b975-152">内の接続文字列を変更しましたので`databaseConnectionStrings.config`を実稼働データベース サーバーを指す、Sam が運用環境でのユーザーとして追加されました。</span><span class="sxs-lookup"><span data-stu-id="9b975-152">Because we changed the connection string in `databaseConnectionStrings.config` to point to the production database server, Sam was added as a user in the production environment.</span></span> <span data-ttu-id="9b975-153">これを確認するには、接続文字列を変更、`databaseConnectionStrings.config`ファイル開発用データベースをバックアップし、アクセス、`Login.aspx`開発環境でのページ。</span><span class="sxs-lookup"><span data-stu-id="9b975-153">To verify this, change the connection string in the `databaseConnectionStrings.config` file back to the development database and then visit the `Login.aspx` page in the development environment.</span></span> <span data-ttu-id="9b975-154">Sam でサインインしようとしています (を参照してください**図 3**)。</span><span class="sxs-lookup"><span data-stu-id="9b975-154">Try to sign in as Sam (see **Figure 3**).</span></span>

[![](users-and-roles-on-the-production-website-cs/_static/image8.png)](users-and-roles-on-the-production-website-cs/_static/image7.png)

<span data-ttu-id="9b975-155">**図 3**:開発環境での Sam としてサインインすることはできません。</span><span class="sxs-lookup"><span data-stu-id="9b975-155">**Figure 3**: You Cannot Sign In As Sam in the Development Environment</span></span>  
<span data-ttu-id="9b975-156">([フルサイズの画像を表示する をクリックします](users-and-roles-on-the-production-website-cs/_static/image9.png))。</span><span class="sxs-lookup"><span data-stu-id="9b975-156">([Click to view full-size image](users-and-roles-on-the-production-website-cs/_static/image9.png))</span></span>

<span data-ttu-id="9b975-157">できませんサインインする Sam として開発環境でのユーザー アカウント情報がローカル データベースに存在しないためです。</span><span class="sxs-lookup"><span data-stu-id="9b975-157">You cannot sign in as Sam in the development environment because the user account information does not exist in the local database.</span></span> <span data-ttu-id="9b975-158">代わりは、実稼働データベースに追加されました。</span><span class="sxs-lookup"><span data-stu-id="9b975-158">Rather, is was added to the production database.</span></span> <span data-ttu-id="9b975-159">これを確認するには、内容を表示、`aspnet_Users`開発と運用環境の両方のデータベース内のテーブル。</span><span class="sxs-lookup"><span data-stu-id="9b975-159">To verify this, view the contents of the `aspnet_Users` table in both the development and production databases.</span></span> <span data-ttu-id="9b975-160">開発環境では、Scott、Jisun、Alice のユーザーのみに 3 つのレコードが必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b975-160">In the development environment there should be only three records for users Scott, Jisun, and Alice.</span></span> <span data-ttu-id="9b975-161">ただし、`aspnet_Users`実稼働データベース内のテーブルが 4 つのレコード。Scott、Jisun、Alice、および Sam です。</span><span class="sxs-lookup"><span data-stu-id="9b975-161">However, the `aspnet_Users` table in the production database has four records: Scott, Jisun, Alice, and Sam.</span></span> <span data-ttu-id="9b975-162">その結果、Sam は、運用環境で web サイトを経由する、開発環境ではなくにサインインできます。</span><span class="sxs-lookup"><span data-stu-id="9b975-162">Consequently, Sam can sign in through the website in production, but not through the development environment.</span></span>

[![](users-and-roles-on-the-production-website-cs/_static/image11.png)](users-and-roles-on-the-production-website-cs/_static/image10.png)

<span data-ttu-id="9b975-163">**図 4**:Sam は、実稼働 web サイトにサインインできます。</span><span class="sxs-lookup"><span data-stu-id="9b975-163">**Figure 4**: Sam Can Sign In On the Production Website</span></span>  
<span data-ttu-id="9b975-164">([フルサイズの画像を表示する をクリックします](users-and-roles-on-the-production-website-cs/_static/image12.png))。</span><span class="sxs-lookup"><span data-stu-id="9b975-164">([Click to view full-size image](users-and-roles-on-the-production-website-cs/_static/image12.png))</span></span>

> [!NOTE]
> <span data-ttu-id="9b975-165">接続文字列を変更することを忘れないでください、`databaseConnectionStrings.config`完了すると、開発用データベースにファイルから文字列 's 接続、開発を使用してサイトをテストするときに運用データで作業する WSAT それ以外の場合の操作環境。</span><span class="sxs-lookup"><span data-stu-id="9b975-165">Don't forget to change the connection string in the `databaseConnectionStrings.config` file back to the development database's connect string when you're done working with the WSAT otherwise you will be working with production data when testing the site through the development environment.</span></span> <span data-ttu-id="9b975-166">ここで説明した技法により、WSAT を使用して、リモート ユーザーおよびロールを管理する、中に、その他の WSAT 構成オプション (アクセス規則、SMTP 設定、トレースおよびデバッグ設定、およびなど) のいずれかの変更が、を変更ことに留意してください。`Web.config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="9b975-166">Also keep in mind that while the technique we just discussed allows us to use the WSAT to remotely manage users and roles, changes to any of the other WSAT configuration options (access rules, SMTP settings, debugging and tracing settings, and so on) modify the `Web.config` file.</span></span> <span data-ttu-id="9b975-167">その結果、開発環境と運用環境にない設定に加えられた変更が適用されます。</span><span class="sxs-lookup"><span data-stu-id="9b975-167">Consequently, any changes made to the settings apply to the development environment and not to the production environment.</span></span>


## <a name="creating-custom-user-and-role-management-web-pages"></a><span data-ttu-id="9b975-168">カスタム ユーザーおよびロール管理 Web ページの作成</span><span class="sxs-lookup"><span data-stu-id="9b975-168">Creating Custom User and Role Management Web Pages</span></span>

<span data-ttu-id="9b975-169">WSAT は、ユーザーとロールを管理するためのボックス システムの不足を提供しますが、ローカルでのみ起動でき、ユーザーと運用環境でロールを管理するために、接続文字列情報に変更を加える必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b975-169">The WSAT provides an out of the box system for managing users and roles, but can only be launched locally and requires making changes to the connection string information in order to manage the users and roles on production.</span></span> <span data-ttu-id="9b975-170">ユーザー アカウントをサポートするほとんどの web サイトには、さまざまなユーザーと管理者は、サイト内のページからユーザーとロールの管理を有効にするロールの管理 web ページも含まれます。</span><span class="sxs-lookup"><span data-stu-id="9b975-170">Most websites that support user accounts also include a number of user and role administration web pages that enable administrators to manage users and roles from pages within the site.</span></span> <span data-ttu-id="9b975-171">このような web ベースの管理ページがそれがより簡単にユーザーとロールの管理し、サイトに不可欠ですが、多くの管理者または管理者へのアクセスや、WSAT を起動する Visual Studio を使用する技術的な背景を持たない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="9b975-171">Such web-based administration pages make it much easier to manage users and roles and are essential for sites where there may be many administrators or administrators that do not have access to or the technical background to use Visual Studio to launch the WSAT.</span></span>

<span data-ttu-id="9b975-172">ASP.NET には、組み込みのログインに関連する Web コントロールにドラッグ アンド ドロップするだけこれらの管理 web ページの多くを実装するための数値が含まれています。</span><span class="sxs-lookup"><span data-stu-id="9b975-172">ASP.NET includes a number of built-in Login-related Web controls that make implementing many of these administrative web pages as easy as drag and drop.</span></span> <span data-ttu-id="9b975-173">たとえば、ページ上に CreateUserWizard コントロールをドラッグし、いくつかのプロパティを設定して新しいユーザー アカウントを作成する管理者用のページを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9b975-173">For example, you can create a page for administrators to create a new user account by dragging the CreateUserWizard control onto the page and setting a few properties.</span></span> <span data-ttu-id="9b975-174">実際、示した WSAT でユーザーを作成するためのページ**図 2**をページに追加できる同じ CreateUserWizard コントロールを使用します。</span><span class="sxs-lookup"><span data-stu-id="9b975-174">In fact, the page for creating users in the WSAT shown in **Figure 2** uses the same CreateUserWizard control that you can add to your pages.</span></span> <span data-ttu-id="9b975-175">さらに、メンバーシップとロール サービスの機能を利用プログラムで、`Membership`と`Roles`.NET Framework のクラス。</span><span class="sxs-lookup"><span data-stu-id="9b975-175">Furthermore, the Membership and Roles services' functionalities are available programmatically through the `Membership` and `Roles` classes in the .NET Framework.</span></span> <span data-ttu-id="9b975-176">これらのクラスには、作成、編集、およびユーザーとロールをもユーザーのロールに追加または削除したり、ロールではユーザーを特定し、他のユーザーと役割に関連するタスクを実行するを削除するコードを記述できます。</span><span class="sxs-lookup"><span data-stu-id="9b975-176">With these classes you can write code to create, edit, and delete users and roles, as well as to add or remove users to roles, to determine what users are in what roles, and to perform other user- and role-related tasks.</span></span>

<span data-ttu-id="9b975-177">[*サービスを構成する、web サイトを使用してアプリケーション*チュートリアル](configuring-a-website-that-uses-application-services-cs.md)ページを追加、`Admin`という名前のフォルダー`CreateAccount.aspx`します。</span><span class="sxs-lookup"><span data-stu-id="9b975-177">In the [*Configuring a Website That Uses Application Services* tutorial](configuring-a-website-that-uses-application-services-cs.md) I added a page to the `Admin` folder named `CreateAccount.aspx`.</span></span> <span data-ttu-id="9b975-178">このページで、サイトに新しいユーザー アカウントを追加して、新しく作成したユーザーが管理者ロールがかどうかを指定する管理者は、(を参照してください**図 5**)。</span><span class="sxs-lookup"><span data-stu-id="9b975-178">This page allows an administrator to add a new user account to the site and to specify whether or not the newly created user is in the Admin role (see **Figure 5**).</span></span>

[![](users-and-roles-on-the-production-website-cs/_static/image14.png)](users-and-roles-on-the-production-website-cs/_static/image13.png)

<span data-ttu-id="9b975-179">**図 5**:管理者は、新しいユーザー アカウントを作成できます。</span><span class="sxs-lookup"><span data-stu-id="9b975-179">**Figure 5**: Administrators Can Create New User Accounts</span></span>  
<span data-ttu-id="9b975-180">([フルサイズの画像を表示する をクリックします](users-and-roles-on-the-production-website-cs/_static/image15.png))。</span><span class="sxs-lookup"><span data-stu-id="9b975-180">([Click to view full-size image](users-and-roles-on-the-production-website-cs/_static/image15.png))</span></span>

<span data-ttu-id="9b975-181">使用に関する詳細な手順と共に、ユーザーおよびロールの管理ページの構築について詳しく説明、`Membership`と`Roles`クラスと、ログインに関連する ASP.NET Web コントロールを必ずお読み、 [web サイトのセキュリティチュートリアル](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)します。</span><span class="sxs-lookup"><span data-stu-id="9b975-181">For a more detailed look at building user and role administration pages, along with step-by-step instructions on using the `Membership` and `Roles` classes and the Login-related ASP.NET Web controls, be sure to read my [Website Security Tutorials](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).</span></span> <span data-ttu-id="9b975-182">ユーザー ロール、およびその他の一般的な管理タスクを割り当てる新しいアカウントを作成し、作成、およびの役割の管理用の web ページを構築する方法のガイダンスを検索します。</span><span class="sxs-lookup"><span data-stu-id="9b975-182">There you'll find guidance on how to build web pages for creating new accounts, creating and managing roles, assigning users to roles, and other common administrative tasks.</span></span>

<span data-ttu-id="9b975-183">運用 web サイトに WSAT のような機能を実装するには、独自の一連の WSAT の機能を実装する web ページをいつでも構築できます。</span><span class="sxs-lookup"><span data-stu-id="9b975-183">To implement WSAT-like functionality on the production website you can always build your own series of web pages that implement the WSAT's features.</span></span> <span data-ttu-id="9b975-184">最初に、フォルダーにある WSAT ソース コードをチェック アウトする`%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`します。</span><span class="sxs-lookup"><span data-stu-id="9b975-184">To help get started, check out the WSAT source code, which is located in the folder `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`.</span></span> <span data-ttu-id="9b975-185">別のオプションは、彼は、彼の記事で共有、Dan Clem の WSAT 代替手段を使用する[ローリング、独自の Web サイト管理ツール](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="9b975-185">Another option is to use Dan Clem's WSAT alternative, which he shares in his article, [Rolling Your Own Web Site Administration Tool](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx).</span></span> <span data-ttu-id="9b975-186">Dan はまで、カスタム WSAT のようなツールを構築するプロセスについて説明します (c# で)、ダウンロード、アプリケーションのソース コードが含まれています、およびホストされる web サイトを自分のカスタム WSAT を追加するための手順について説明します。</span><span class="sxs-lookup"><span data-stu-id="9b975-186">Dan walks readers through the process of building a custom WSAT-like tool, includes his application's source code for download (in C#), and gives step-by-step instructions for adding his custom WSAT to a hosted website.</span></span>

## <a name="summary"></a><span data-ttu-id="9b975-187">まとめ</span><span class="sxs-lookup"><span data-stu-id="9b975-187">Summary</span></span>

<span data-ttu-id="9b975-188">ASP.NET Web サイト管理ツール (WSAT) は、web サイトのユーザーおよびロールの情報を管理するメンバーシップとロールのアプリケーション サービスと連携して使用できます。</span><span class="sxs-lookup"><span data-stu-id="9b975-188">The ASP.NET Web Site Administration Tool (WSAT) can be used in tandem with the Membership and Roles application services to manage user and role information for your website.</span></span> <span data-ttu-id="9b975-189">残念ながら、WSAT のみがローカルでアクセスできると、実稼働 web サイトからアクセスされることはできません。</span><span class="sxs-lookup"><span data-stu-id="9b975-189">Unfortunately, the WSAT is only accessible locally and cannot be visited from your production website.</span></span> <span data-ttu-id="9b975-190">ただし、開発の接続文字列を変更することで、実稼働データベースをポイントするための環境を使用できます、WSAT ユーザーと、実稼働 web サイト ロールの管理します。</span><span class="sxs-lookup"><span data-stu-id="9b975-190">However, by changing the connection string in the development environment to point to the production database you can use the WSAT to manage the users and roles on the production website.</span></span>

<span data-ttu-id="9b975-191">WSAT アプローチは、ユーザーとロールを管理する迅速かつ簡単な方法により、中に、接続文字列情報を一時的な変更と同様に Visual Studio から WSAT を起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9b975-191">While the WSAT approach affords a quick and easy way to manage users and roles, it necessitates launching the WSAT from Visual Studio as well as temporary changes to the connection string information.</span></span> <span data-ttu-id="9b975-192">WSAT はユーザーと、運用環境でロールを管理する簡単な方法を提供しています、面倒ですが、複数の管理者または管理者がないか、Visual Studio と、WSAT に慣れていないユーザーともの web サイトは機能しません。</span><span class="sxs-lookup"><span data-stu-id="9b975-192">The WSAT offers a quick way to manage users and roles on production, but is cumbersome and does not work well for websites with multiple administrators or with administrators who do not have or are not familiar with Visual Studio and the WSAT.</span></span> <span data-ttu-id="9b975-193">これらの理由から、ユーザー アカウントをサポートするほとんどの web サイトには、管理用の web ページのセットが含まれます。</span><span class="sxs-lookup"><span data-stu-id="9b975-193">For these reasons, most websites that support user accounts include a set of administrative web pages.</span></span> <span data-ttu-id="9b975-194">このような一連の web ページは、WSAT が不要し、任意のコンピューターからのさまざまな管理ユーザーによって使用されます。</span><span class="sxs-lookup"><span data-stu-id="9b975-194">Such a set of web pages eliminates the need for the WSAT and used by various administrative users from any computer.</span></span>

<span data-ttu-id="9b975-195">満足のプログラミングです。</span><span class="sxs-lookup"><span data-stu-id="9b975-195">Happy Programming!</span></span>

### <a name="further-reading"></a><span data-ttu-id="9b975-196">関連項目</span><span class="sxs-lookup"><span data-stu-id="9b975-196">Further Reading</span></span>

<span data-ttu-id="9b975-197">このチュートリアルで説明したトピックの詳細については、次の情報を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9b975-197">For more information on the topics discussed in this tutorial, refer to the following resources:</span></span>

- [<span data-ttu-id="9b975-198">ASP を調べています。NET のメンバーシップ、ロール、およびプロファイル</span><span class="sxs-lookup"><span data-stu-id="9b975-198">Examining ASP.NET's Membership, Roles, and Profile</span></span>](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [<span data-ttu-id="9b975-199">独自の Web サイト管理ツールのローリング</span><span class="sxs-lookup"><span data-stu-id="9b975-199">Rolling Your Own Web Site Administration Tool</span></span>](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [<span data-ttu-id="9b975-200">Web サイト管理ツールの概要</span><span class="sxs-lookup"><span data-stu-id="9b975-200">Web Site Administration Tool Overview</span></span>](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [<span data-ttu-id="9b975-201">Web サイトのセキュリティのチュートリアル</span><span class="sxs-lookup"><span data-stu-id="9b975-201">Website Security Tutorials</span></span>](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> <span data-ttu-id="9b975-202">[前へ](precompiling-your-website-cs.md)
> [次へ](asp-net-hosting-options-vb.md)</span><span class="sxs-lookup"><span data-stu-id="9b975-202">[Previous](precompiling-your-website-cs.md)
[Next](asp-net-hosting-options-vb.md)</span></span>