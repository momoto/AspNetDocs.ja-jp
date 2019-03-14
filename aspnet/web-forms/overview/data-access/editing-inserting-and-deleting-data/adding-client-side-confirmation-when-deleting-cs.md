---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: (C#) を削除するときに、クライアント側の確認を追加する |Microsoft Docs
author: rick-anderson
description: これまでに作成したインターフェイスで、ユーザーは編集ボタンをクリックするためのものと削除 ボタンをクリックしてデータを誤って削除できます。 この t.
ms.author: riande
ms.date: 07/17/2006
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: b8cca6ece2eb008170192dc1774a6f88c1b37a21
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034829"
---
<a name="adding-client-side-confirmation-when-deleting-c"></a><span data-ttu-id="1212d-104">削除時、クライアント側の確認を追加する (C#)</span><span class="sxs-lookup"><span data-stu-id="1212d-104">Adding Client-Side Confirmation When Deleting (C#)</span></span>
====================
<span data-ttu-id="1212d-105">によって[Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="1212d-105">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="1212d-106">[サンプル アプリをダウンロード](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe)または[PDF のダウンロード](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)</span><span class="sxs-lookup"><span data-stu-id="1212d-106">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe) or [Download PDF](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)</span></span>

> <span data-ttu-id="1212d-107">これまでに作成したインターフェイスで、ユーザーは編集ボタンをクリックするためのものと削除 ボタンをクリックしてデータを誤って削除できます。</span><span class="sxs-lookup"><span data-stu-id="1212d-107">In the interfaces we've created so far, a user can accidentally delete data by clicking the Delete button when they meant to click the Edit button.</span></span> <span data-ttu-id="1212d-108">このチュートリアルでは、Delete ボタンがクリックされたときに表示されるクライアント側の確認 ダイアログ ボックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="1212d-108">In this tutorial we'll add a client-side confirmation dialog box that appears when the Delete button is clicked.</span></span>


## <a name="introduction"></a><span data-ttu-id="1212d-109">はじめに</span><span class="sxs-lookup"><span data-stu-id="1212d-109">Introduction</span></span>

<span data-ttu-id="1212d-110">過去のいくつかのチュートリアルで ve 連携して、挿入、編集、および削除機能を提供する、アプリケーションのアーキテクチャ、ObjectDataSource、およびデータ Web コントロールを使用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="1212d-110">Over the past several tutorials we ve seen how to use our application architecture, ObjectDataSource, and the data Web controls in concert to provide inserting, editing, and deleting capabilities.</span></span> <span data-ttu-id="1212d-111">確認したらインターフェイスを削除するきませんでしたが、削除で構成されたクリックされたときに、ポストバックが発生する ObjectDataSource s を呼び出すボタンであり、`Delete()`メソッド。</span><span class="sxs-lookup"><span data-stu-id="1212d-111">The deleting interfaces we ve examined thus far have been composed of a Delete button that, when clicked, causes a postback and invokes the ObjectDataSource s `Delete()` method.</span></span> <span data-ttu-id="1212d-112">`Delete()`メソッドは、実際の発行、データ アクセス層に呼び出しを伝達するビジネス ロジック層から構成されているメソッドを呼び出します`DELETE`ステートメントはデータベースにします。</span><span class="sxs-lookup"><span data-stu-id="1212d-112">The `Delete()` method then invokes the configured method from the Business Logic Layer, which propagates the call down to the Data Access Layer, issuing the actual `DELETE` statement to the database.</span></span>

<span data-ttu-id="1212d-113">このユーザー インターフェイスでは、訪問者を GridView、DetailsView、または FormView コントロールを使用してレコードを削除することが、その削除 ボタンをクリックすると、何らかの確認が不足しています。</span><span class="sxs-lookup"><span data-stu-id="1212d-113">While this user interface enables visitors to delete records through the GridView, DetailsView, or FormView controls, it lacks any sort of confirmation when the user clicks the Delete button.</span></span> <span data-ttu-id="1212d-114">ユーザーが誤ってクリックした場合 をクリックするもので、ときに、削除 ボタンの編集、レコードを更新するためのものがインストールされます。 代わりにします。</span><span class="sxs-lookup"><span data-stu-id="1212d-114">If a user accidentally clicks the Delete button when they meant to click Edit, the record they meant to update will instead be deleted.</span></span> <span data-ttu-id="1212d-115">このチュートリアルでは、これを防ぐため、削除ボタンがクリックされたときに表示されるクライアント側の確認 ダイアログ ボックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="1212d-115">To help prevent this, in this tutorial we'll add a client-side confirmation dialog box that appears when the Delete button is clicked.</span></span>

<span data-ttu-id="1212d-116">JavaScript`confirm(string)`関数は、[ok] の 2 つのボタンに搭載されていて、(図 1 参照) をキャンセルするモーダル ダイアログ ボックス内のテキストとして、文字列入力パラメーターを表示します。</span><span class="sxs-lookup"><span data-stu-id="1212d-116">The JavaScript `confirm(string)` function displays its string input parameter as the text inside a modal dialog box that comes equipped with two buttons - OK and Cancel (see Figure 1).</span></span> <span data-ttu-id="1212d-117">`confirm(string)`関数によってどのようなボタンがクリックされたブール値を返します (`true`、ユーザーが [ok] をクリックすると、および`false`[キャンセル] をクリックした場合)。</span><span class="sxs-lookup"><span data-stu-id="1212d-117">The `confirm(string)` function returns a Boolean value depending on what button is clicked (`true`, if the user clicks OK, and `false` if they click Cancel).</span></span>


![JavaScript confirm(string) メソッドは、モーダルのクライアント側のメッセージ ボックスを表示します](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

<span data-ttu-id="1212d-119">**図 1**:JavaScript`confirm(string)`メソッドは、クライアント側のモーダルのメッセージ ボックスを表示します。</span><span class="sxs-lookup"><span data-stu-id="1212d-119">**Figure 1**: The JavaScript `confirm(string)` Method Displays a Modal, Client-Side Messagebox</span></span>


<span data-ttu-id="1212d-120">値の場合、フォームの送信中に`false`が、フォームの送信をキャンセルし、クライアント側のイベント ハンドラーから返されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-120">During a form submission, if a value of `false` is returned from a client-side event handler then the form submission is cancelled.</span></span> <span data-ttu-id="1212d-121">この機能を使用する場合は、この削除ボタン s のクライアント側ができる`onclick`イベント ハンドラーの呼び出しの値を返す`confirm("Are you sure you want to delete this product?")`します。</span><span class="sxs-lookup"><span data-stu-id="1212d-121">Using this feature, we can have the Delete button s client-side `onclick` event handler return the value of a call to `confirm("Are you sure you want to delete this product?")`.</span></span> <span data-ttu-id="1212d-122">ユーザーが [キャンセル] をクリックすると`confirm(string)`原因と、フォームの送信をキャンセルするため、false が返されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-122">If the user clicks Cancel, `confirm(string)` will return false, thereby causing the form submission to cancel.</span></span> <span data-ttu-id="1212d-123">ポストバックと t を受注の Delete ボタンがクリックされた製品が削除されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-123">With no postback, the product whose Delete button was clicked won t be deleted.</span></span> <span data-ttu-id="1212d-124">ただし、ユーザーは確認のダイアログ ボックスで [ok] をクリックすると場合、は、ポストバックがに伴って続行され、製品が削除されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-124">If, however, the user clicks OK in the confirmation dialog box, the postback will continue unabated and the product will be deleted.</span></span> <span data-ttu-id="1212d-125">参照してください[を使用して JavaScript s`confirm()`フォームの送信を制御するメソッド](http://www.webreference.com/programming/javascript/confirm/)この手法の詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="1212d-125">Consult [Using JavaScript s `confirm()` Method to Control Form Submission](http://www.webreference.com/programming/javascript/confirm/) for more information on this technique.</span></span>

<span data-ttu-id="1212d-126">必要なクライアント側スクリプトを追加することが若干を [commandfield] を使用するときのテンプレートを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="1212d-126">Adding the necessary client-side script differs slightly if using templates than when using a CommandField.</span></span> <span data-ttu-id="1212d-127">そのため、このチュートリアルでは、FormView や GridView の両方の例を見ていますが。</span><span class="sxs-lookup"><span data-stu-id="1212d-127">Therefore, in this tutorial we will look at both a FormView and GridView example.</span></span>

> [!NOTE]
> <span data-ttu-id="1212d-128">クライアント側の確認方法を使用して、このチュートリアルで説明しているようで、ユーザーが JavaScript をサポートするブラウザーでアクセスしているし、JavaScript が有効であること。</span><span class="sxs-lookup"><span data-stu-id="1212d-128">Using client-side confirmation techniques, like the ones discussed in this tutorial, assumes that your users are visiting with browsers that support JavaScript and that they have JavaScript enabled.</span></span> <span data-ttu-id="1212d-129">特定のユーザーの場合は true。 これらの前提条件のいずれかの場合は、削除ボタンをクリックするとはすぐがポストバックを (確認メッセージ ボックスが表示されない)。</span><span class="sxs-lookup"><span data-stu-id="1212d-129">If either of these assumptions are not true for a particular user, clicking the Delete button will immediately cause a postback (not displaying a confirm messagebox).</span></span>


## <a name="step-1-creating-a-formview-that-supports-deletion"></a><span data-ttu-id="1212d-130">手順 1: 削除をサポートする、フォーム ビューの作成</span><span class="sxs-lookup"><span data-stu-id="1212d-130">Step 1: Creating a FormView That Supports Deletion</span></span>

<span data-ttu-id="1212d-131">フォーム ビューを追加して、開始、`ConfirmationOnDelete.aspx`ページで、`EditInsertDelete`フォルダー、バックアップを使用して製品情報をプルする新しい ObjectDataSource にバインドすること、`ProductsBLL`クラスの`GetProducts()`メソッド。</span><span class="sxs-lookup"><span data-stu-id="1212d-131">Start by adding a FormView to the `ConfirmationOnDelete.aspx` page in the `EditInsertDelete` folder, binding it to a new ObjectDataSource that pulls back the product information via the `ProductsBLL` class s `GetProducts()` method.</span></span> <span data-ttu-id="1212d-132">ObjectDataSource をまた構成ように、`ProductsBLL`クラス s `DeleteProduct(productID)` ObjectDataSource s メソッドにマップされて`Delete()`メソッド; INSERT および UPDATE のタブのドロップダウン リストが (None) に設定されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="1212d-132">Also configure the ObjectDataSource so that the `ProductsBLL` class s `DeleteProduct(productID)` method is mapped to the ObjectDataSource s `Delete()` method; ensure that the INSERT and UPDATE tabs drop-down lists are set to (None).</span></span> <span data-ttu-id="1212d-133">最後に、FormView s のスマート タグでページングを有効にするチェック ボックスを確認します。</span><span class="sxs-lookup"><span data-stu-id="1212d-133">Finally, check the Enable Paging checkbox in the FormView s smart tag.</span></span>

<span data-ttu-id="1212d-134">これらの手順の後は、新しい ObjectDataSource s の宣言型マークアップは、次のようになります。</span><span class="sxs-lookup"><span data-stu-id="1212d-134">After these steps, the new ObjectDataSource s declarative markup will look like the following:</span></span>


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

<span data-ttu-id="1212d-135">オプティミスティック同時実行制御を使用していない、過去例のように少し ObjectDataSource s をクリアするため`OldValuesParameterFormatString`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="1212d-135">As in our past examples that did not use optimistic concurrency, take a moment to clear out the ObjectDataSource s `OldValuesParameterFormatString` property.</span></span>

<span data-ttu-id="1212d-136">削除、FormView s のみをサポートする ObjectDataSource コントロールにバインドされているため`ItemTemplate`のみの削除 ボタン、新機能と更新プログラムのボタンのないを提供します。</span><span class="sxs-lookup"><span data-stu-id="1212d-136">Since it has been bound to an ObjectDataSource control that only supports deleting, the FormView s `ItemTemplate` offers only the Delete button, lacking the New and Update buttons.</span></span> <span data-ttu-id="1212d-137">ただし、FormView s の宣言型マークアップが、余分な含まれ`EditItemTemplate`と`InsertItemTemplate`、これを削除することができます。</span><span class="sxs-lookup"><span data-stu-id="1212d-137">The FormView s declarative markup, however, includes a superfluous `EditItemTemplate` and `InsertItemTemplate`, which can be removed.</span></span> <span data-ttu-id="1212d-138">カスタマイズする少し、`ItemTemplate`ができるので、製品のサブセットのみのデータ フィールドを示しています。</span><span class="sxs-lookup"><span data-stu-id="1212d-138">Take a moment to customize the `ItemTemplate` so that is shows only a subset of the product data fields.</span></span> <span data-ttu-id="1212d-139">私で製品の名前を表示するように構成 ve、 `<h3>` (削除) と共にその業者とカテゴリ名の上の見出しです。</span><span class="sxs-lookup"><span data-stu-id="1212d-139">I ve configured mine to show the product s name in an `<h3>` heading above its supplier and category names (along with the Delete button).</span></span>


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

<span data-ttu-id="1212d-140">これらの変更は、ユーザーを削除 ボタンをクリックするだけで、製品を削除することができます、一度に 1 つの製品を通じて切り替えるできる web ページを完全に機能があります。</span><span class="sxs-lookup"><span data-stu-id="1212d-140">With these changes, we have a fully functional web page that allows a user to toggle through the products one at a time, with the ability to delete a product by simply clicking the Delete button.</span></span> <span data-ttu-id="1212d-141">図 2 は、ブラウザーで表示したときにこれまで、進行状況のスクリーン ショットを示します。</span><span class="sxs-lookup"><span data-stu-id="1212d-141">Figure 2 shows a screen shot of our progress thus far when viewed through a browser.</span></span>


<span data-ttu-id="1212d-142">[![FormView には、1 つの製品についての情報が表示されます。](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="1212d-142">[![The FormView Shows Information About a Single Product](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)</span></span>

<span data-ttu-id="1212d-143">**図 2**:FormView 表示情報について、1 つの製品 ([フルサイズの画像を表示する をクリックします](adding-client-side-confirmation-when-deleting-cs/_static/image4.png))。</span><span class="sxs-lookup"><span data-stu-id="1212d-143">**Figure 2**: The FormView Shows Information About a Single Product ([Click to view full-size image](adding-client-side-confirmation-when-deleting-cs/_static/image4.png))</span></span>


## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a><span data-ttu-id="1212d-144">手順 2: 削除ボタン クライアント側の onclick イベントから confirm(string) 関数を呼び出す</span><span class="sxs-lookup"><span data-stu-id="1212d-144">Step 2: Calling the confirm(string) Function from the Delete Buttons Client-Side onclick Event</span></span>

<span data-ttu-id="1212d-145">最後の手順は、FormView を作成すると、このような削除ボタンを構成するときに、s が、JavaScript、訪問者によってクリックされた`confirm(string)`関数が呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-145">With the FormView created, the final step is to configure the Delete button such that when it s clicked by the visitor, the JavaScript `confirm(string)` function is invoked.</span></span> <span data-ttu-id="1212d-146">ボタンや LinkButton、ImageButton のクライアント側へのクライアント側スクリプトの追加`onclick`イベントの使用により実現できます、 `OnClientClick property`、これは ASP.NET 2.0 に新しいします。</span><span class="sxs-lookup"><span data-stu-id="1212d-146">Adding client-side script to a Button, LinkButton, or ImageButton s client-side `onclick` event can be accomplished through the use of the `OnClientClick property`, which is new to ASP.NET 2.0.</span></span> <span data-ttu-id="1212d-147">値が必要なため、`confirm(string)`このプロパティを設定する関数が返されるだけです。 `return confirm('Are you certain that you want to delete this product?');`</span><span class="sxs-lookup"><span data-stu-id="1212d-147">Since we want to have the value of the `confirm(string)` function returned, simply set this property to: `return confirm('Are you certain that you want to delete this product?');`</span></span>

<span data-ttu-id="1212d-148">この変更後に削除 LinkButton s の宣言型構文ようになります。</span><span class="sxs-lookup"><span data-stu-id="1212d-148">After this change the Delete LinkButton s declarative syntax should look something like:</span></span>


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

<span data-ttu-id="1212d-149">すべてが s で終了です。</span><span class="sxs-lookup"><span data-stu-id="1212d-149">That s all there is to it!</span></span> <span data-ttu-id="1212d-150">図 3 は、アクションでこの確認のスクリーン ショットを示します。</span><span class="sxs-lookup"><span data-stu-id="1212d-150">Figure 3 shows a screen shot of this confirmation in action.</span></span> <span data-ttu-id="1212d-151">削除ボタンをクリックすると、[確認] ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-151">Clicking the Delete button brings up the confirm dialog box.</span></span> <span data-ttu-id="1212d-152">ユーザーは、[キャンセル] をクリックすると、ポストバックがキャンセルされ、製品は削除されません。</span><span class="sxs-lookup"><span data-stu-id="1212d-152">If the user clicks Cancel, the postback is cancelled and the product is not deleted.</span></span> <span data-ttu-id="1212d-153">ポストバックの継続のかどうか、ただし、ユーザーは、[ok] をクリックして、および ObjectDataSource の`Delete()`メソッドが呼び出される、データベースのレコードを削除中に使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-153">If, however, the user clicks OK, the postback continues and the ObjectDataSource s `Delete()` method is invoked, culminating in the database record being deleted.</span></span>

> [!NOTE]
> <span data-ttu-id="1212d-154">渡された文字列、 `confirm(string)` JavaScript 関数は、アポストロフィ (引用符ではなく) で区切られます。</span><span class="sxs-lookup"><span data-stu-id="1212d-154">The string passed into the `confirm(string)` JavaScript function is delimited with apostrophes (rather than quotation marks).</span></span> <span data-ttu-id="1212d-155">JavaScript ではいずれかの文字を使用して文字列を区切ることができます。</span><span class="sxs-lookup"><span data-stu-id="1212d-155">In JavaScript, strings can be delimited using either character.</span></span> <span data-ttu-id="1212d-156">渡された文字列の区切り記号のようにアポストロフィここで使用`confirm(string)`を使用する区切り記号では、あいまいさを持ち込んでいない、`OnClientClick`プロパティの値。</span><span class="sxs-lookup"><span data-stu-id="1212d-156">We use apostrophes here so that the delimiters for the string passed into `confirm(string)` do not introduce an ambiguity with the delimiters used for the `OnClientClick` property value.</span></span>


<span data-ttu-id="1212d-157">[![確認メッセージは、今すぐ表示と削除 ボタンをクリックして](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1212d-157">[![A Confirmation is Now Displayed When Clicking the Delete Button](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)</span></span>

<span data-ttu-id="1212d-158">**図 3**:確認メッセージは、今すぐ表示と削除 ボタンをクリックして ([フルサイズの画像を表示する をクリックします](adding-client-side-confirmation-when-deleting-cs/_static/image7.png))。</span><span class="sxs-lookup"><span data-stu-id="1212d-158">**Figure 3**: A Confirmation is Now Displayed When Clicking the Delete Button ([Click to view full-size image](adding-client-side-confirmation-when-deleting-cs/_static/image7.png))</span></span>


## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a><span data-ttu-id="1212d-159">手順 3: [Commandfield]、[削除] ボタンの OnClientClick プロパティを構成します。</span><span class="sxs-lookup"><span data-stu-id="1212d-159">Step 3: Configuring the OnClientClick Property for the Delete Button in a CommandField</span></span>

<span data-ttu-id="1212d-160">確認のダイアログ ボックスを構成するだけでそれに関連付けられたすることができます、テンプレートで直接、ボタン、LinkButton、ImageButton に作業するとき、 `OnClientClick` 、JavaScript の結果を返すプロパティ`confirm(string)`関数。</span><span class="sxs-lookup"><span data-stu-id="1212d-160">When working with a Button, LinkButton, or ImageButton directly in a template, a confirmation dialog box can be associated with it by simply configuring its `OnClientClick` property to return the results of the JavaScript `confirm(string)` function.</span></span> <span data-ttu-id="1212d-161">ただし、フィールドの削除 ボタンを追加すると、GridView、DetailsView - が commandfield はありません、`OnClientClick`宣言によって設定できるプロパティです。</span><span class="sxs-lookup"><span data-stu-id="1212d-161">However, the CommandField - which adds a field of Delete buttons to a GridView or DetailsView - does not have an `OnClientClick` property that can be set declaratively.</span></span> <span data-ttu-id="1212d-162">代わりに、適切な GridView、DetailsView s に削除 ボタンを参照する必要がありますプログラムで`DataBound`イベント ハンドラー、および設定してその`OnClientClick`プロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="1212d-162">Instead, we must programmatically reference the Delete button in the GridView or DetailsView s appropriate `DataBound` event handler, and then set its `OnClientClick` property there.</span></span>

> [!NOTE]
> <span data-ttu-id="1212d-163">S [削除] ボタンを設定するときに`OnClientClick`プロパティで、適切な`DataBound`へのアクセスがあるイベント ハンドラーでは、データは、現在のレコードにバインドされました。</span><span class="sxs-lookup"><span data-stu-id="1212d-163">When setting the Delete button s `OnClientClick` property in the appropriate `DataBound` event handler, we have access to the data was bound to the current record.</span></span> <span data-ttu-id="1212d-164">つまり、「は Chai 製品を削除しますか?」など、特定のレコードの詳細を含めるに確認メッセージを拡張できます。</span><span class="sxs-lookup"><span data-stu-id="1212d-164">This means we can extend the confirmation message to include details about the particular record, such as, "Are you sure you want to delete the Chai product?"</span></span> <span data-ttu-id="1212d-165">このようなカスタマイズは、データ バインディング構文を使用してテンプレートのこともできます。</span><span class="sxs-lookup"><span data-stu-id="1212d-165">Such customization is also possible in templates using databinding syntax.</span></span>


<span data-ttu-id="1212d-166">実際に設定する、 `OnClientClick` CommandField、let s に削除ボタンのプロパティ ページに GridView を追加します。</span><span class="sxs-lookup"><span data-stu-id="1212d-166">To practice setting the `OnClientClick` property for the Delete button(s) in a CommandField, let s add a GridView to the page.</span></span> <span data-ttu-id="1212d-167">この GridView、FormView を使用する同じ ObjectDataSource コントロールの使用を構成します。</span><span class="sxs-lookup"><span data-stu-id="1212d-167">Configure this GridView to use the same ObjectDataSource control that the FormView uses.</span></span> <span data-ttu-id="1212d-168">GridView s のみ製品の名前、カテゴリ、および仕入先が含まれる BoundFields 制限もできます。</span><span class="sxs-lookup"><span data-stu-id="1212d-168">Also limit the GridView s BoundFields to only include the product s name, category, and supplier.</span></span> <span data-ttu-id="1212d-169">最後に、GridView s のスマート タグからの削除を有効にするチェック ボックスを確認します。</span><span class="sxs-lookup"><span data-stu-id="1212d-169">Lastly, check the Enable Deleting checkbox from the GridView s smart tag.</span></span> <span data-ttu-id="1212d-170">GridView s に、[commandfield] を追加します`Columns`コレクションとその`ShowDeleteButton`プロパティに設定`true`します。</span><span class="sxs-lookup"><span data-stu-id="1212d-170">This will add a CommandField to the GridView s `Columns` collection with its `ShowDeleteButton` property set to `true`.</span></span>

<span data-ttu-id="1212d-171">これらの変更を行った後、次のように GridView s の宣言型マークアップになります。</span><span class="sxs-lookup"><span data-stu-id="1212d-171">After making these changes, your GridView s declarative markup should look like the following:</span></span>


[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

<span data-ttu-id="1212d-172">[Commandfield] には、GridView s からプログラムでアクセスできる 1 つ削除 LinkButton のインスタンスが含まれています。`RowDataBound`イベント ハンドラー。</span><span class="sxs-lookup"><span data-stu-id="1212d-172">The CommandField contains a single Delete LinkButton instance that can be accessed programmatically from the GridView s `RowDataBound` event handler.</span></span> <span data-ttu-id="1212d-173">設定できる、参照とその`OnClientClick`プロパティに応じて。</span><span class="sxs-lookup"><span data-stu-id="1212d-173">Once referenced, we can set its `OnClientClick` property accordingly.</span></span> <span data-ttu-id="1212d-174">イベント ハンドラーを作成、`RowDataBound`を次のコードを使用してイベント。</span><span class="sxs-lookup"><span data-stu-id="1212d-174">Create an event handler for the `RowDataBound` event using the following code:</span></span>


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

<span data-ttu-id="1212d-175">このイベント ハンドラーは、データ行 (削除 ボタンを持つもの) と連携し、プログラムで、削除 ボタンを参照して開始します。</span><span class="sxs-lookup"><span data-stu-id="1212d-175">This event handler works with data rows (those that will have the Delete button) and begins by programmatically referencing the Delete button.</span></span> <span data-ttu-id="1212d-176">[全般] では、次のパターンを使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-176">In general use the following pattern:</span></span>


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

<span data-ttu-id="1212d-177">*ButtonType* [commandfield] のボタンや LinkButton、ImageButton によって使用されているボタンの種類です。</span><span class="sxs-lookup"><span data-stu-id="1212d-177">*ButtonType* is the type of button being used by the CommandField - Button, LinkButton, or ImageButton.</span></span> <span data-ttu-id="1212d-178">既定では、[commandfield] は、Linkbutton を使用してが、これは、[commandfield] s からカスタマイズできます`ButtonType property`します。</span><span class="sxs-lookup"><span data-stu-id="1212d-178">By default, the CommandField uses LinkButtons, but this can be customized via the CommandField s `ButtonType property`.</span></span> <span data-ttu-id="1212d-179">*CommandFieldIndex* GridView s 内で [commandfield] の序数インデックス`Columns`、コレクションは、 *controlIndex* [commandfield] s 内の Delete ボタンのインデックス`Controls`コレクション。</span><span class="sxs-lookup"><span data-stu-id="1212d-179">The *commandFieldIndex* is the ordinal index of the CommandField within the GridView s `Columns` collection, whereas the *controlIndex* is the index of the Delete button within the CommandField s `Controls` collection.</span></span> <span data-ttu-id="1212d-180">*ControlIndex*値は、[commandfield] でその他のボタンを基準としたボタン s の位置に依存します。</span><span class="sxs-lookup"><span data-stu-id="1212d-180">The *controlIndex* value depends on the button s position relative to other buttons in the CommandField.</span></span> <span data-ttu-id="1212d-181">たとえば、唯一のボタン、[commandfield] に表示されますが、削除ボタンの場合は、インデックスは 0 を使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-181">For example, if the only button displayed in the CommandField is the Delete button, use an index of 0.</span></span> <span data-ttu-id="1212d-182">かどうか、ただしが s 削除 ボタンの前の編集 ボタンを使用して、インデックスの 2。</span><span class="sxs-lookup"><span data-stu-id="1212d-182">If, however, there s an Edit button that precedes the Delete button, use an index of 2.</span></span> <span data-ttu-id="1212d-183">2 のインデックスを使用する理由は Delete ボタンの前に [commandfield] によって 2 つのコントロールが追加されたためです。 [編集] ボタンと LiteralControl s、編集、削除ボタンの間にスペースを追加するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-183">The reason an index of 2 is used is because two controls are added by the CommandField before the Delete button: the Edit button and a LiteralControl that s used to add some space between the Edit and Delete buttons.</span></span>

<span data-ttu-id="1212d-184">この特定の例で、[commandfield] Linkbutton を使用して、います、左端のフィールドを*commandFieldIndex*は 0。</span><span class="sxs-lookup"><span data-stu-id="1212d-184">For our particular example, the CommandField uses LinkButtons and, being the left-most field, has a *commandFieldIndex* of 0.</span></span> <span data-ttu-id="1212d-185">使用して他のボタンはありませんが、[commandfield] で [削除] ボタンがある、ので、 *controlIndex*は 0。</span><span class="sxs-lookup"><span data-stu-id="1212d-185">Since there are no other buttons but the Delete button in the CommandField, we use a *controlIndex* of 0.</span></span>

<span data-ttu-id="1212d-186">後、[commandfield] で [削除] ボタンを参照するには、次に GridView の現在の行にバインドされている製品についての情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="1212d-186">After referencing the Delete button in the CommandField, we next grab information about the product bound to the current GridView row.</span></span> <span data-ttu-id="1212d-187">最後に、秒の削除 ボタンを設定します`OnClientClick`プロパティを適切な JavaScript で製品の名前が含まれています。</span><span class="sxs-lookup"><span data-stu-id="1212d-187">Finally, we set the Delete button s `OnClientClick` property to the appropriate JavaScript, which includes the product s name.</span></span> <span data-ttu-id="1212d-188">JavaScript 文字列が渡されるため、`confirm(string)`関数は、アポストロフィ、s の製品名内に表示される任意のアポストロフィはエスケープする必要がありますを使用して区切られます。</span><span class="sxs-lookup"><span data-stu-id="1212d-188">Since the JavaScript string passed into the `confirm(string)` function is delimited using apostrophes we must escape any apostrophes that appear within the product s name.</span></span> <span data-ttu-id="1212d-189">S の製品名にアポストロフィをエスケープする具体的には、"`\'`"。</span><span class="sxs-lookup"><span data-stu-id="1212d-189">In particular, any apostrophes in the product s name are escaped with "`\'`".</span></span>

<span data-ttu-id="1212d-190">これらの変更は完全な GridView が表示されます (図 4 参照)、カスタマイズされた確認ダイアログ ボックスで [削除] ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="1212d-190">With these changes complete, clicking on a Delete button in the GridView displays a customized confirmation dialog box (see Figure 4).</span></span> <span data-ttu-id="1212d-191">として、FormView から確認メッセージ ボックスと、ユーザーが [キャンセル] をクリックした場合、ポストバックが取り消された場合、発生してから、削除できないようにすること。</span><span class="sxs-lookup"><span data-stu-id="1212d-191">As with the confirmation messagebox from the FormView, if the user clicks Cancel the postback is cancelled, thereby preventing the deletion from occurring.</span></span>

> [!NOTE]
> <span data-ttu-id="1212d-192">この手法が、DetailsView で [commandfield] で [削除] ボタンをプログラムでアクセスすることもできます。</span><span class="sxs-lookup"><span data-stu-id="1212d-192">This technique can also be used to programmatically access the Delete button in the CommandField in a DetailsView.</span></span> <span data-ttu-id="1212d-193">DetailsView、ただし、d を作成、イベント ハンドラーを`DataBound`DetailsView があるないため、イベント、`RowDataBound`イベント。</span><span class="sxs-lookup"><span data-stu-id="1212d-193">For the DetailsView, however, you d create an event handler for the `DataBound` event, since the DetailsView does not have a `RowDataBound` event.</span></span>


<span data-ttu-id="1212d-194">[![GridView の削除 ボタンをクリックすると、カスタマイズされた確認ダイアログ ボックスが表示されます。](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="1212d-194">[![Clicking the GridView s Delete Button Displays a Customized Confirmation Dialog Box](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)</span></span>

<span data-ttu-id="1212d-195">**図 4**:GridView の削除 ボタンをクリックするとカスタマイズの確認 ダイアログ ボックスが表示されます ([フルサイズの画像を表示する をクリックします](adding-client-side-confirmation-when-deleting-cs/_static/image10.png))。</span><span class="sxs-lookup"><span data-stu-id="1212d-195">**Figure 4**: Clicking the GridView s Delete Button Displays a Customized Confirmation Dialog Box ([Click to view full-size image](adding-client-side-confirmation-when-deleting-cs/_static/image10.png))</span></span>


## <a name="using-templatefields"></a><span data-ttu-id="1212d-196">TemplateFields を使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-196">Using TemplateFields</span></span>

<span data-ttu-id="1212d-197">[Commandfield] の欠点の 1 つは、そのボタンは、インデックスを通じてアクセスする必要があり、結果のオブジェクトは、適切なボタンの種類 (ボタンや LinkButton、ImageButton) にキャストする必要があります。</span><span class="sxs-lookup"><span data-stu-id="1212d-197">One of the disadvantages of the CommandField is that its buttons must be accessed through indexing and that the resulting object must be cast to the appropriate button type (Button, LinkButton, or ImageButton).</span></span> <span data-ttu-id="1212d-198">実行時まで検出できない問題への招待の「マジック ナンバー」およびハード コーディングされた型を使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-198">Using "magic numbers" and hard-coded types invites problems that cannot be discovered until runtime.</span></span> <span data-ttu-id="1212d-199">たとえば、または別の開発者は、いくつかの時点を将来 (Edit ボタン) などの変更で [commandfield] に新しいボタンを追加する場合、`ButtonType`プロパティ、既存のコードは、エラーを発生させずはコンパイルされますが、例外が発生する可能性があります、ページにアクセスまたは、コードの記述方法と、加えられた変更によって、予期しない動作します。</span><span class="sxs-lookup"><span data-stu-id="1212d-199">For example, if you, or another developer, adds new buttons to the CommandField at some point in the future (such as an Edit button) or changes the `ButtonType` property, the existing code will still compile without error, but visiting the page may cause an exception or unexpected behavior, depending on how your code was written and what changes were made.</span></span>

<span data-ttu-id="1212d-200">別のアプローチでは、TemplateFields GridView および DetailsView のコマンドに変換します。</span><span class="sxs-lookup"><span data-stu-id="1212d-200">An alternative approach is to convert the GridView and DetailsView s CommandFields into TemplateFields.</span></span> <span data-ttu-id="1212d-201">これを TemplateField が生成されます、 `ItemTemplate` LinkButton (またはボタンまたは ImageButton) を持つ各ボタン、[commandfield] にします。</span><span class="sxs-lookup"><span data-stu-id="1212d-201">This will generate a TemplateField with an `ItemTemplate` that has a LinkButton (or Button or ImageButton) for each button in the CommandField.</span></span> <span data-ttu-id="1212d-202">これらのボタン`OnClientClick`、フォーム ビューで表示した場合、または適切なプログラムでアクセスできるに、プロパティを宣言によって、割り当てられることができます`DataBound`イベント ハンドラーを次のパターンを使用します。</span><span class="sxs-lookup"><span data-stu-id="1212d-202">These buttons `OnClientClick` properties can be assigned declaratively, as we saw with the FormView, or can be programmatically accessed in the appropriate `DataBound` event handler using the following pattern:</span></span>


[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

<span data-ttu-id="1212d-203">場所*controlID*ボタン秒の値は、`ID`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="1212d-203">Where *controlID* is the value of the button s `ID` property.</span></span> <span data-ttu-id="1212d-204">このパターンには、キャストのハード コーディングされた型も必要ですが、削除、インデックス作成の必要性ランタイム エラーが発生せずに変更をレイアウトすることができます。</span><span class="sxs-lookup"><span data-stu-id="1212d-204">While this pattern still requires a hard-coded type for the cast, it removes the need for indexing, allowing for the layout to change without resulting in a runtime error.</span></span>

## <a name="summary"></a><span data-ttu-id="1212d-205">まとめ</span><span class="sxs-lookup"><span data-stu-id="1212d-205">Summary</span></span>

<span data-ttu-id="1212d-206">JavaScript`confirm(string)`関数は、フォームの送信を制御するための一般的に使用される手法です。</span><span class="sxs-lookup"><span data-stu-id="1212d-206">The JavaScript `confirm(string)` function is a commonly used technique for controlling form submission workflow.</span></span> <span data-ttu-id="1212d-207">実行すると、関数には、2 つのボタン、[ok] と [キャンセル] を含む、クライアント側のモーダル ダイアログ ボックスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="1212d-207">When executed, the function displays a modal, client-side dialog box that includes two buttons, OK and Cancel.</span></span> <span data-ttu-id="1212d-208">ユーザーが [ok] をクリックすると、`confirm(string)`関数が返される`true`; [キャンセル] をクリックすると戻ります`false`します。</span><span class="sxs-lookup"><span data-stu-id="1212d-208">If the user clicks OK, the `confirm(string)` function returns `true`; clicking Cancel returns `false`.</span></span> <span data-ttu-id="1212d-209">この機能は、送信処理中に、イベント ハンドラーによって返された場合は、フォームの送信をキャンセルするブラウザーの動作を組み合わせて`false`レコードを削除するときに、確認メッセージ ボックスを表示するために使用できます。</span><span class="sxs-lookup"><span data-stu-id="1212d-209">This functionality, coupled with a browser s behavior to cancel a form submission if an event handler during the submission process returns `false`, can be used to display a confirmation messagebox when deleting a record.</span></span>

<span data-ttu-id="1212d-210">`confirm(string)`関数は、ボタンの Web コントロール s のクライアント側を関連付けることにより`onclick`s コントロールを使用してイベント ハンドラー`OnClientClick`プロパティ。</span><span class="sxs-lookup"><span data-stu-id="1212d-210">The `confirm(string)` function can be associated with a Button Web control s client-side `onclick` event handler through the control s `OnClientClick` property.</span></span> <span data-ttu-id="1212d-211">テンプレート - または - GridView、DetailsView で TemplateField FormView のテンプレートのいずれかで [削除] ボタンを使用する場合このプロパティ宣言またはプログラムでは、このチュートリアルで説明したようにします。</span><span class="sxs-lookup"><span data-stu-id="1212d-211">When working with a Delete button in a template - either in one of the FormView s templates or in a TemplateField in the DetailsView or GridView - this property can be set either declaratively or programmatically, as we saw in this tutorial.</span></span>

<span data-ttu-id="1212d-212">満足のプログラミングです。</span><span class="sxs-lookup"><span data-stu-id="1212d-212">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="1212d-213">執筆者紹介</span><span class="sxs-lookup"><span data-stu-id="1212d-213">About the Author</span></span>

<span data-ttu-id="1212d-214">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)、7 つ受け取りますブックおよびの創設者の著者[4GuysFromRolla.com](http://www.4guysfromrolla.com)、Microsoft Web テクノロジと 1998 年から携わっています。</span><span class="sxs-lookup"><span data-stu-id="1212d-214">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="1212d-215">Scott は、フリーのコンサルタント、トレーナー、およびライターとして動作します。</span><span class="sxs-lookup"><span data-stu-id="1212d-215">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="1212d-216">最新の著書は[ *Sams 教える自分で ASP.NET 2.0 24 時間以内に*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)します。</span><span class="sxs-lookup"><span data-stu-id="1212d-216">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="1212d-217">彼に到達できる[mitchell@4GuysFromRolla.comします。](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="1212d-217">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span> <span data-ttu-id="1212d-218">彼のブログにあるでまたは[ http://ScottOnWriting.NET](http://ScottOnWriting.NET)します。</span><span class="sxs-lookup"><span data-stu-id="1212d-218">or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1212d-219">[前へ](implementing-optimistic-concurrency-cs.md)
> [次へ](limiting-data-modification-functionality-based-on-the-user-cs.md)</span><span class="sxs-lookup"><span data-stu-id="1212d-219">[Previous](implementing-optimistic-concurrency-cs.md)
[Next](limiting-data-modification-functionality-based-on-the-user-cs.md)</span></span>