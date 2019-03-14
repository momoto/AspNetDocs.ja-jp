---
title: MVC アプリへのビューの追加
author: Rick-Anderson
description: MVC アプリへのビューの追加
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: afa7584529566ebe82a0eb3849de89bd0df064bd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051009"
---
<a name="adding-a-view"></a><span data-ttu-id="0fa89-103">ビューの追加</span><span class="sxs-lookup"><span data-stu-id="0fa89-103">Adding a View</span></span>
====================
<span data-ttu-id="0fa89-104">によって[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="0fa89-104">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](sample/code-location.md)]

<span data-ttu-id="0fa89-105">このセクションではしようとしている変更、`HelloWorldController`ビュー テンプレート ファイルを明確には、クライアントへの HTML 応答を生成するプロセスをカプセル化を使用するクラス。</span><span class="sxs-lookup"><span data-stu-id="0fa89-105">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span> 

<span data-ttu-id="0fa89-106">使用してビュー テンプレート ファイルを作成します、 [Razor ビュー エンジン](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-106">You'll create a view template file using the [Razor view engine](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md).</span></span> <span data-ttu-id="0fa89-107">Razor ベースのビュー テンプレートが、 *.cshtml*ファイル拡張子、および HTML 出力を C# を使用して作成する洗練された方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-107">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="0fa89-108">Razor の文字と、ビュー テンプレートの作成時に必要なキーストローク数を最小化し、ワークフローのコーディングの高速で、流体できます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-108">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="0fa89-109">現在、`Index` メソッドは、コントローラー クラスでハード コーディングされるメッセージを含む文字列を返します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-109">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="0fa89-110">変更、`Index`メソッドを呼び出すコント ローラー[ビュー](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View)メソッドは、次のコードに示すようにします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-110">Change the `Index` method to call the controllers [View](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) method, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

<span data-ttu-id="0fa89-111">`Index`上記のメソッドでは、ビュー テンプレートを使用して、ブラウザーへの HTML 応答を生成します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-111">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="0fa89-112">コント ローラー メソッド (とも呼ばれます[アクション メソッド](http://rachelappel.com/asp.net-mvc-actionresults-explained)) など、`Index`一般に、上記のメソッドが返す、 [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (から派生したクラスまたは[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx))、string と同様にないプリミティブ型。</span><span class="sxs-lookup"><span data-stu-id="0fa89-112">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="0fa89-113">右クリックして、 *Views\HelloWorld*フォルダーをクリックします**追加**、 をクリックし、**レイアウト (Razor) を使用する MVC 5 ビュー ページ**します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-113">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image1.png)   
  
<span data-ttu-id="0fa89-114">**項目の名前を指定** ダイアログ ボックスに、入力*インデックス*、順にクリックします**OK**します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-114">In the **Specify Name for Item** dialog box, enter *Index*, and then click **OK**.</span></span>  
  
![](adding-a-view/_static/image2.png)  
  
<span data-ttu-id="0fa89-115">**レイアウト ページの選択**ダイアログ ボックスで、既定値をそのまま使用 **\_Layout.cshtml**  をクリック**OK**。</span><span class="sxs-lookup"><span data-stu-id="0fa89-115">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image3.png)  
  
<span data-ttu-id="0fa89-116">上記のダイアログ ボックスで、 *views \shared*左側のウィンドウでフォルダーを選択します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-116">In the dialog above, the *Views\Shared* folder is selected in the left pane.</span></span> <span data-ttu-id="0fa89-117">カスタム レイアウト ファイルを別のフォルダーである場合は、選択する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-117">If you had a custom layout file in another folder, you could select it.</span></span> <span data-ttu-id="0fa89-118">チュートリアルの後半で、レイアウト ファイルについて説明します</span><span class="sxs-lookup"><span data-stu-id="0fa89-118">We'll talk about the layout file later in the tutorial</span></span>

<span data-ttu-id="0fa89-119">*MvcMovie\Views\HelloWorld\Index.cshtml*ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-119">The *MvcMovie\Views\HelloWorld\Index.cshtml* file is created.</span></span>

![](adding-a-view/_static/image4.png)

<span data-ttu-id="0fa89-120">次の強調表示されたマークアップを追加します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-120">Add the following highlighted markup.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

