---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: ビューマスターページにデータを渡す (VB) |Microsoft Docs
author: microsoft
description: このチュートリアルの目的は、コントローラーからビューマスターページにデータを渡す方法について説明することです。 ビュー m にデータを渡す2つの方法を検討しています...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593709"
---
# <a name="passing-data-to-view-master-pages-vb"></a>ビュー マスター ページにデータを渡す (VB)

[Microsoft](https://github.com/microsoft)

[PDF のダウンロード](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> このチュートリアルの目的は、コントローラーからビューマスターページにデータを渡す方法について説明することです。 ビューマスターページにデータを渡す2つの方法を検討します。 まず、管理が困難なアプリケーションを生成する簡単なソリューションについて説明します。 次に、より多くの初期作業を必要とする、より優れたソリューションを確認しますが、結果として、保守しやすいアプリケーションが得られます。

## <a name="passing-data-to-view-master-pages"></a>ビューマスターページにデータを渡す

このチュートリアルの目的は、コントローラーからビューマスターページにデータを渡す方法について説明することです。 ビューマスターページにデータを渡す2つの方法を検討します。 まず、管理が困難なアプリケーションを生成する簡単なソリューションについて説明します。 次に、より多くの初期作業を必要とする、より優れたソリューションを確認しますが、結果として、保守しやすいアプリケーションが得られます。

### <a name="the-problem"></a>問題を

たとえば、ムービーデータベースアプリケーションを構築しているときに、アプリケーションのすべてのページにムービーカテゴリの一覧を表示したいとします (図1を参照)。 さらに、ムービーカテゴリのリストがデータベーステーブルに格納されているとします。 そのような場合は、データベースからカテゴリを取得し、ムービーカテゴリのリストをビューマスターページ内に表示するのが理にかなっています。

[ビューマスターページでのムービーカテゴリの表示 ![](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**図 01**: ビューマスターページでのムービーカテゴリの表示 ([クリックすると、フルサイズの画像が表示](passing-data-to-view-master-pages-vb/_static/image3.png)される)

ここで問題が発生します。 マスターページでムービーカテゴリの一覧を取得するにはどうすればよいですか。 マスターページでモデルクラスのメソッドを直接呼び出すことが魅力的です。 つまり、マスターページ内のデータベースからデータを取得するためのコードを含めることをお勧めします。 ただし、MVC コントローラーをバイパスしてデータベースにアクセスすると、MVC アプリケーションを構築する主な利点の1つである問題の明確な分離に違反することになります。

Mvc アプリケーションでは、mvc ビューと mvc モデル間のすべての対話を MVC コントローラーで処理する必要があります。 このような問題を分離することにより、保守性が高く、適応性があり、テストが容易なアプリケーションになります。

MVC アプリケーションでは、ビューに渡されるすべてのデータ (ビューマスターページを含む) は、コントローラーアクションによってビューに渡される必要があります。 さらに、データはビューデータを利用して渡す必要があります。 このチュートリアルの残りの部分では、ビューマスターページにビューデータを渡す2つの方法を確認します。

### <a name="the-simple-solution"></a>単純なソリューション

まず、コントローラーからビューマスターページにビューデータを渡す最も単純なソリューションを見てみましょう。 最も簡単な解決策は、各コントローラーアクションのマスターページのビューデータを渡すことです。

リスト1のコントローラーについて考えてみましょう。 `Index()` と `Details()`という名前の2つのアクションを公開します。 `Index()` アクションメソッドは、ムービーデータベーステーブル内のすべてのムービーを返します。 `Details()` アクションメソッドは、特定のムービーカテゴリに含まれるすべてのムービーを返します。

**リスト1– `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

`Index()` と `Details()` の操作の両方で、データを表示するための2つの項目が追加されていることに注意してください。 `Index()` アクションでは、カテゴリと映画の2つのキーが追加されます。 Categories キーは、ビューマスターページに表示されるムービーカテゴリの一覧を表します。 ムービーキーは、インデックスビューページに表示されるムービーの一覧を表します。

`Details()` アクションでは、カテゴリと映画という名前の2つのキーも追加されます。 もう一度カテゴリキーは、ビューマスターページに表示されるムービーカテゴリの一覧を表します。 ムービーキーは、[詳細ビュー] ページに表示される特定のカテゴリの映画の一覧を表します (図2を参照)。

[詳細ビューの ![](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**図 02**: 詳細ビュー ([クリックすると、フルサイズの画像が表示](passing-data-to-view-master-pages-vb/_static/image6.png)されます)

インデックスビューは、リスト2に含まれています。 単に、[データの表示] の映画項目で表されるムービーの一覧を反復処理します。

**リスト2– `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

ビューマスターページは、リスト3に含まれています。 ビューマスターページでは、カテゴリアイテムによって表されるすべてのムービーカテゴリが、ビューデータから反復処理され、レンダリングされます。

**リスト3– `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

すべてのデータは、ビューデータを通じてビューおよびビューマスターページに渡されます。 これは、マスターページにデータを渡す正しい方法です。

では、このソリューションにはどのような問題があるのでしょうか。 問題は、このソリューションがドライ (DRY 原則) の原則に違反していることです。 各コントローラーアクションは、データを表示するために、同じムービーカテゴリのリストを追加する必要があります。 アプリケーションのコードが重複していると、アプリケーションの保守、調整、および変更がはるかに困難になります。

### <a name="the-good-solution"></a>優れたソリューション

このセクションでは、コントローラーアクションからビューマスターページにデータを渡す方法について、別の方法を検討しています。 各コントローラーアクションのマスターページのムービーカテゴリを追加するのではなく、ムービーカテゴリをビューデータに1回だけ追加します。 ビューマスターページで使用されるすべてのビューデータは、アプリケーションコントローラーに追加されます。

ApplicationController クラスは、リスト4に含まれています。

ApplicationController クラスは、リスト4に含まれています。

**リスト4– `Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

リスト4のアプリケーションコントローラーに関しては、次の3つの点に注意する必要があります。 最初に、クラスは基本の System.web. Mvc. Controller クラスから継承されていることに注意してください。 アプリケーションコントローラーは、コントローラークラスです。

次に、Application controller クラスが MustInherit クラスであることに注意してください。 MustInherit クラスは、具象クラスによって実装される必要があるクラスです。 アプリケーションコントローラーは MustInherit クラスであるため、クラスで定義されているメソッドを直接呼び出すことはできません。 アプリケーションクラスを直接呼び出そうとすると、"リソースが見つかりません" というエラーメッセージが表示されます。

3番目の方法として、アプリケーションコントローラーには、データを表示するためのムービーカテゴリの一覧を追加するコンストラクターが含まれていることに注意してください。 アプリケーションコントローラーから継承されるすべてのコントローラークラスは、アプリケーションコントローラーのコンストラクターを自動的に呼び出します。 アプリケーションコントローラーから継承する任意のコントローラーで任意のアクションを呼び出すと、ムービーカテゴリが自動的にビューデータに含まれます。

リスト5のムービーコントローラーは、アプリケーションコントローラーから継承されます。

**リスト5– `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

ムービーコントローラーは、前のセクションで説明した Home コントローラーと同様に、`Index()` と `Details()`という名前の2つのアクションメソッドを公開しています。 ビューマスターページに表示されるムービーカテゴリの一覧は、`Index()` または `Details()` のいずれの方法でもデータを表示するために追加されていないことに注意してください。 ムービーコントローラーはアプリケーションコントローラーから継承するため、ムービーカテゴリの一覧が追加され、データが自動的に表示されます。

ビューマスターページのビューデータを追加するこのソリューションは、ドライ (DRY 原則) の原則に違反していないことに注意してください。 データを表示するためのムービーカテゴリのリストを追加するためのコードは、アプリケーションコントローラーのコンストラクターという1つの場所にのみ含まれています。

### <a name="summary"></a>要約

このチュートリアルでは、コントローラーからビューマスターページにビューデータを渡す2つの方法について説明しました。 まず、単純な方法を検討しましたが、アプローチを維持するのは困難です。 最初のセクションでは、アプリケーションの各コントローラーアクションでビューマスターページのビューデータを追加する方法について説明しました。 ドライ (DRY 原則) の原則に違反しているため、これは不適切なアプローチでした。

次に、ビューマスターページでデータを表示するために必要なデータを追加するための、はるかに優れた方法を検討します。 各コントローラーアクションにビューデータを追加するのではなく、アプリケーションコントローラー内に1回だけビューデータを追加しました。 このようにして、ASP.NET MVC アプリケーションのビューマスターページにデータを渡すときにコードが重複しないようにすることができます。

> [!div class="step-by-step"]
> [前へ](creating-page-layouts-with-view-master-pages-vb.md)
