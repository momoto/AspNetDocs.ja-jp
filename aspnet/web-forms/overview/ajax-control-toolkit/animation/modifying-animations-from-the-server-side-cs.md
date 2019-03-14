---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: サーバー側 (c#) からアニメーションを変更する |Microsoft Docs
author: wenz
description: アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。 アニメーションも可能性があります.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: ac2c2b1e9cfceba7f818f3f2dcbd719e94bea83e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57041429"
---
<a name="modifying-animations-from-the-server-side-c"></a><span data-ttu-id="1e8be-104">サーバー側 (c#) からアニメーションを変更します。</span><span class="sxs-lookup"><span data-stu-id="1e8be-104">Modifying Animations From The Server Side (C#)</span></span>
====================
<span data-ttu-id="1e8be-105">によって[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="1e8be-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="1e8be-106">[コードのダウンロード](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)または[PDF のダウンロード](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="1e8be-106">[Download Code](http://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) or [Download PDF](http://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span></span>

> <span data-ttu-id="1e8be-107">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="1e8be-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1e8be-108">サーバー側で、アニメーションを変更することも</span><span class="sxs-lookup"><span data-stu-id="1e8be-108">The animations may also be changed on the server-side</span></span>


## <a name="overview"></a><span data-ttu-id="1e8be-109">概要</span><span class="sxs-lookup"><span data-stu-id="1e8be-109">Overview</span></span>

<span data-ttu-id="1e8be-110">アニメーション コントロール、ASP.NET AJAX Control Toolkit ではなくコントロールだけをコントロールにアニメーションを追加するために全体のフレームワークです。</span><span class="sxs-lookup"><span data-stu-id="1e8be-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="1e8be-111">サーバー側で、アニメーションを変更することも</span><span class="sxs-lookup"><span data-stu-id="1e8be-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="1e8be-112">手順</span><span class="sxs-lookup"><span data-stu-id="1e8be-112">Steps</span></span>

<span data-ttu-id="1e8be-113">まず、含める、 `ScriptManager` ; ページで次に、ASP.NET AJAX ライブラリが読み込まれる Control Toolkit を使用すること。</span><span class="sxs-lookup"><span data-stu-id="1e8be-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

<span data-ttu-id="1e8be-114">次のようなテキストのパネルに、アニメーションが適用されます。</span><span class="sxs-lookup"><span data-stu-id="1e8be-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

<span data-ttu-id="1e8be-115">パネルの関連付けられている CSS クラス、便利な背景色を定義し、パネルの固定幅の設定も。</span><span class="sxs-lookup"><span data-stu-id="1e8be-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

<span data-ttu-id="1e8be-116">コードの残りの部分がサーバー側で実行され、マークアップ; は使用しません代わりに、作成するコードを使用、`AnimationExtender`コントロール。</span><span class="sxs-lookup"><span data-stu-id="1e8be-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

<span data-ttu-id="1e8be-117">ただし、Control Toolkit 現在アクセスことはできません、API を個別にアニメーションを作成します。</span><span class="sxs-lookup"><span data-stu-id="1e8be-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="1e8be-118">ただしを設定すること、`AnimationExtender`アニメーションを宣言的に割り当てるときに使用する XML マークアップを含む文字列へのアニメーション プロパティ。</span><span class="sxs-lookup"><span data-stu-id="1e8be-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="1e8be-119">含めることはできませんが、XML を作成するには、 `<Animations>` .NET Framework の XML を使用する可能性があります要素は、サポートまたは、次のコードのように、文字列を指定だけです。</span><span class="sxs-lookup"><span data-stu-id="1e8be-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

<span data-ttu-id="1e8be-120">最後に、追加、`AnimationExtender`内で現在のページにコントロール、`<form runat="server">`要素、アニメーションが含まれており、実行されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1e8be-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]


<span data-ttu-id="1e8be-121">[![サーバー側の C #/vb のコードを使用してアニメーションの作成します。](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1e8be-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span></span>

<span data-ttu-id="1e8be-122">サーバー側の C #/vb のコードを使用してアニメーションの作成 ([フルサイズの画像を表示する をクリックします](modifying-animations-from-the-server-side-cs/_static/image3.png))。</span><span class="sxs-lookup"><span data-stu-id="1e8be-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e8be-123">[前へ](triggering-an-animation-in-another-control-cs.md)
> [次へ](executing-animations-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1e8be-123">[Previous](triggering-an-animation-in-another-control-cs.md)
[Next](executing-animations-using-client-side-code-cs.md)</span></span>