<span data-ttu-id="0fa89-121">右クリックして、 *Index.cshtml*ファイルおよび選択**ブラウザーで表示**します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-121">Right click the *Index.cshtml* file and select **View in Browser**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="0fa89-123">右クリック、 *Index.cshtml*ファイルおよび選択**Page Inspector で表示します。**</span><span class="sxs-lookup"><span data-stu-id="0fa89-123">You can also right click the *Index.cshtml* file and select **View in Page Inspector.**</span></span> <span data-ttu-id="0fa89-124">参照してください、 [Page Inspector チュートリアル](../../views/using-page-inspector-in-aspnet-mvc.md)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-124">See the [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) for more information.</span></span>

<span data-ttu-id="0fa89-125">また、アプリケーションを実行しを参照、`HelloWorld`コント ローラー (`http://localhost:xxxx/HelloWorld`)。</span><span class="sxs-lookup"><span data-stu-id="0fa89-125">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="0fa89-126">`Index`コント ローラーのメソッドは多くの作業を行わない; に単に、ステートメントを実行した`return View()`、指定されている、メソッドが応答をブラウザーにレンダリングするビュー テンプレート ファイルを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-126">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="0fa89-127">ASP.NET MVC の既定値を使用してに明示的に使用するビュー テンプレート ファイルの名前を指定していないので、 *Index.cshtml*でファイルの表示、 *\Views\HelloWorld*フォルダー。</span><span class="sxs-lookup"><span data-stu-id="0fa89-127">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="0fa89-128">次の図は、文字列&quot;こんにちは from our View Template!&quot;ビューにハードコーディングします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-128">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="0fa89-129">ように見えますね。</span><span class="sxs-lookup"><span data-stu-id="0fa89-129">Looks pretty good.</span></span> <span data-ttu-id="0fa89-130">ただし、ブラウザーのタイトル バーの表示"インデックス-My ASP.NET Application、"をページの上部にあるビッグ リンクという「アプリケーション名」に注意してください。</span><span class="sxs-lookup"><span data-stu-id="0fa89-130">However, notice that the browser's title bar shows "Index - My ASP.NET Application," and the big link at the top of the page says "Application name."</span></span> <span data-ttu-id="0fa89-131">によってどのようにブラウザー ウィンドウを作成、表示する右上にある 3 本の棒をクリックする必要がありますに、**ホーム**、**について**、**連絡先**、 **登録**と**ログイン**リンク。</span><span class="sxs-lookup"><span data-stu-id="0fa89-131">Depending on how small you make your browser window, you might need to click the three bars in the upper right to see the to the **Home**, **About**, **Contact**, **Register** and **Log in** links.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="0fa89-132">ビューとレイアウト ページを変更します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-132">Changing Views and Layout Pages</span></span>

<span data-ttu-id="0fa89-133">最初に、変更したい、&quot;アプリケーション名&quot;ページの上部にあるリンクです。</span><span class="sxs-lookup"><span data-stu-id="0fa89-133">First, you want to change the &quot;Application name&quot; link at the top of the page.</span></span> <span data-ttu-id="0fa89-134">このテキストはすべてのページに共通です。</span><span class="sxs-lookup"><span data-stu-id="0fa89-134">That text is common to every page.</span></span> <span data-ttu-id="0fa89-135">アプリケーション内の各ページに表示される場合でも、プロジェクト内の 1 か所で実際に実装されます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-135">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="0fa89-136">移動して、 */ビュー/共有*フォルダー**ソリューション エクスプ ローラー**を開くと、  *\_Layout.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="0fa89-136">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="0fa89-137">このファイルと呼ばれます、*レイアウト ページ*他のすべてのページを使用する共有フォルダー内にあるとします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-137">This file is called a *layout page* and it's in the shared folder that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="0fa89-139">レイアウト テンプレートを使用すると、1 つの場所で、サイトの HTML コンテナー レイアウトを指定し、そのサイト内の複数のページに適用できます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-139">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="0fa89-140">`@RenderBody()` という行を見つけます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-140">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="0fa89-141">`RenderBody` は、作成したビュー固有のページがすべて表示されるプレースホルダーで、レイアウト ページに&quot;ラップ&quot;されます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-141">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="0fa89-142">たとえば、選択した場合、**について**リンクを*Views\Home\About.cshtml*内でビューが表示される、`RenderBody`メソッド。</span><span class="sxs-lookup"><span data-stu-id="0fa89-142">For example, if you select the **About** link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="0fa89-143">タイトル要素の内容を変更します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-143">Change the contents of the title element.</span></span> <span data-ttu-id="0fa89-144">変更、 [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx)からレイアウト テンプレート&quot;アプリケーション名&quot;に&quot;MVC ムービー&quot;とコント ローラーから`Home`に`Movies`します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-144">Change the [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) in the layout template from &quot;Application name&quot; to &quot;MVC Movie&quot; and the controller from `Home` to `Movies`.</span></span> <span data-ttu-id="0fa89-145">完全なレイアウト ファイルは、以下に示します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-145">The complete layout file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

