---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
title: 映画データベース アプリケーションを 15 分間に ASP.NET MVC を作成 (c#) |Microsoft Docs
author: StephenWalther
description: Stephen Walther データベース駆動 ASP.NET MVC アプリケーション全体の開始から完了するを構築します。 このチュートリアルでは、新しい t している人たちの導入として優れています.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: dd1be137-91c5-47a8-8137-fecf0789c7f5
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
msc.type: authoredcontent
ms.openlocfilehash: 16d62102713b0b86aa93284e39c82d3ae492f892
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051879"
---
<a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-c"></a><span data-ttu-id="4696f-104">ASP.NET MVC を使用し、映画データベース アプリケーションを 15 分で作成する (C#)</span><span class="sxs-lookup"><span data-stu-id="4696f-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (C#)</span></span>
====================
<span data-ttu-id="4696f-105">によって[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="4696f-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="4696f-106">コードをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="4696f-106">Download Code</span></span>](http://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_CS.zip)

> <span data-ttu-id="4696f-107">Stephen Walther データベース駆動 ASP.NET MVC アプリケーション全体の開始から完了するを構築します。</span><span class="sxs-lookup"><span data-stu-id="4696f-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="4696f-108">このチュートリアルは、ASP.NET MVC アプリケーションを構築するためのプロセスを把握したいは、ASP.NET MVC フレームワークに初めて、およびユーザーの導入として優れています。</span><span class="sxs-lookup"><span data-stu-id="4696f-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>


<span data-ttu-id="4696f-109">このチュートリアルの目的は、「は、」の感覚をつかむことに、ASP.NET MVC アプリケーションを構築します。</span><span class="sxs-lookup"><span data-stu-id="4696f-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="4696f-110">このチュートリアルでは爆発開始から終了する全体 ASP.NET MVC アプリケーションを構築します。</span><span class="sxs-lookup"><span data-stu-id="4696f-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="4696f-111">私は、どのようにすることができますを一覧表示、作成、およびデータベース レコードを編集を示す単純なデータベース駆動型アプリケーションを構築する方法を示します。</span><span class="sxs-lookup"><span data-stu-id="4696f-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="4696f-112">アプリケーションを構築するプロセスを簡略化するのには、Visual Studio 2008 のスキャフォールディング機能の利点をみましょう。</span><span class="sxs-lookup"><span data-stu-id="4696f-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="4696f-113">最初のコードと、コント ローラー、モデル、およびビューのコンテンツを生成する Visual Studio をお知らせします。</span><span class="sxs-lookup"><span data-stu-id="4696f-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="4696f-114">Active Server Pages または ASP.NET を使用する場合、しする必要があります ASP.NET MVC とてもなじみやすいものです。</span><span class="sxs-lookup"><span data-stu-id="4696f-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="4696f-115">ASP.NET MVC ビューは、Active Server Pages アプリケーションのページとよく似ています。</span><span class="sxs-lookup"><span data-stu-id="4696f-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="4696f-116">また、従来の ASP.NET Web フォーム アプリケーションと同じように ASP.NET MVC を使うと、言語と .NET framework によって提供されるクラスの豊富なセットへのフル アクセス。</span><span class="sxs-lookup"><span data-stu-id="4696f-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="4696f-117">思いますが、このチュートリアルを把握するのと同様と異なる場合、Active Server Pages または ASP.NET Web フォーム アプリケーションの開発エクスペリエンスの両方の ASP.NET MVC アプリケーションを構築するためのエクスペリエンスです。</span><span class="sxs-lookup"><span data-stu-id="4696f-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="4696f-118">映画データベース アプリケーションの概要</span><span class="sxs-lookup"><span data-stu-id="4696f-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="4696f-119">私たちの目標では、簡潔であるために、非常に単純な映画データベース アプリケーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="4696f-120">簡単なムービー データベース アプリケーションでは次の 3 つの作業を行うことを許可します。</span><span class="sxs-lookup"><span data-stu-id="4696f-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="4696f-121">ムービー データベース レコードのセットを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="4696f-121">List a set of movie database records</span></span>
2. <span data-ttu-id="4696f-122">新しいムービー データベース レコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-122">Create a new movie database record</span></span>
3. <span data-ttu-id="4696f-123">既存のムービー データベース レコードを編集します。</span><span class="sxs-lookup"><span data-stu-id="4696f-123">Edit an existing movie database record</span></span>

<span data-ttu-id="4696f-124">ここでも、単純化するため、アプリケーションのビルドに必要な ASP.NET MVC framework の機能の最小数を活用移動します。</span><span class="sxs-lookup"><span data-stu-id="4696f-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="4696f-125">たとえば、私たちはありませんの恩恵をテスト駆動型開発。</span><span class="sxs-lookup"><span data-stu-id="4696f-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="4696f-126">アプリケーションを作成するためには、それぞれ、次の手順を完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="4696f-127">ASP.NET MVC Web アプリケーション プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="4696f-128">データベースの作成</span><span class="sxs-lookup"><span data-stu-id="4696f-128">Create the database</span></span>
3. <span data-ttu-id="4696f-129">データベース モデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-129">Create the database model</span></span>
4. <span data-ttu-id="4696f-130">ASP.NET MVC コント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="4696f-131">ASP.NET MVC ビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="4696f-132">準備作業</span><span class="sxs-lookup"><span data-stu-id="4696f-132">Preliminaries</span></span>

<span data-ttu-id="4696f-133">Visual Studio 2008 または Visual Web Developer 2008 Express、ASP.NET MVC アプリケーションを構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="4696f-134">また、ASP.NET MVC framework をダウンロードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="4696f-135">Visual Studio 2008 を所有していない場合は、この web サイトから、Visual Studio 2008 の 90 日間試用版をダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="4696f-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="4696f-136">または、する ASP.NET MVC アプリケーションを作成できます Visual Web Developer Express 2008。</span><span class="sxs-lookup"><span data-stu-id="4696f-136">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="4696f-137">Visual Web Developer Express を使用すると、Service Pack 1 がインストールされているが必要です。</span><span class="sxs-lookup"><span data-stu-id="4696f-137">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="4696f-138">Visual Web Developer 2008 Express with Service Pack 1 は、この web サイトからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="4696f-138">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="4696f-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span><span class="sxs-lookup"><span data-stu-id="4696f-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="4696f-140">Visual Studio 2008 または Visual Web Developer 2008 をインストールした後は、ASP.NET MVC framework をインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-140">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="4696f-141">ASP.NET MVC フレームワークは、次の web サイトからダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="4696f-141">You can download the ASP.NET MVC framework from the following website:</span></span>

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="4696f-142">ASP.NET framework と ASP.NET MVC フレームワークを個別にダウンロードする代わりに、Web Platform Installer の利点を実行できます。</span><span class="sxs-lookup"><span data-stu-id="4696f-142">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="4696f-143">Web Platform Installer は、アプリケーションを簡単にインストールされているアプリケーションを管理することができますが、コンピューターです。</span><span class="sxs-lookup"><span data-stu-id="4696f-143">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)


## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="4696f-144">ASP.NET MVC Web アプリケーション プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-144">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="4696f-145">Visual Studio 2008 で新しい ASP.NET MVC Web アプリケーション プロジェクトを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="4696f-145">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="4696f-146">メニュー オプションを選択**ファイル、新しいプロジェクト**図 1 新しいプロジェクト ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-146">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="4696f-147">プログラミング言語として C# を選択し、ASP.NET MVC Web アプリケーション プロジェクト テンプレートを選択します。</span><span class="sxs-lookup"><span data-stu-id="4696f-147">Select C# as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="4696f-148">プロジェクト MovieApp の名前を付け、[ok] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-148">Give your project the name MovieApp and click the OK button.</span></span>


<span data-ttu-id="4696f-149">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-149">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)</span></span>

<span data-ttu-id="4696f-150">**図 01**:[新しいプロジェクト] ダイアログ ボックス ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-150">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))</span></span>


<span data-ttu-id="4696f-151">必ず、新しいプロジェクト ダイアログの上部にあるドロップダウン リストから .NET Framework 3.5 を選択するか、ASP.NET MVC Web アプリケーション プロジェクト テンプレートは表示されません。</span><span class="sxs-lookup"><span data-stu-id="4696f-151">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>


<span data-ttu-id="4696f-152">新しい MVC Web アプリケーション プロジェクトを作成するたびに Visual Studio では、個別の単体テスト プロジェクトを作成するように求められます。</span><span class="sxs-lookup"><span data-stu-id="4696f-152">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="4696f-153">図 2 ダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-153">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="4696f-154">いますしないテストは作成このチュートリアルでは時間的制約のためであり、そうする必要がありますだと少しこの) を選択、**いいえ**オプションを選択し、をクリックして、 **OK**ボタン。</span><span class="sxs-lookup"><span data-stu-id="4696f-154">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4696f-155">Visual Web Developer では、テスト プロジェクトはサポートされません。</span><span class="sxs-lookup"><span data-stu-id="4696f-155">Visual Web Developer does not support test projects.</span></span>


<span data-ttu-id="4696f-156">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-156">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)</span></span>

<span data-ttu-id="4696f-157">**図 02**:単体テスト プロジェクトの作成 ダイアログ ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-157">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))</span></span>


<span data-ttu-id="4696f-158">ASP.NET MVC アプリケーションが標準的な一連のフォルダー: モデル、ビュー、およびコント ローラーのフォルダー。</span><span class="sxs-lookup"><span data-stu-id="4696f-158">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="4696f-159">この標準的な一連のソリューション エクスプ ローラー ウィンドウでフォルダーを確認できます。</span><span class="sxs-lookup"><span data-stu-id="4696f-159">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="4696f-160">私たちは、映画データベース アプリケーションをビルドするにはそれぞれのモデル、ビュー、およびコント ローラーのフォルダーにファイルを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-160">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="4696f-161">Visual Studio で新しい MVC アプリケーションを作成するときに、サンプル アプリケーションを取得します。</span><span class="sxs-lookup"><span data-stu-id="4696f-161">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="4696f-162">最初から開始するため、このサンプル アプリケーションのコンテンツを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-162">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="4696f-163">次のファイルと、次のフォルダーを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-163">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="4696f-164">Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="4696f-164">Controllers\HomeController.cs</span></span>
- <span data-ttu-id="4696f-165">Views\Home</span><span class="sxs-lookup"><span data-stu-id="4696f-165">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="4696f-166">データベースの作成</span><span class="sxs-lookup"><span data-stu-id="4696f-166">Creating the Database</span></span>

<span data-ttu-id="4696f-167">ムービー データベース レコードを保持するためにデータベースを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-167">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="4696f-168">さいわい、Visual Studio には、SQL Server Express という名前のフリー データベースが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-168">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="4696f-169">データベースを作成する次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="4696f-169">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="4696f-170">アプリを右クリックして\_メニュー オプションを選択して、ソリューション エクスプ ローラー ウィンドウで、データ フォルダー**追加]、[新しい項目の**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-170">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="4696f-171">選択、**データ**カテゴリと選択、 **SQL Server データベース**テンプレート (図 3 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="4696f-171">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="4696f-172">新しいデータベースの名前*MoviesDB.mdf*  をクリックし、**追加**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-172">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="4696f-173">アプリにある MoviesDB.mdf ファイルをダブルクリックして、データベースに接続することができます、データベースを作成した後\_データ フォルダー。</span><span class="sxs-lookup"><span data-stu-id="4696f-173">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="4696f-174">MoviesDB.mdf ファイルをダブルクリックすると、サーバー エクスプ ローラー ウィンドウが開きます。</span><span class="sxs-lookup"><span data-stu-id="4696f-174">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4696f-175">サーバー エクスプ ローラー ウィンドウには、Visual Web Developer の場合、データベース エクスプ ローラー ウィンドウがという名前です。</span><span class="sxs-lookup"><span data-stu-id="4696f-175">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>


<span data-ttu-id="4696f-176">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-176">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)</span></span>

<span data-ttu-id="4696f-177">**図 03**:Microsoft SQL Server データベースを作成する ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-177">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))</span></span>


<span data-ttu-id="4696f-178">次に、新しいデータベースのテーブルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-178">Next, we need to create a new database table.</span></span> <span data-ttu-id="4696f-179">サーバー エクスプ ローラー ウィンドウ内でテーブル フォルダーを右クリックし、メニュー オプションを選択**新しいテーブルの追加**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-179">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="4696f-180">このメニュー オプションを選択すると、データベースのテーブル デザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="4696f-180">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="4696f-181">次のデータベース列を作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-181">Create the following database columns:</span></span>

<a id="0.1_table01"></a>


| <span data-ttu-id="4696f-182">**列名**</span><span class="sxs-lookup"><span data-stu-id="4696f-182">**Column Name**</span></span> | <span data-ttu-id="4696f-183">**データ型**</span><span class="sxs-lookup"><span data-stu-id="4696f-183">**Data Type**</span></span> | <span data-ttu-id="4696f-184">**Null を許容します。**</span><span class="sxs-lookup"><span data-stu-id="4696f-184">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4696f-185">ID</span><span class="sxs-lookup"><span data-stu-id="4696f-185">Id</span></span> | <span data-ttu-id="4696f-186">Int</span><span class="sxs-lookup"><span data-stu-id="4696f-186">Int</span></span> | <span data-ttu-id="4696f-187">False</span><span class="sxs-lookup"><span data-stu-id="4696f-187">False</span></span> |
| <span data-ttu-id="4696f-188">Title</span><span class="sxs-lookup"><span data-stu-id="4696f-188">Title</span></span> | <span data-ttu-id="4696f-189">nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="4696f-189">Nvarchar(100)</span></span> | <span data-ttu-id="4696f-190">False</span><span class="sxs-lookup"><span data-stu-id="4696f-190">False</span></span> |
| <span data-ttu-id="4696f-191">ディレクター</span><span class="sxs-lookup"><span data-stu-id="4696f-191">Director</span></span> | <span data-ttu-id="4696f-192">nvarchar (100)</span><span class="sxs-lookup"><span data-stu-id="4696f-192">Nvarchar(100)</span></span> | <span data-ttu-id="4696f-193">False</span><span class="sxs-lookup"><span data-stu-id="4696f-193">False</span></span> |
| <span data-ttu-id="4696f-194">DateReleased</span><span class="sxs-lookup"><span data-stu-id="4696f-194">DateReleased</span></span> | <span data-ttu-id="4696f-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="4696f-195">DateTime</span></span> | <span data-ttu-id="4696f-196">False</span><span class="sxs-lookup"><span data-stu-id="4696f-196">False</span></span> |


<span data-ttu-id="4696f-197">最初の列、Id 列には、2 つの特殊なプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="4696f-197">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="4696f-198">最初に、Id 列を主キー列としてマークする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-198">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="4696f-199">Id 列を選択すると、クリックして、**主キーの設定**(キーのようなアイコンは) ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-199">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="4696f-200">次に、Id 列が Id 列としてマークする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-200">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="4696f-201">列のプロパティ ウィンドウでは、Identity の指定 セクションまでスクロールしを展開します。</span><span class="sxs-lookup"><span data-stu-id="4696f-201">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="4696f-202">変更、 **Id**プロパティ値を**はい**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-202">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="4696f-203">完了したら、図 4 ようテーブルになります。</span><span class="sxs-lookup"><span data-stu-id="4696f-203">When you are finished, the table should look like Figure 4.</span></span>


<span data-ttu-id="4696f-204">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-204">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)</span></span>

<span data-ttu-id="4696f-205">**図 04**:映画データベース テーブル ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-205">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))</span></span>


<span data-ttu-id="4696f-206">最後の手順では、新しいテーブルを保存します。</span><span class="sxs-lookup"><span data-stu-id="4696f-206">The final step is to save the new table.</span></span> <span data-ttu-id="4696f-207">保存ボタン (フロッピー ディスクのアイコン) をクリックし、新しいテーブル名の映画を提供します。</span><span class="sxs-lookup"><span data-stu-id="4696f-207">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="4696f-208">テーブルの作成が完了したら、ムービー レコードの一部をテーブルに追加します。</span><span class="sxs-lookup"><span data-stu-id="4696f-208">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="4696f-209">サーバー エクスプ ローラー ウィンドウで映画のテーブルを右クリックし、メニュー オプションを選択**テーブル データの表示**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-209">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="4696f-210">(図 5 参照)、お気に入りの映画の一覧を入力します。</span><span class="sxs-lookup"><span data-stu-id="4696f-210">Enter a list of your favorite movies (see Figure 5).</span></span>


<span data-ttu-id="4696f-211">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-211">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)</span></span>

<span data-ttu-id="4696f-212">**図 05**:ムービーのレコードの入力 ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-212">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))</span></span>


## <a name="creating-the-model"></a><span data-ttu-id="4696f-213">モデルを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-213">Creating the Model</span></span>

<span data-ttu-id="4696f-214">次に、データベースを表すクラスのセットを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-214">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="4696f-215">データベース モデルを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-215">We need to create a database model.</span></span> <span data-ttu-id="4696f-216">移動、データベース モデルのクラスを自動的に生成する Microsoft Entity Framework を活用します。</span><span class="sxs-lookup"><span data-stu-id="4696f-216">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4696f-217">ASP.NET MVC フレームワークは、Microsoft Entity Framework には関連付けられません。</span><span class="sxs-lookup"><span data-stu-id="4696f-217">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="4696f-218">さまざまなオブジェクト リレーショナル マッピングを活用して、データベース モデル クラスを作成できます (または/M) LINQ to SQL、Subsonic、および NHibernate などのツール。</span><span class="sxs-lookup"><span data-stu-id="4696f-218">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>


<span data-ttu-id="4696f-219">エンティティ データ モデル ウィザードを起動する次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="4696f-219">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="4696f-220">ソリューション エクスプ ローラー ウィンドウおよびメニュー オプションを選択して、モデル フォルダーを右クリックして**追加、新しい項目の**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-220">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="4696f-221">選択、**データ**カテゴリと選択、 **ADO.NET Entity Data Model**テンプレート。</span><span class="sxs-lookup"><span data-stu-id="4696f-221">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="4696f-222">データ モデルに名前を付けます*MoviesDBModel.edmx*  をクリックし、**追加**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-222">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="4696f-223">[追加] ボタンをクリックした後、Entity Data Model ウィザードでは、(図 6 参照) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-223">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="4696f-224">ウィザードの次の手順に従います。</span><span class="sxs-lookup"><span data-stu-id="4696f-224">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="4696f-225">**モデルのコンテンツの選択**手順で、**データベースから生成**オプション。</span><span class="sxs-lookup"><span data-stu-id="4696f-225">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="4696f-226">**データ接続の選択**ステップで、使用、 *MoviesDB.mdf*データ接続と名前*MoviesDBEntities*接続の設定。</span><span class="sxs-lookup"><span data-stu-id="4696f-226">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="4696f-227">をクリックして、**次**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-227">Click the **Next** button.</span></span>
3. <span data-ttu-id="4696f-228">**データベース オブジェクトの選択**ステップ、[テーブル] ノードを展開し、映画のテーブルを選択します。</span><span class="sxs-lookup"><span data-stu-id="4696f-228">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="4696f-229">名前空間を入力*MovieApp.Models*  をクリックし、**完了**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-229">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>


<span data-ttu-id="4696f-230">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-230">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)</span></span>

<span data-ttu-id="4696f-231">**図 06**:Entity Data Model ウィザードでデータベース モデルを生成する ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-231">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))</span></span>


<span data-ttu-id="4696f-232">Entity Data Model ウィザードを完了すると、Entity Data Model のデザイナーが開きます。</span><span class="sxs-lookup"><span data-stu-id="4696f-232">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="4696f-233">デザイナーは、映画データベース テーブルを表示する必要があります (図 7 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="4696f-233">The Designer should display the Movies database table (see Figure 7).</span></span>


<span data-ttu-id="4696f-234">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-234">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)</span></span>

<span data-ttu-id="4696f-235">**図 07**:Entity Data Model デザイナー ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-235">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))</span></span>


<span data-ttu-id="4696f-236">続行する前に 1 つの変更を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-236">We need to make one change before we continue.</span></span> <span data-ttu-id="4696f-237">という名前のモデル クラスを生成するエンティティのデータ ウィザード*映画*映画データベース テーブルを表します。</span><span class="sxs-lookup"><span data-stu-id="4696f-237">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="4696f-238">映画クラスを使用して、特定のムービーを表す、ためにクラスの名前を変更する必要があります*ムービー*の代わりに*映画*(単数形ではなく複数形)。</span><span class="sxs-lookup"><span data-stu-id="4696f-238">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="4696f-239">デザイナー画面で、クラスの名前をダブルクリックし、ムービーからムービーにクラスの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="4696f-239">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="4696f-240">この変更を加えたら、 をクリックして、**保存**ムービー クラスを生成する (フロッピー ディスクのアイコン) をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-240">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="4696f-241">ASP.NET MVC コント ローラーの作成</span><span class="sxs-lookup"><span data-stu-id="4696f-241">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="4696f-242">次の手順では、ASP.NET MVC コント ローラーを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-242">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="4696f-243">コント ローラーは、ユーザーが、ASP.NET MVC アプリケーションと対話する方法を制御する責任を負います。</span><span class="sxs-lookup"><span data-stu-id="4696f-243">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="4696f-244">この場合は、以下の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="4696f-244">Follow these steps:</span></span>

1. <span data-ttu-id="4696f-245">ソリューション エクスプ ローラー ウィンドウで、Controllers フォルダーを右クリックし、メニュー オプションを選択**追加、コント ローラー**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-245">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="4696f-246">コント ローラーの追加 ダイアログ ボックスで、名前を入力します。 *HomeController*というラベルの付いたチェック ボックスをオンおよび**アクション メソッドの作成、更新、および詳細のシナリオを追加**(図 8 参照)。</span><span class="sxs-lookup"><span data-stu-id="4696f-246">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="4696f-247">をクリックして、**追加**をプロジェクトに新しいコント ローラーを追加するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-247">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="4696f-248">次の手順を完了すると、リスト 1 で、コント ローラーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-248">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="4696f-249">インデックスの詳細は、作成、という名前のメソッドが含まれていることを確認および編集します。</span><span class="sxs-lookup"><span data-stu-id="4696f-249">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="4696f-250">次のセクションを使用するこれらのメソッドを取得するために必要なコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="4696f-250">In the following sections, we'll add the necessary code to get these methods to work.</span></span>


<span data-ttu-id="4696f-251">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-251">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)</span></span>

<span data-ttu-id="4696f-252">**図 08**:新しい ASP.NET MVC コント ローラーの追加 ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-252">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))</span></span>


<span data-ttu-id="4696f-253">**Listing 1 – Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="4696f-253">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample1.cs)]

## <a name="listing-database-records"></a><span data-ttu-id="4696f-254">データベース レコードの一覧</span><span class="sxs-lookup"><span data-stu-id="4696f-254">Listing Database Records</span></span>

<span data-ttu-id="4696f-255">Home コント ローラーの Index() メソッドは、ASP.NET MVC アプリケーションの既定の方法です。</span><span class="sxs-lookup"><span data-stu-id="4696f-255">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="4696f-256">ASP.NET MVC アプリケーションを実行すると、Index() メソッドが呼び出される最初のコント ローラー メソッドを使用します。</span><span class="sxs-lookup"><span data-stu-id="4696f-256">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="4696f-257">Index() メソッドを使用して、映画データベース テーブルからレコードの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="4696f-257">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="4696f-258">データベースの利用 Index() メソッドを使用して、ムービーのデータベース レコードを取得する前に作成したモデル クラス移動します。</span><span class="sxs-lookup"><span data-stu-id="4696f-258">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="4696f-259">リスト 2 で HomeController クラスを変更しましたという名前の新しいプライベート フィールドが含まれるように\_db します。</span><span class="sxs-lookup"><span data-stu-id="4696f-259">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="4696f-260">MoviesDBEntities クラスは、データベース モデルを表し、このクラスを使用して、データベースと通信します。</span><span class="sxs-lookup"><span data-stu-id="4696f-260">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="4696f-261">リスト 2 で Index() メソッドも変更しました。</span><span class="sxs-lookup"><span data-stu-id="4696f-261">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="4696f-262">Index() メソッドでは、MoviesDBEntities クラスを使用して、映画データベース テーブルからすべてのムービーのレコードを取得します。</span><span class="sxs-lookup"><span data-stu-id="4696f-262">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="4696f-263">式 *\_db します。MovieSet.ToList()* 映画データベース テーブルからすべてのムービーのレコードの一覧を返します。</span><span class="sxs-lookup"><span data-stu-id="4696f-263">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="4696f-264">ムービーの一覧は、ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-264">The list of movies is passed to the view.</span></span> <span data-ttu-id="4696f-265">View() メソッドに渡されるものは、ビュー データとして、ビューに渡されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-265">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="4696f-266">**2 – Controllers/HomeController.cs (変更された Index メソッド) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="4696f-266">**Listing 2 – Controllers/HomeController.cs (modified Index method)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample2.cs)]

