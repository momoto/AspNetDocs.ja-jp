---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-vb
title: データベースの開発と展開 (VB) の戦略 |Microsoft Docs
author: rick-anderson
description: 最初に、データ駆動型アプリケーションをデプロイするときに、開発環境を運用環境で無条件、データベースをコピーできます。 B..
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 07b8905d-78ac-4252-97fb-8675b3fb0bbf
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/strategies-for-database-development-and-deployment-vb
msc.type: authoredcontent
ms.openlocfilehash: e07da4b5263ac3c6db19c375ca00cbcf87e0b35a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042179"
---
<a name="strategies-for-database-development-and-deployment-vb"></a>データベースの開発と配置のための戦略 (VB)
====================
によって[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF のダウンロード](http://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial10_DBDevel_vb.pdf)

> 最初に、データ駆動型アプリケーションをデプロイするときに、開発環境を運用環境で無条件、データベースをコピーできます。 ブラインドを実行する、以降のデプロイでのコピーで、実稼働データベースに入力データが上書きされます。 代わりに、データベースを展開するには、開発用データベースを実稼働データベースへの最後の配置以降に行われた変更を適用する必要があります。 このチュートリアルは、これらの課題を調べ、chronicling と最後の配置以降のデータベースに加えられた変更を適用することを支援するさまざまな方法を提供しています。


## <a name="introduction"></a>はじめに

前のチュートリアルで既に説明した、ASP.NET アプリケーションの配置、開発環境から運用環境に関連するコンテンツをコピーがあります。 展開は、1 回限りのイベントがありません。 ではなく場合や、ソフトウェアの新しいバージョンがリリースされるたびに発生するバグまたはセキュリティ上の問題を特定して対処します。 ASP.NET ページをコピーするときに前回の配置以降のイメージ、JavaScript ファイル、およびこれらのファイルに配慮する必要はありません、運用環境にこのようなその他のファイルが変更されました。 できます盲目的に、ファイルをコピーする運用環境では、既存のコンテンツを上書きします。 残念ながら、この単純さは、データベースを展開するのには拡張されません。

最初に、データ駆動型アプリケーションをデプロイするときに、開発環境を運用環境で無条件、データベースをコピーできます。 ブラインドを実行する、以降のデプロイでのコピーで、実稼働データベースに入力データが上書きされます。 適用する代わりに、データベースの配置は、*変更*開発用データベースを実稼働データベースへの最後の配置以降に行われました。 このチュートリアルは、これらの課題を調べ、chronicling と最後の配置以降のデータベースに加えられた変更を適用することを支援するさまざまな方法を提供しています。

## <a name="the-challenges-of-deploying-a-database"></a>データベースの配置の課題

最初に、データ駆動型アプリケーションをデプロイする前に 1 つのデータベースがある、盲目的にすることが最初に、データ駆動型アプリケーションをデプロイするときに開発環境でデータベースが namely でデータベースをコピーします開発環境、運用環境にします。 データベースの 2 つのコピーがあるアプリケーションをデプロイした後: 開発環境および実稼働環境で 1 つで 1 つ。

展開の間で開発および運用データベースは同期になります。実稼働データベースのスキーマが変更されていない、開発データベースのスキーマはの新機能が追加されるとを変更できます。 追加または列、テーブル、ビュー、またはストアド プロシージャを削除する場合があります。 開発用データベースに追加される重要なデータもあります。 多くのデータ ドリブン アプリケーションには、ルックアップ テーブルがないユーザーが編集可能なハード コーディングされた、アプリケーション固有のデータが設定が含まれます。 たとえば、オークションの web サイトには、落札されている項目の条件を記述するための選択肢のドロップダウン リストがあります。新規などの新しい好適、およびフェアします。 ドロップダウン リストで直接これらのオプションをハード コーディングするのではなく、データベース テーブル内に配置する、通常はお勧めします。 開発中は、役に立たなかったという名前の新しい条件がテーブルに追加し、アプリケーションをデプロイするときに場合、この同じレコードを実稼働データベースでルックアップ テーブルに追加する必要があります。

理想的には、データベースの配置は、開発から運用環境にデータベースをコピーします。 ただし、アプリケーションを展開し、開発を再開後、実稼働データベースがされている表示されている実際のユーザーからの実際のデータに注意してください。 そのため、運用環境で、[次へ] の展開に、開発からデータベースを単純にコピーした場合は、実稼働データベースを上書きして、既存のデータを失います。 最終的な結果は、こと、データベースの配置を要約する最後の展開以降、開発用データベースに加えられた変更を適用します。

データベースを展開するには、前回の配置以降のスキーマと、場合によっては、データの変更を適用することが含まれているため、変更の履歴をする必要がありますある維持 (または展開時に決定されます) これらの変更を運用環境に適用できるようにします。 さまざまな管理およびデータ モデルに変更を適用するための手法があります。

### <a name="defining-the-baseline"></a>ベースラインを定義します。

アプリケーションのデータベースに変更を維持するには、いくつか開始状態に変更を適用する基準がある必要があります。 極端な開始状態にないテーブル、ビュー、またはストアド プロシージャで空のデータベースが可能性があります。 このような基準は、すべてのデータベースのテーブル、ビュー、および初期デプロイ後に加えられた変更とストアド プロシージャの作成を含める必要があるために、大きな変化がログに発生します。 スペクトルのもう一方の端には、最初に、実稼働環境に配置されているデータベースのバージョンとしてベースラインを設定できます。 この選択は、次の最初のデプロイ、データベースに加えられた変更のみが含まれるために、変更ログはこれより小さな量で生成されます。 これは、ことをお勧めするアプローチです。 もちろんできます道路アプローチの複数の中間ベースラインを定義するいくつかのポイント間、データベースの最初の作成と最初にデータベースがデプロイされます。

したら選択基準では、構成基準のバージョンを再作成を実行できる SQL スクリプトを生成して検討してください。 このようなスクリプトを使うと、データベースのベースライン バージョンをすばやく再作成できます。 この機能は、大型のプロジェクトで特に便利なプロジェクトやテスト、ステージングなどの追加の環境で作業する複数の開発者である可能性がありますでそれぞれに独自のデータベースのコピーを必要があります。

さまざまな構成基準のバージョンの SQL スクリプトの生成に使用できるツールがあります。 SQL Server Management Studio (SSMS)、データベースを右クリックしては、タスクのサブメニューに移動し、スクリプトの生成オプションを選択します。 データベース オブジェクトを作成する SQL コマンドを含むファイルを生成するように指示できるスクリプト ウィザードが起動します。 別のオプションは、だけでなく、データベース テーブルで、データベース スキーマも、データを作成する SQL コマンドが生成できるデータベース公開ウィザードです。 データベース パブリッシュ ウィザードの詳細を説明したに戻り、*データベースを配置する*チュートリアル。 どのようなツールを使用するのに関係なく末尾が必要で、データベースのベースライン バージョンを再作成に使用できるスクリプト ファイルを必要な発生します。

## <a name="documenting-the-database-changes-in-prose"></a>Prose でデータベースの変更を文書化

開発フェーズ中に、データ モデルへの変更のログを保持する最も簡単な方法では、prose で変更を記録します。 たとえば、展開済みアプリケーションの開発中に新しい列を追加する場合、`Employees`テーブルから列を削除する、`Orders`テーブル、および新しいテーブルを追加 (`ProductCategories`)、テキスト ファイルや Microsoft Word 文書を維持します。次の履歴。

<a id="0.8_table01"></a>


| **変更日** | **変更の詳細** |
| --- | --- |
| 2009-02-03: | 追加された列`DepartmentID`(`int`、NOT NULL) を`Employees`テーブル。 外部キー制約を追加`Departments.DepartmentID`に`Employees.DepartmentID`します。 |
| 2009-02-05: | 削除された列`TotalWeight`から、`Orders`テーブル。 既にでキャプチャしたデータが関連付けられている`OrderDetails`レコード。 |
| 2009-02-12: | 作成、`ProductCategories`テーブル。 次の 3 つの列がある: `ProductCategoryID` (`int`、 `IDENTITY`、 `NOT NULL`)、 `CategoryName` (`nvarchar(50)`、 `NOT NULL`)、および`Active`(`bit`、 `NOT NULL`)。 主キー制約を追加`ProductCategoryID`、既定値は 1 ~`Active`します。 |


このアプローチの欠点を数多くあります。 まず、automation のことを期待することはありません。 いつでもこれらの変更は、アプリケーションの展開時に開発者が手動で実装する必要があります変更、一度に 1 つずつなどデータベースに適用する必要。 さらに、変更ログを使用してベースラインからのデータベースの特定のバージョンを再構築する場合は、そのため時間がかかりますますます多くログのサイズの拡大に合わせて。 このメソッドのもう 1 つは、わかりやすくするため、各変更ログ エントリの詳細レベルは左から人の変更を記録することです。 複数の開発者のチームで他よりも詳細なより読みやすい、またはより正確なのエントリが作成一部可能性があります。 また、入力ミスおよびその他の人に関連するデータ エントリ エラー場合があります。

Prose でデータベースの変更を文書化の主な利点は、わかりやすくするためです。 作成およびデータベース オブジェクトを変更するための SQL 構文知識の t 必要はありません。 代わりに、prose で変更を記録し、SQL Server Management Studio のグラフィカル ユーザー インターフェイスからそれらを実装できます。

Prose で、変更ログは、確かに、スコープ内に大きいものなど、特定のプロジェクトにも非常に高度で受注 t 作業を管理、データ モデルに頻繁に変更または複数の開発者が関係します。 ただし、このアプローチを勝ち取る、小規模プロジェクト データ モデルに不定期の変更のみを持ち、個人の開発者がない強力なバック グラウンドで作成およびデータベース オブジェクトを変更するための SQL 構文で非常にうまく機能させる見てきました。

> [!NOTE]
> 変更ログの情報は技術的には、展開時までに必要なだけの変更履歴を維持することをお勧めします。 1 つを保持することではなく変更のログ ファイル、成長し続けることを検討データベース バージョンごとに別の変更のログ ファイル。 通常はするバージョン、データベースが展開されている各時間。 変更ログのログを維持することにより、ベースラインから開始を再作成する任意のデータベース バージョン バージョン 1 以降では変更ログ スクリプトを実行してとを再作成する必要があります、バージョンに到達するまで続行します。


## <a name="recording-the-sql-change-statements"></a>変更の SQL ステートメントを記録

Prose の変更ログを維持するための主な欠点は、自動化に未対応です。 理想的には、デプロイ時に運用データベースにデータベースの変更の実装は手順の一覧を手動で実行する必要がなくスクリプトを実行するボタンをクリックすると同じくらい簡単でしょう。 そのような自動化は、データ モデルを変更するために使用するこれらの SQL コマンドを含む変更ログを保持することで。

SQL 構文では、複数のステートメントを作成すると、さまざまなデータベース オブジェクトの変更が含まれています。 たとえば、 [ *CREATE TABLE ステートメント*](https://msdn.microsoft.com/library/ms174979.aspx)を実行すると、指定した列と制約で新しいテーブルを作成します。 [ *ALTER TABLE ステートメント*](https://msdn.microsoft.com/library/ms190273.aspx) 、追加、削除、またはその列または制約を変更することは、既存のテーブルを変更します。 作成、変更、およびインデックス、ビュー、ユーザー定義関数、ストアド プロシージャ、トリガー、およびその他のデータベース オブジェクトを削除するステートメントもあります。

新しい列を追加する展開済みアプリケーションの開発中にイメージを前の例に戻る、`Employees`テーブルから列を削除する、`Orders`テーブル、および新しいテーブルの追加 (`ProductCategories`)。 このようなアクションは、次の SQL コマンドの変更のログ ファイルになります。

[!code-sql[Main](strategies-for-database-development-and-deployment-vb/samples/sample1.sql)]

1 回のクリック操作は、デプロイ時に実稼働データベースにこれらの変更をプッシュします。 SQL Server Management Studio を開き、実稼働データベースに接続する、新しいクエリ ウィンドウを開き、変更ログの内容を貼り付けますおよび実行スクリプトを実行する をクリックします。

## <a name="using-a-comparison-tool-to-synchronize-the-data-models"></a>比較ツールを使用して、データ モデルを同期するには

Prose でデータベースの変更を文書化は簡単ですが、開発者は一度に 1 つ、実稼働データベースの各変更を行う、変更を実装する必要があります。これらの変更を実装する、ボタンをクリックすると簡単で、実稼働データベースでは、変更、SQL コマンドを文書化、学習し、SQL ステートメントと作成およびデータベース オブジェクトを変更するための構文を使いこなすが必要です。 データベースの比較ツールは、両方のアプローチから最良のものを受け取り、最悪の事態を破棄します。

データベースの比較ツールは、スキーマまたは 2 つのデータベースのデータを比較し、データベースの違いを示すサマリー レポートが表示されます。 次に、ボタンをクリックして、1 つまたは複数のデータベース オブジェクトを同期するための SQL コマンドを生成できます。 データベースの比較ツールを使用するには、開発を比較して、実行時に変更が適用される実稼働データベースのスキーマにそのため、実稼働データベースで、展開時、SQL を含むファイルを生成するコマンドを簡単に言うと、その it開発データベースのスキーマを反映しています。

これは、さまざまなサード パーティのデータベースの比較ツールがさまざまなベンダーによって提供されます。 このような 1 つの例は、 [ *SQL Compare*](http://www.red-gate.com/products/SQL_Compare/)により、 [ *Red Gate Software*](http://www.red-gate.com/)します。 %S を SQL の比較を使用して、比較し、開発および運用データベース スキーマを同期するプロセスを説明を使用できます。

> [!NOTE]
> この記事の執筆時に、現在のバージョンの SQL の比較は、395 ドルのコストを Standard Edition では、バージョン 7.1 では、でした。 14 日間の無料試用版をダウンロードして理解できます。


SQL Compare の開始時に比較プロジェクト ダイアログ ボックスが開き、保存されている SQL Compare プロジェクトを表示します。 新しいプロジェクトを作成します。 比較するデータベースに関する情報を入力するプロジェクト構成ウィザードが起動 (図 1 参照)。 開発および運用環境のデータベースの情報を入力します。


[![開発と実稼働データベースを比較します。](strategies-for-database-development-and-deployment-vb/_static/image2.jpg)](strategies-for-database-development-and-deployment-vb/_static/image1.jpg)

**図 1**:開発と実稼働データベースの比較 ([フルサイズの画像を表示する をクリックします](strategies-for-database-development-and-deployment-vb/_static/image3.jpg))。


> [!NOTE]
> かどうか、開発環境のデータベースには、SQL Express Edition のデータベース ファイルで、`App_Data`図 1 に示すダイアログ ボックスで選択するには、SQL Server Express データベース サーバーでデータベースを登録する必要がありますが、web サイトのフォルダー。 これを実現する最も簡単な方法では、SQL Server Management Studio (SSMS) を開き、SQL Server Express データベース サーバーに接続して、データベースをアタッチします。 SSMS のコンピューターにインストールされていない場合は、ダウンロードしてから無料でインストール[*バージョンの SQL Server 2008 Management Studio Basic*](https://www.microsoft.com/downloads/details.aspx?FamilyId=7522A683-4CB2-454E-B908-E805E9BD4E28&amp;displaylang=en)します。


に加えて、比較するデータベースを選択すると、さまざまなオプション タブから比較設定を指定することもできます。1 つのオプションをオンにすることがありますが、「無視制約とインデックス名」 前のチュートリアルで追加されています、アプリケーション サービスの開発と運用環境のデータベースにデータベース オブジェクトを思い出してください。 使用した場合、`aspnet_regsql.exe`ツールを開発および運用データベースとの間に主キーと一意の制約名が異なることがわかりますし、実稼働データベースでこれらのオブジェクトを作成します。 その結果、SQL Compare フラグが設定されるすべての異なるとしてアプリケーション サービスのテーブル。 「を無視する制約とインデックス名」のままにすることができますか、オフにして、制約名を同期または SQL の比較をこれらの相違を無視するように指示します。

データベースを選択した後比較 (および比較オプションの確認)、比較を開始します [今すぐ比較] ボタンをクリックします。 次のいくつか秒間に SQL Compare は 2 つのデータベースのスキーマを検査し、どのように異なるかのレポートを生成します。 SQL Compare インターフェイスでこのような相違点を説明する方法を表示する開発用データベースにいくつかの変更を意図的加えました。 図 2 に示すようは追加したら、`BirthDate`列を`Authors`テーブルを削除、`ISBN`列から、`Books`テーブル、および、新しいテーブルを追加`Ratings`、ユーザー サイト率をレビュー対象のブックにアクセスできるようにすることは。

> [!NOTE]
> このチュートリアルで行われたデータ モデルの変更は、データベースの比較ツールを使用して説明するために行われました。 今後のチュートリアルでデータベースにこれらの変更が表示されますされません。


[![SQL の比較は、開発と実稼働データベースの違いを示します](strategies-for-database-development-and-deployment-vb/_static/image5.jpg)](strategies-for-database-development-and-deployment-vb/_static/image4.jpg)

**図 2**:SQL の比較には、開発の間の相違点と実稼働データベースが一覧表示されます ([フルサイズの画像を表示する をクリックします](strategies-for-database-development-and-deployment-vb/_static/image6.jpg))。


グループにデータベース オブジェクトを分解 SQL Compare、どのようなオブジェクトをすばやく表示する両方のデータベースに存在しますが、さまざまなオブジェクトが 1 つのデータベースが、一方に存在してがオブジェクトは同じです。 両方のデータベースに存在しますが、異なる 2 つのオブジェクトがあるように、:`Authors`テーブルで、追加の列がある、および`Books`テーブルで、1 つ削除します。 開発用データベース、つまり、新しく作成にのみ存在する 1 つのオブジェクトがある`Ratings`テーブル。 117 オブジェクトは両方のデータベースで同じですが。

データベース オブジェクトを選択するには、これらのオブジェクトの違いを示す [SQL の相違点] ウィンドウが表示されます。 図 2 では、下部に表示される、SQL の相違点 ウィンドウで強調表示する、`Authors`開発用データベース内のテーブルが、`BirthDate`列に含まれていない、`Authors`実稼働データベースのテーブル。

相違点を確認し、同期するオブジェクトを選択すると、した後は、次の手順は、開発用データベースに一致するように、運用データベースのスキーマを更新するために必要な SQL コマンドを生成します。 これは、同期ウィザードによって実現されます。 オブジェクトを同期して、操作をまとめたものです。 同期ウィザードを確認します (図 3 参照) を計画します。 データベースをすぐに同期したり、都合のよいタイミングで実行できる SQL コマンドのスクリプトを生成できます。


[![同期ウィザードを使用して、データベース スキーマを同期](strategies-for-database-development-and-deployment-vb/_static/image8.jpg)](strategies-for-database-development-and-deployment-vb/_static/image7.jpg)

**図 3**:データベース スキーマの同期の同期ウィザードを使用して ([フルサイズの画像を表示する をクリックします](strategies-for-database-development-and-deployment-vb/_static/image9.jpg))。


データベースの比較ツールなどの Red Gate Software の SQL Compare s、ポイント アンド クリックするだけの実稼働データベースには、開発データベースのスキーマに変更を適用します。

> [!NOTE]
> SQL Compare を比較し、2 つのデータベースを同期*スキーマ*します。 残念ながら、ありませんを比較し、2 つのデータベース テーブル内のデータを同期します。 Red Gate Software という製品を提供して[ *SQL データの比較*](http://www.red-gate.com/products/SQL_Data_Compare/)を比較し、2 つのデータベース間でデータを同期するが、SQL の比較から別の製品であり別 395 ドルのコストします。


## <a name="taking-the-application-offline-during-deployment"></a>デプロイ時にアプリケーションをオフライン

としてこれらのチュートリアルでは、全体の文言展開は複数の手順を含むプロセス: 開発環境から運用環境に ASP.NET ページ、マスター ページ、CSS ファイル、JavaScript ファイル、画像、およびその他の必要なコンテンツをコピー環境です。が必要な場合は、実稼働環境に固有の構成情報をコピー最後の配置以降のデータ モデルに変更を適用しています。 ファイルの数、データベースの変更の複雑さに応じて次の手順できます任意の場所数秒からに数分かかるを完了します。 この期間中に、web アプリケーションは flux では、サイトにアクセスするユーザー エラーまたは予期しない動作が発生する可能性があります。

Web サイトをデプロイするときに、デプロイが完了するまで、「オフライン」web アプリケーションを実行することをお勧めします。 アプリケーションをオフライン (バックアップしておくと、展開プロセスが完了すると) ファイルをアップロードして、削除することと同じくらい簡単です。 ASP.NET 2.0 では、という名前のファイルが存在するだけで始まる`app_offline.htm`でアプリケーションのルート ディレクトリが全体の web サイト「オフライン」です。 内容では、そのサイトの ASP.NET ページへの要求は応答が自動的に、`app_offline.htm`ファイル。 そのファイルが削除されると、アプリケーションがオンラインに戻る。

アップロードする同じくらい簡単ですし、デプロイ時にオフライン アプリケーション、`app_offline.htm`の運用環境にファイルのルート ディレクトリ、展開プロセスを開始し、後に削除する (または別のものに名前を変更する) の前に 1 回の展開完了しました。 詳細についてはこの手法に John Peterson 記事を参照してくださいを[ *ASP.NET アプリケーション オフライン*](http://www.15seconds.com/issue/061207.htm)します。

## <a name="summary"></a>まとめ

データ ドリブン アプリケーションを展開する主な課題は、データベースの配置を中心として展開します。 開発環境で 1 - と運用環境で 1 つのデータベースの 2 つのバージョンがあるためは、開発の新機能が追加されるとこれらの 2 つのデータベース スキーマが同期なります。 新機能は、運用データベースとして、実際のユーザーからの実際のデータが設定されて、することはできませんを上書きするため、実稼働データベースで変更された開発用データベース (ASP.NET ページ、アプリケーションを構成するファイルを展開する場合とは異なりイメージ ファイル、およびなど)。 代わりに、データベースを展開するには、前回の配置以降に、実稼働データベースの開発用データベースに加えられた変更の正確なセットを実装する必要があります。

このチュートリアルを保守し、データベースの変更のログの適用、3 つの手法について説明しました。 最も簡単な方法で prose の変更を記録することです。 この手法を使用する実稼働データベースの手動プロセスでこれらの変更を実装する、これは必要ありません SQL コマンドのサポート技術情報の作成およびデータベース オブジェクトを変更するため。 高度なアプローチとつながります大規模なプロジェクトまたはプロジェクトで複数の開発者である 1 つとして一連の SQL コマンドを変更を記録することです。 これは、ターゲット データベースにこれらの変更をロールアウトが大幅に hastens します。 両方のアプローチの長所は、SQL Compare Red Gate Software s など、データベースの比較ツールを使用して実現できます。

このチュートリアルでは、データ ドリブン アプリケーションの配置への取り組みで終了します。 次の一連のチュートリアルは、運用環境でエラーに応答する方法を検索します。 死の黄色い画面ではなくではなくフレンドリ エラー ページを表示する方法について説明します。 エラーの詳細をログ記録する方法と、このようなエラーが発生したときにアラートを見てみましょう。

満足のプログラミングです。

> [!div class="step-by-step"]
> [前へ](configuring-a-website-that-uses-application-services-vb.md)
> [次へ](displaying-a-custom-error-page-vb.md)