<span data-ttu-id="0fa89-146">アプリケーションと、次のようになりました注意実行&quot;MVC ムービー&quot;します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-146">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="0fa89-147">をクリックして、**について**リンク、およびするは、そのページの表示方法を参照してください。 &quot;MVC ムービー&quot;もします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-147">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="0fa89-148">レイアウト テンプレートで 1 回、変更を行うことができましたが、サイトのすべてのページで、新しいタイトルを反映します.</span><span class="sxs-lookup"><span data-stu-id="0fa89-148">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="0fa89-149">作成したときに、 *Views\HelloWorld\Index.cshtml*ファイルでは、次のコードが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0fa89-149">When we first created the *Views\HelloWorld\Index.cshtml* file, it contained the following code:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="0fa89-150">上記の Razor コードでは、レイアウト ページを明示的に設定です。</span><span class="sxs-lookup"><span data-stu-id="0fa89-150">The Razor code above is explicitly setting the layout page.</span></span> <span data-ttu-id="0fa89-151">確認、*ビュー\\_ViewStart.cshtml*ファイル、正確な同じ Razor マークアップが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0fa89-151">Examine the *Views\\_ViewStart.cshtml* file, it contains the exact same Razor markup.</span></span> <span data-ttu-id="0fa89-152">*[ビュー\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* ファイルは、すべてのビューを使用する一般的なレイアウトを定義、アウトまたは削除からそのコードをコメントするため、 *Views\HelloWorld\Index.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="0fa89-152">The *[Views\\_ViewStart.cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* file defines the common layout that all views will use, therefore you can comment out or remove that code from the *Views\HelloWorld\Index.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

<span data-ttu-id="0fa89-153">`Layout` プロパティを使用すれば、別のレイアウト ビューを設定することができます。また、`null` に設定して、レイアウト ファイルが使用されないようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-153">You can use the `Layout` property to set a different layout view, or set it to `null` so no layout file will be used.</span></span>

<span data-ttu-id="0fa89-154">ここで、インデックス ビューのタイトルを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0fa89-154">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="0fa89-155">開いている*MvcMovie\Views\HelloWorld\Index.cshtml*します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-155">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="0fa89-156">2 か所変更する場合: 最初に、テキスト表示される、ブラウザーのタイトルにおよび、セカンダリ ヘッダー (、`<h2>`要素)。</span><span class="sxs-lookup"><span data-stu-id="0fa89-156">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="0fa89-157">これを少し変えれば、コードのどの部分でアプリのどの部分が変更されるかを確認することができます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-157">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

<span data-ttu-id="0fa89-158">セット上のコードを表示する HTML のタイトルを示すために、`Title`のプロパティ、`ViewBag`オブジェクト (これは、 *Index.cshtml*テンプレートの表示)。</span><span class="sxs-lookup"><span data-stu-id="0fa89-158">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="0fa89-159">注意してレイアウト テンプレート ( *views \shared\\_Layout.cshtml* ) では、この値を使用して、`<title>`要素の一部として、`<head>`セクション html で以前に変更します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-159">Notice that the layout template ( *Views\Shared\\_Layout.cshtml* ) uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

<span data-ttu-id="0fa89-160">これを使用して`ViewBag`アプローチでは、渡すことができます簡単に他のパラメーター、テンプレートの表示と、レイアウト ファイルの間。</span><span class="sxs-lookup"><span data-stu-id="0fa89-160">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="0fa89-161">アプリケーションを実行します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-161">Run the application.</span></span> <span data-ttu-id="0fa89-162">ブラウザーのタイトル、プライマリ見出し、およびセカンダリ見出しが変更されていることに注意してください </span><span class="sxs-lookup"><span data-stu-id="0fa89-162">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="0fa89-163">(ブラウザーに変更内容が表示されない場合は、キャッシュされたコンテンツを表示している可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-163">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="0fa89-164">ブラウザーで Ctrl + F5 キーを押して、サーバーからの応答が強制的に読み込まれるようにしてください)。ブラウザーのタイトルが作成された、`ViewBag.Title`設定します、 *Index.cshtml*テンプレートと追加表示&quot;-Movie App&quot;レイアウト ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-164">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="0fa89-165">また方法でコンテンツ、 *Index.cshtml*とテンプレートの表示がマージされた、  *\_Layout.cshtml*テンプレートの表示と 1 つの HTML 応答がブラウザーに送信されました。</span><span class="sxs-lookup"><span data-stu-id="0fa89-165">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="0fa89-166">レイアウト テンプレートを使用すれば、アプリケーションのすべてのページに適用される変更をとても簡単に行うことができます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-166">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="0fa89-167">ごく一部&quot;データ&quot;(この場合、&quot;こんにちは from our View Template!&quot;メッセージ) はハード コーディング、ただしします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-167">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="0fa89-168">MVC アプリケーションには、 &quot;V&quot; (ビュー) があると、 &quot;C&quot; (コント ローラー) が&quot;M&quot;まだ (モデル)。</span><span class="sxs-lookup"><span data-stu-id="0fa89-168">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="0fa89-169">まもなく、データベースを作成し、モデル データを取得する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-169">Shortly, we'll walk through how to create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="0fa89-170">コントローラーからビューへのデータの受け渡し</span><span class="sxs-lookup"><span data-stu-id="0fa89-170">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="0fa89-171">データベースに移動してモデルについて説明する前に、まずについて説明しましょうコント ローラーからビューに情報を渡します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-171">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="0fa89-172">受信 URL 要求に応答には、コント ローラー クラスが呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-172">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="0fa89-173">コント ローラー クラスは、受信ブラウザーを処理するコードは、要求、データベースからデータを取得し、最終的には、ブラウザーに送信する応答の種類を決定を記述します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-173">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="0fa89-174">テンプレートの表示は、生成し、ブラウザーへの HTML 応答を書式設定するコント ローラーから使用できます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-174">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="0fa89-175">コント ローラーはどのようなデータまたはオブジェクトが応答をブラウザーにレンダリングするテンプレートの表示のために必要なを提供する責任を負います。</span><span class="sxs-lookup"><span data-stu-id="0fa89-175">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="0fa89-176">ベスト プラクティス: **ビュー テンプレートのビジネス ロジックを実行またはデータベースと直接やり取りする必要がありますしない**します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-176">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="0fa89-177">代わりに、ビュー テンプレートは、コント ローラーによって提供されるデータのみを操作する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-177">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="0fa89-178">この保守&quot;懸念事項の分離&quot;も利用できるコード クリーン、テストが容易な保守しやすくなります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-178">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="0fa89-179">現時点では、`Welcome`内のアクション メソッド、`HelloWorldController`クラスは、`name`と`numTimes`パラメーターとし、ブラウザーに直接値を出力します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-179">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="0fa89-180">この応答を文字列としてレンダリングするコント ローラーがあるのではなく、代わりにビュー テンプレートを使用するコント ローラーを変更してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0fa89-180">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="0fa89-181">このビュー テンプレートでは動的応答が生成されます。これは、応答を生成するために、コントローラーからビューに適量のデータを渡す必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-181">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="0fa89-182">コント ローラーにビュー テンプレートに必要な動的データ (パラメーター) を配置することでこれを行う、`ViewBag`ビュー テンプレートでアクセスできるオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="0fa89-182">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="0fa89-183">戻り、 *HelloWorldController.cs*ファイルし、変更、`Welcome`を追加するメソッド、`Message`と`NumTimes`値を`ViewBag`オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="0fa89-183">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="0fa89-184">`ViewBag` 動的オブジェクト、つまりに自由を配置します。`ViewBag`オブジェクトには定義されているプロパティがない内部に、何かを設定するまでです。</span><span class="sxs-lookup"><span data-stu-id="0fa89-184">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="0fa89-185">[ASP.NET MVC モデル バインド システム](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)名前付きパラメーターを自動的にマップされます (`name`と`numTimes`)、メソッドのパラメーターのアドレス バーで、クエリ文字列から。</span><span class="sxs-lookup"><span data-stu-id="0fa89-185">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="0fa89-186">完全な *HelloWorldController.cs* ファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-186">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

<span data-ttu-id="0fa89-187">これで、`ViewBag`オブジェクトに自動的にビューに渡されるデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0fa89-187">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span> <span data-ttu-id="0fa89-188">次に、[ようこそ] ビュー テンプレートをする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-188">Next, you need a Welcome view template!</span></span> <span data-ttu-id="0fa89-189">**ビルド**メニューの **ソリューションのビルド**(または Ctrl + Shift + B)、プロジェクトがコンパイルされるかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-189">In the **Build** menu, select **Build Solution** (or Ctrl+Shift+B) to make sure the project is compiled.</span></span> <span data-ttu-id="0fa89-190">右クリックして、 *Views\HelloWorld*フォルダーをクリックします**追加**、 をクリックし、**レイアウト (Razor) を使用する MVC 5 ビュー ページ**します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-190">Right click the *Views\HelloWorld* folder and click **Add**, then click **MVC 5 View Page with Layout (Razor)**.</span></span>
  
![](adding-a-view/_static/image10.png)   
  
<span data-ttu-id="0fa89-191">**項目の名前を指定** ダイアログ ボックスに、入力*へようこそ*、順にクリックします**OK**します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-191">In the **Specify Name for Item** dialog box, enter *Welcome*, and then click **OK**.</span></span>   
  
<span data-ttu-id="0fa89-192">**レイアウト ページの選択**ダイアログ ボックスで、既定値をそのまま使用 **\_Layout.cshtml**  をクリック**OK**。</span><span class="sxs-lookup"><span data-stu-id="0fa89-192">In the **Select a Layout Page** dialog, accept the default **\_Layout.cshtml** and click **OK**.</span></span>  
  
![](adding-a-view/_static/image11.png)   

<span data-ttu-id="0fa89-193">*MvcMovie\Views\HelloWorld\Welcome.cshtml*ファイルが作成されます。</span><span class="sxs-lookup"><span data-stu-id="0fa89-193">The *MvcMovie\Views\HelloWorld\Welcome.cshtml* file is created.</span></span>

<span data-ttu-id="0fa89-194">内のマークアップを置き換える、 *Welcome.cshtml*ファイル。</span><span class="sxs-lookup"><span data-stu-id="0fa89-194">Replace the markup in the *Welcome.cshtml* file.</span></span> <span data-ttu-id="0fa89-195">というループを作成します&quot;こんにちは&quot;回数だけ、ユーザーの質問にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0fa89-195">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="0fa89-196">完全な*Welcome.cshtml*ファイルを次に示します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-196">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

<span data-ttu-id="0fa89-197">アプリケーションを実行して、次の URL を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0fa89-197">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="0fa89-198">データは URL から取得され、コント ローラーを使用して、渡されるようになりました、[モデル バインダー](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-198">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="0fa89-199">コント ローラーにデータをパッケージ化、`ViewBag`オブジェクトと、ビューにオブジェクトを渡します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-199">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="0fa89-200">ビューはし、ユーザーに、HTML としてデータを表示します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-200">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="0fa89-201">上記のサンプルで使用して、`ViewBag`コント ローラーからビューにデータを渡すオブジェクト。</span><span class="sxs-lookup"><span data-stu-id="0fa89-201">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="0fa89-202">チュートリアルの後半で、ビュー モデルを使用して、コントローラーからビューにデータを渡します。</span><span class="sxs-lookup"><span data-stu-id="0fa89-202">Later in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="0fa89-203">ビュー モデル アプローチは、データを渡すことは、ビュー バッグのアプローチで一般的に推奨です。</span><span class="sxs-lookup"><span data-stu-id="0fa89-203">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="0fa89-204">ブログ記事を参照してください。[動的 V 厳密に型指定されたビュー](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="0fa89-204">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span> 

<span data-ttu-id="0fa89-205">一種の&quot;M&quot;モデルがデータベースの種類ではありません。</span><span class="sxs-lookup"><span data-stu-id="0fa89-205">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="0fa89-206">学習したことを確認し、ムービーのデータベースを作成してみましょう。</span><span class="sxs-lookup"><span data-stu-id="0fa89-206">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0fa89-207">[前へ](adding-a-controller.md)
> [次へ](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="0fa89-207">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>