<span data-ttu-id="4696f-267">Index() メソッドは、インデックスをという名前のビューを返します。</span><span class="sxs-lookup"><span data-stu-id="4696f-267">The Index() method returns a view named Index.</span></span> <span data-ttu-id="4696f-268">ムービー データベース レコードの一覧を表示するには、このビューを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-268">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="4696f-269">この場合は、以下の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="4696f-269">Follow these steps:</span></span>


<span data-ttu-id="4696f-270">プロジェクトをビルドする必要があります (メニュー オプションを選択**ソリューションのビルドをビルドします**) 開く前に、**ビューの追加**ダイアログまたはクラスを持たないに表示されます、**データ クラスを表示**。ドロップダウン リスト。</span><span class="sxs-lookup"><span data-stu-id="4696f-270">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>


1. <span data-ttu-id="4696f-271">コード エディターで Index() メソッドを右クリックし、メニュー オプションを選択**ビューの追加**(図 9 参照)。</span><span class="sxs-lookup"><span data-stu-id="4696f-271">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="4696f-272">ビューの追加 ダイアログ ボックスで、チェック ボックスをオンにというラベルが付いたことを確認します**厳密に型指定されたビューを作成する**がチェックされます。</span><span class="sxs-lookup"><span data-stu-id="4696f-272">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="4696f-273">**コンテンツを表示**ドロップダウン リストで、値を選択*一覧*します。</span><span class="sxs-lookup"><span data-stu-id="4696f-273">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="4696f-274">**データ クラスを表示**ドロップダウン リストで、値を選択して*MovieApp.Models.Movie*します。</span><span class="sxs-lookup"><span data-stu-id="4696f-274">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="4696f-275">新しいを作成する [追加] ボタンをクリックします (図 10 参照) を表示します。</span><span class="sxs-lookup"><span data-stu-id="4696f-275">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="4696f-276">次の手順を完了すると、Index.aspx をという名前の新しいビューは views \home フォルダーに追加されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-276">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="4696f-277">リスト 3 では、インデックス ビューの内容が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4696f-277">The contents of the Index view are included in Listing 3.</span></span>


<span data-ttu-id="4696f-278">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-278">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)</span></span>

<span data-ttu-id="4696f-279">**図 09**:コント ローラー アクションからビューの追加 ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-279">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))</span></span>


<span data-ttu-id="4696f-280">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-280">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)</span></span>

<span data-ttu-id="4696f-281">**図 10**:ビューの追加 ダイアログで新しいビューを作成する ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-281">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))</span></span>


<span data-ttu-id="4696f-282">**Listing 3 – Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="4696f-282">**Listing 3 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample3.aspx)]

<span data-ttu-id="4696f-283">インデックス ビューには、すべての HTML テーブル内の映画データベース テーブルからムービー レコードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-283">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="4696f-284">ビューには、ViewData.Model プロパティで表される各ムービーを反復処理する foreach ループが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-284">The view contains a foreach loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="4696f-285">F5 キーを押すことによって、アプリケーションを実行すると、図 11 では、web ページが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-285">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>


<span data-ttu-id="4696f-286">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-286">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)</span></span>

<span data-ttu-id="4696f-287">**図 11**:インデックス ビュー ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-287">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))</span></span>


## <a name="creating-new-database-records"></a><span data-ttu-id="4696f-288">新しいデータベース レコードを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-288">Creating New Database Records</span></span>

<span data-ttu-id="4696f-289">前のセクションで作成したインデックス ビューには、新しいデータベース レコードを作成するためのリンクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-289">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="4696f-290">みましょうロジックを実装および新しいムービーのデータベース レコードを作成するために必要なビューを作成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-290">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="4696f-291">Home コント ローラーには、Create() という名前の 2 つのメソッドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-291">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="4696f-292">最初の Create() メソッドにパラメーターがありません。</span><span class="sxs-lookup"><span data-stu-id="4696f-292">The first Create() method has no parameters.</span></span> <span data-ttu-id="4696f-293">Create() メソッドのこのオーバー ロードを使用して、新しいムービーのデータベース レコードを作成するための HTML フォームを表示できます。</span><span class="sxs-lookup"><span data-stu-id="4696f-293">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="4696f-294">2 番目の Create() メソッドでは、FormCollection パラメーターがあります。</span><span class="sxs-lookup"><span data-stu-id="4696f-294">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="4696f-295">Create() メソッドのこのオーバー ロードは、新しいムービーを作成するための HTML フォームがサーバーに投稿されたときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-295">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="4696f-296">この 2 つ目の Create() メソッドが AcceptVerbs 属性、メソッドが HTTP POST 操作を実行しない限り、呼び出されていることを防ぎますを持つことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4696f-296">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP POST operation is performed.</span></span>

<span data-ttu-id="4696f-297">この 2 つ目の Create() メソッドは、リスト 4 の更新された HomeController クラスに変更されています。</span><span class="sxs-lookup"><span data-stu-id="4696f-297">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="4696f-298">Create() メソッドの新しいバージョンは、ムービー パラメーターを受け取り、映画データベース テーブルに新しいビデオを挿入するためのロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-298">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4696f-299">Bind 属性に注意してください。</span><span class="sxs-lookup"><span data-stu-id="4696f-299">Notice the Bind attribute.</span></span> <span data-ttu-id="4696f-300">HTML フォームからムービー Id プロパティを更新するため、このプロパティを明示的に除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-300">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>


<span data-ttu-id="4696f-301">**4 – controllers \homecontroller.cs (変更の作成方法) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="4696f-301">**Listing 4 – Controllers\HomeController.cs (modified Create method)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample4.cs)]

<span data-ttu-id="4696f-302">Visual Studio で簡単に新しいムービー データベースを作成するためのフォームを作成できます (図 12 を参照してください) を記録します。</span><span class="sxs-lookup"><span data-stu-id="4696f-302">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="4696f-303">この場合は、以下の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="4696f-303">Follow these steps:</span></span>

1. <span data-ttu-id="4696f-304">コード エディターで Create() メソッドを右クリックし、メニュー オプションを選択**ビューの追加**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-304">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="4696f-305">チェック ボックスをオンにというラベルが付いたことを確認します。**厳密に型指定されたビューを作成する**がチェックされます。</span><span class="sxs-lookup"><span data-stu-id="4696f-305">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="4696f-306">**コンテンツを表示**ドロップダウン リストで、値を選択*作成*です。</span><span class="sxs-lookup"><span data-stu-id="4696f-306">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="4696f-307">**データ クラスを表示**ドロップダウン リストで、値を選択して*MovieApp.Models.Movie*します。</span><span class="sxs-lookup"><span data-stu-id="4696f-307">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="4696f-308">をクリックして、**追加**新しいビューを作成するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-308">Click the **Add** button to create the new view.</span></span>


<span data-ttu-id="4696f-309">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-309">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)</span></span>

<span data-ttu-id="4696f-310">**図 12**:作成ビューの追加 ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-310">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))</span></span>


<span data-ttu-id="4696f-311">Visual Studio は、自動的にリスト 5 で、ビューを生成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-311">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="4696f-312">このビューには、各ムービー クラスのプロパティに対応するフィールドを含む HTML フォームが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-312">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="4696f-313">**Listing 5 – Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="4696f-313">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="4696f-314">ビューの追加 ダイアログで作成した HTML 形式では、フォームの Id フィールドを生成します。</span><span class="sxs-lookup"><span data-stu-id="4696f-314">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="4696f-315">Id 列が Id 列であるため、このフォームのフィールドは不要し、安全に削除することができます。</span><span class="sxs-lookup"><span data-stu-id="4696f-315">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>


<span data-ttu-id="4696f-316">作成ビューを追加した後は、データベースに新しいムービーのレコードを追加できます。</span><span class="sxs-lookup"><span data-stu-id="4696f-316">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="4696f-317">F5 キーを押してアプリケーションを実行し、図 13 でフォームを新規作成 をクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-317">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="4696f-318">完了し、フォームを送信する場合、新しいムービーのデータベース レコードが作成されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-318">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="4696f-319">フォームの検証を自動的に取得することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4696f-319">Notice that you get form validation automatically.</span></span> <span data-ttu-id="4696f-320">、映画のリリース日を入力を怠ると、または無効なリリース日を入力する、、フォームが再表示し、リリース日フィールドが強調表示されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-320">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>


<span data-ttu-id="4696f-321">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-321">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)</span></span>

<span data-ttu-id="4696f-322">**図 13**:新しいムービーのデータベース レコードを作成する ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-322">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))</span></span>


## <a name="editing-existing-database-records"></a><span data-ttu-id="4696f-323">既存のデータベース レコードの編集</span><span class="sxs-lookup"><span data-stu-id="4696f-323">Editing Existing Database Records</span></span>

<span data-ttu-id="4696f-324">前のセクションでは、一覧表示し、新しいデータベース レコードを作成する方法を説明しました。</span><span class="sxs-lookup"><span data-stu-id="4696f-324">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="4696f-325">この最後のセクションでは、既存のデータベース レコードを編集する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4696f-325">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="4696f-326">最初に、編集フォームを生成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-326">First, we need to generate the Edit form.</span></span> <span data-ttu-id="4696f-327">Visual Studio は私たちにとって編集フォームを自動的に生成されるため、この手順は簡単です。</span><span class="sxs-lookup"><span data-stu-id="4696f-327">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="4696f-328">HomeController.cs クラスを Visual Studio コード エディターで開き、次の手順します。</span><span class="sxs-lookup"><span data-stu-id="4696f-328">Open the HomeController.cs class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="4696f-329">コード エディターで Edit() メソッドを右クリックし、メニュー オプションを選択**ビューの追加**(図 14 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="4696f-329">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="4696f-330">チェック ボックスをラベル付け**厳密に型指定されたビューを作成する**します。</span><span class="sxs-lookup"><span data-stu-id="4696f-330">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="4696f-331">**コンテンツを表示**ドロップダウン リストで、値を選択*編集*します。</span><span class="sxs-lookup"><span data-stu-id="4696f-331">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="4696f-332">**データ クラスを表示**ドロップダウン リストで、値を選択して*MovieApp.Models.Movie*します。</span><span class="sxs-lookup"><span data-stu-id="4696f-332">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="4696f-333">をクリックして、**追加**新しいビューを作成するボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4696f-333">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="4696f-334">次の手順を完了するには、views \home フォルダーに Edit.aspx をという名前の新しいビューが追加されます。</span><span class="sxs-lookup"><span data-stu-id="4696f-334">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="4696f-335">このビューには、ムービーのレコードを編集するための HTML フォームが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-335">This view contains an HTML form for editing a movie record.</span></span>


<span data-ttu-id="4696f-336">[![[新しいプロジェクト] ダイアログ ボックス](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="4696f-336">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)</span></span>

<span data-ttu-id="4696f-337">**図 14**:編集ビューの追加 ([フルサイズの画像を表示する をクリックします](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))。</span><span class="sxs-lookup"><span data-stu-id="4696f-337">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))</span></span>


> [!NOTE] 
> 
> <span data-ttu-id="4696f-338">編集ビューには、映画 Id プロパティに対応する HTML フォーム フィールドが含まれています。</span><span class="sxs-lookup"><span data-stu-id="4696f-338">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="4696f-339">Id プロパティの値を編集しているユーザーをしたくないため、このフォームのフィールドを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-339">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>


<span data-ttu-id="4696f-340">最後に、データベース レコードの編集をサポートするように、Home コント ローラーを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4696f-340">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="4696f-341">更新された HomeController クラスは、6 の一覧に含まれます。</span><span class="sxs-lookup"><span data-stu-id="4696f-341">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="4696f-342">**6 – controllers \homecontroller.cs (Edit メソッド) を一覧表示します。**</span><span class="sxs-lookup"><span data-stu-id="4696f-342">**Listing 6 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample6.cs)]

<span data-ttu-id="4696f-343">リストの 6 で追加のロジック Edit() メソッドの両方のオーバー ロードを追加しました。</span><span class="sxs-lookup"><span data-stu-id="4696f-343">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="4696f-344">最初の Edit() メソッドは、メソッドに渡される Id パラメーターに対応するムービー データベース レコードを返します。</span><span class="sxs-lookup"><span data-stu-id="4696f-344">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="4696f-345">2 番目のオーバー ロードは、データベースのムービーのレコードに更新プログラムを実行します。</span><span class="sxs-lookup"><span data-stu-id="4696f-345">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="4696f-346">元のビデオを取得して呼び出して ApplyPropertyChanges()、データベース内の既存のムービーを更新する必要がありますに注意してください。</span><span class="sxs-lookup"><span data-stu-id="4696f-346">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="4696f-347">まとめ</span><span class="sxs-lookup"><span data-stu-id="4696f-347">Summary</span></span>

<span data-ttu-id="4696f-348">このチュートリアルの目的は、ASP.NET MVC アプリケーションを構築するためのエクスペリエンスの感覚をつかむことにしました。</span><span class="sxs-lookup"><span data-stu-id="4696f-348">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="4696f-349">ASP.NET MVC web アプリケーションを構築するが、Active Server Pages または ASP.NET アプリケーションの開発エクスペリエンスのとよく似ていますが検出されたと思います。</span><span class="sxs-lookup"><span data-stu-id="4696f-349">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="4696f-350">このチュートリアルでは、ASP.NET MVC フレームワークの最も基本的な機能のみを調査します。</span><span class="sxs-lookup"><span data-stu-id="4696f-350">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="4696f-351">今後のチュートリアルでは、私たちをさらに深くコント ローラー、コント ローラー アクション、ビュー、データの表示、および HTML ヘルパーなどのトピックです。</span><span class="sxs-lookup"><span data-stu-id="4696f-351">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4696f-352">次へ</span><span class="sxs-lookup"><span data-stu-id="4696f-352">Next</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb.md)