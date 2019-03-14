---
title: Web ファームでの ASP.NET Core のホスト
author: guardrex
description: Web ファーム環境での共有リソースを使用して、ASP.NET Core アプリのインスタンスを複数ホストする方法について説明します。
ms.author: riande
ms.custom: mvc
ms.date: 11/26/2018
uid: host-and-deploy/web-farm
ms.openlocfilehash: 4873665e6174a6acf885e1ebb41fb005d646bd1f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028619"
---
# <a name="host-aspnet-core-in-a-web-farm"></a><span data-ttu-id="2bbf4-103">Web ファームでの ASP.NET Core のホスト</span><span class="sxs-lookup"><span data-stu-id="2bbf4-103">Host ASP.NET Core in a web farm</span></span>

<span data-ttu-id="2bbf4-104">著者: [Luke Latham](https://github.com/guardrex)、[Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="2bbf4-104">By [Luke Latham](https://github.com/guardrex) and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="2bbf4-105">"*Web ファーム*" とは、アプリのインスタンスを複数ホストする、2 つ以上の Web サーバー (または "*ノード*") のグループのことです。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-105">A *web farm* is a group of two or more web servers (or *nodes*) that host multiple instances of an app.</span></span> <span data-ttu-id="2bbf4-106">ユーザーからの要求が Web ファームに到着すると、"*ロード バランサー*" が要求を Web ファームのノードに分散します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-106">When requests from users arrive to a web farm, a *load balancer* distributes the requests to the web farm's nodes.</span></span> <span data-ttu-id="2bbf4-107">Web ファームの利点は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-107">Web farms improve:</span></span>

* <span data-ttu-id="2bbf4-108">**信頼性/可用性** &ndash; 1 つまたは複数のノードに障害が発生しても、ロード バランサーによって要求がルーティングされ、要求の処理を続行することができます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-108">**Reliability/availability** &ndash; When one or more nodes fail, the load balancer can route requests to other functioning nodes to continue processing requests.</span></span>
* <span data-ttu-id="2bbf4-109">**容量/パフォーマンス** &ndash; 複数のノードは 1 台のサーバーよりもより多くの要求を処理できます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-109">**Capacity/performance** &ndash; Multiple nodes can process more requests than a single server.</span></span> <span data-ttu-id="2bbf4-110">ロード バランサーは、ノードへの要求を分散することにでワークロードのバランスをとります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-110">The load balancer balances the workload by distributing requests to the nodes.</span></span>
* <span data-ttu-id="2bbf4-111">**スケーラビリティ** &ndash; より多くの (またはより少ない) 容量が必要になると、ワークロードに一致するようにアクティブなノードの数を増加 (または減少) させることができます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-111">**Scalability** &ndash; When more or less capacity is required, the number of active nodes can be increased or decreased to match the workload.</span></span> <span data-ttu-id="2bbf4-112">[Azure App Service](https://azure.microsoft.com/services/app-service/) などの Web ファーム プラットフォーム テクノロジでは、システム管理者の要求に応じて、または人の介入なしに、自動的にノードを追加したり削除したりできます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-112">Web farm platform technologies, such as [Azure App Service](https://azure.microsoft.com/services/app-service/), can automatically add or remove nodes at the request of the system administrator or automatically without human intervention.</span></span>
* <span data-ttu-id="2bbf4-113">**保守容易性** &ndash; Web ファームのノードでは一連の共有サービスを利用できるため、システム管理が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-113">**Maintainability** &ndash; Nodes of a web farm can rely on a set of shared services, which results in easier system management.</span></span> <span data-ttu-id="2bbf4-114">たとえば、Web ファームのノードにおいて、画像やダウンロード可能ファイルなどの静的リソースのために、単一のデータベース サーバーと共通のネットワークの場所を利用することができます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-114">For example, the nodes of a web farm can rely upon a single database server and a common network location for static resources, such as images and downloadable files.</span></span>

<span data-ttu-id="2bbf4-115">このトピックでは、共有リソースを利用する Web ファームでホストされている ASP.NET Core アプリ用の構成と依存関係について説明します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-115">This topic describes configuration and dependencies for ASP.NET core apps hosted in a web farm that rely upon shared resources.</span></span>

## <a name="general-configuration"></a><span data-ttu-id="2bbf4-116">全般構成</span><span class="sxs-lookup"><span data-stu-id="2bbf4-116">General configuration</span></span>

<xref:host-and-deploy/index>  
<span data-ttu-id="2bbf4-117">ホスティング環境を設定し、ASP.NET Core アプリを展開する方法を学習します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-117">Learn how to set up hosting environments and deploy ASP.NET Core apps.</span></span> <span data-ttu-id="2bbf4-118">Web ファームの各ノード上のプロセス マネージャーを構成して、アプリの起動と再起動を自動化します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-118">Configure a process manager on each node of the web farm to automate app starts and restarts.</span></span> <span data-ttu-id="2bbf4-119">各ノードには ASP.NET Core ランタイムが必要です。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-119">Each node requires the ASP.NET Core runtime.</span></span> <span data-ttu-id="2bbf4-120">詳細については、ドキュメントの[ホストと展開](xref:host-and-deploy/index)に関する部分のトピックをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-120">For more information, see the topics in the [Host and deploy](xref:host-and-deploy/index) area of the documentation.</span></span>

<xref:host-and-deploy/proxy-load-balancer>  
<span data-ttu-id="2bbf4-121">プロキシ サーバーとロード バランサーの背後にホストされているアプリの構成について説明します。このような構成では、要求の重要な情報がわからなくなることがよくあります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-121">Learn about configuration for apps hosted behind proxy servers and load balancers, which often obscure important request information.</span></span>

<xref:host-and-deploy/azure-apps/index>  
<span data-ttu-id="2bbf4-122">[Azure App Service](https://azure.microsoft.com/services/app-service/) は ASP.NET Core を含む Web アプリをホストするための [Microsoft クラウド コンピューティング プラットフォーム サービス](https://azure.microsoft.com/)です。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-122">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span> <span data-ttu-id="2bbf4-123">App Service は、自動スケーリング、負荷分散、修正プログラムの適用、および継続的配置を提供する、フル マネージドのプラットフォームです。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-123">App Service is a fully managed platform that provides automatic scaling, load balancing, patching, and continuous deployment.</span></span>

## <a name="app-data"></a><span data-ttu-id="2bbf4-124">アプリのデータ</span><span class="sxs-lookup"><span data-stu-id="2bbf4-124">App data</span></span>

<span data-ttu-id="2bbf4-125">アプリが複数のインスタンスに対してスケーリングされると、ノード間での共有を必要とするアプリの状態が出現する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-125">When an app is scaled to multiple instances, there might be app state that requires sharing across nodes.</span></span> <span data-ttu-id="2bbf4-126">この状態が一時的である場合は、[IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache) を共有することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-126">If the state is transient, consider sharing an [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache).</span></span> <span data-ttu-id="2bbf4-127">共有状態を永続的に保つ必要がある場合は、共有状態をデータベースに格納することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-127">If the shared state requires persistence, consider storing the shared state in a database.</span></span>

## <a name="required-configuration"></a><span data-ttu-id="2bbf4-128">必要な構成</span><span class="sxs-lookup"><span data-stu-id="2bbf4-128">Required configuration</span></span>

<span data-ttu-id="2bbf4-129">Web ファームに展開されるアプリに対して、データの保護とキャッシュを構成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-129">Data Protection and Caching require configuration for apps deployed to a web farm.</span></span>

### <a name="data-protection"></a><span data-ttu-id="2bbf4-130">データの保護</span><span class="sxs-lookup"><span data-stu-id="2bbf4-130">Data Protection</span></span>

<span data-ttu-id="2bbf4-131">アプリでは、データを保護するために [ASP.NET Core データ保護システム](xref:security/data-protection/introduction)が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-131">The [ASP.NET Core Data Protection system](xref:security/data-protection/introduction) is used by apps to protect data.</span></span> <span data-ttu-id="2bbf4-132">データ保護では、"*キー リング*" に格納されている一連の暗号化キーが利用されます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-132">Data Protection relies upon a set of cryptographic keys stored in a *key ring*.</span></span> <span data-ttu-id="2bbf4-133">データ保護システムを初期化すると、キー リングをローカルに格納する[既定の設定](xref:security/data-protection/configuration/default-settings)が適用されます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-133">When the Data Protection system is initialized, it applies [default settings](xref:security/data-protection/configuration/default-settings) that store the key ring locally.</span></span> <span data-ttu-id="2bbf4-134">既定の構成では、Web ファームの各ノード上に一意のキー リングが格納されます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-134">Under the default configuration, a unique key ring is stored on each node of the web farm.</span></span> <span data-ttu-id="2bbf4-135">このため、Web ファームの各ノードは、他のノード上のアプリが暗号化したデータを暗号化解除することはできません。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-135">Consequently, each web farm node can't decrypt data that's encrypted by an app on any other node.</span></span> <span data-ttu-id="2bbf4-136">既定の構成が Web ファームでのアプリのホスト全般に対して適切であるわけではありません。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-136">The default configuration isn't generally appropriate for hosting apps in a web farm.</span></span> <span data-ttu-id="2bbf4-137">共有キー リングを実装する代わりに、ユーザー要求を常に同じノードにルーティングすることもできます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-137">An alternative to implementing a shared key ring is to always route user requests to the same node.</span></span> <span data-ttu-id="2bbf4-138">Web ファームの展開に向けたデータ保護システムの構成について詳しくは、<xref:security/data-protection/configuration/overview> をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-138">For more information on Data Protection system configuration for web farm deployments, see <xref:security/data-protection/configuration/overview>.</span></span>

### <a name="caching"></a><span data-ttu-id="2bbf4-139">キャッシュ</span><span class="sxs-lookup"><span data-stu-id="2bbf4-139">Caching</span></span>

<span data-ttu-id="2bbf4-140">Web ファーム環境におけるキャッシュのメカニズムでは、Web ファームのノード間でキャッシュされる項目を共有する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-140">In a web farm environment, the caching mechanism must share cached items across the web farm's nodes.</span></span> <span data-ttu-id="2bbf4-141">キャッシュは、一般的な Redis Cache (SQL Server 共有データベース) を利用するか、またはキャッシュされる項目を Web ファーム間で共有するカスタム実装のキャッシュを利用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-141">Caching must either rely upon a common Redis cache, a shared SQL Server database, or a custom caching implementation that shares cached items across the web farm.</span></span> <span data-ttu-id="2bbf4-142">詳細については、「 <xref:performance/caching/distributed> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-142">For more information, see <xref:performance/caching/distributed>.</span></span>

## <a name="dependent-components"></a><span data-ttu-id="2bbf4-143">依存コンポーネント</span><span class="sxs-lookup"><span data-stu-id="2bbf4-143">Dependent components</span></span>

<span data-ttu-id="2bbf4-144">次のシナリオに追加構成は必要ありませんが、シナリオが依存するテクノロジには、Web ファーム用の構成が必要です。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-144">The following scenarios don't require additional configuration, but they depend on technologies that require configuration for web farms.</span></span>

| <span data-ttu-id="2bbf4-145">シナリオ</span><span class="sxs-lookup"><span data-stu-id="2bbf4-145">Scenario</span></span> | <span data-ttu-id="2bbf4-146">依存先 &hellip;</span><span class="sxs-lookup"><span data-stu-id="2bbf4-146">Depends on &hellip;</span></span> |
| -------- | ------------------- |
| <span data-ttu-id="2bbf4-147">認証</span><span class="sxs-lookup"><span data-stu-id="2bbf4-147">Authentication</span></span> | <span data-ttu-id="2bbf4-148">データ保護 (<xref:security/data-protection/configuration/overview> を参照)。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-148">Data Protection (see <xref:security/data-protection/configuration/overview>).</span></span><br><br><span data-ttu-id="2bbf4-149">詳細については、次のトピックを参照してください。 <xref:security/authentication/cookie> および <xref:security/cookie-sharing></span><span class="sxs-lookup"><span data-stu-id="2bbf4-149">For more information, see <xref:security/authentication/cookie> and <xref:security/cookie-sharing>.</span></span> |
| <span data-ttu-id="2bbf4-150">Identity</span><span class="sxs-lookup"><span data-stu-id="2bbf4-150">Identity</span></span> | <span data-ttu-id="2bbf4-151">認証とデータベースの構成。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-151">Authentication and database configuration.</span></span><br><br><span data-ttu-id="2bbf4-152">詳細については、「 <xref:security/authentication/identity> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-152">For more information, see <xref:security/authentication/identity>.</span></span> |
| <span data-ttu-id="2bbf4-153">セッション</span><span class="sxs-lookup"><span data-stu-id="2bbf4-153">Session</span></span> | <span data-ttu-id="2bbf4-154">データ保護 (暗号化された Cookie) (<xref:security/data-protection/configuration/overview> を参照) とキャッシュ (<xref:performance/caching/distributed> を参照)。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-154">Data Protection (encrypted cookies) (see <xref:security/data-protection/configuration/overview>) and Caching (see <xref:performance/caching/distributed>).</span></span><br><br><span data-ttu-id="2bbf4-155">詳細については、次を参照してください。[セッションとアプリの状態。セッション状態](xref:fundamentals/app-state#session-state)します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-155">For more information, see [Session and app state: Session state](xref:fundamentals/app-state#session-state).</span></span> |
| <span data-ttu-id="2bbf4-156">TempData</span><span class="sxs-lookup"><span data-stu-id="2bbf4-156">TempData</span></span> | <span data-ttu-id="2bbf4-157">データ保護 (暗号化された cookie) (を参照してください<xref:security/data-protection/configuration/overview>) またはセッション (を参照してください[セッションとアプリの状態。セッション状態](xref:fundamentals/app-state#session-state))。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-157">Data Protection (encrypted cookies) (see <xref:security/data-protection/configuration/overview>) or Session (see [Session and app state: Session state](xref:fundamentals/app-state#session-state)).</span></span><br><br><span data-ttu-id="2bbf4-158">詳細については、次を参照してください。[セッションとアプリの状態。TempData](xref:fundamentals/app-state#tempdata)します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-158">For more information, see [Session and app state: TempData](xref:fundamentals/app-state#tempdata).</span></span> |
| <span data-ttu-id="2bbf4-159">偽造防止</span><span class="sxs-lookup"><span data-stu-id="2bbf4-159">Anti-forgery</span></span> | <span data-ttu-id="2bbf4-160">データ保護 (<xref:security/data-protection/configuration/overview> を参照)。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-160">Data Protection (see <xref:security/data-protection/configuration/overview>).</span></span><br><br><span data-ttu-id="2bbf4-161">詳細については、「 <xref:security/anti-request-forgery> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-161">For more information, see <xref:security/anti-request-forgery>.</span></span> |

## <a name="troubleshoot"></a><span data-ttu-id="2bbf4-162">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="2bbf4-162">Troubleshoot</span></span>

### <a name="data-protection-and-caching"></a><span data-ttu-id="2bbf4-163">データ保護とキャッシュ</span><span class="sxs-lookup"><span data-stu-id="2bbf4-163">Data Protection and caching</span></span>

<span data-ttu-id="2bbf4-164">データ保護またはキャッシュが Web ファーム環境用に構成されていない場合、要求の処理中に断続的にエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-164">When Data Protection or caching isn't configured for a web farm environment, intermittent errors occur when requests are processed.</span></span> <span data-ttu-id="2bbf4-165">このエラーは、ノード間で同じリソースが共有されておらず、ユーザー要求が同じノードにルーティングされない場合があるために発生します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-165">This occurs because nodes don't share the same resources and user requests aren't always routed back to the same node.</span></span>

<span data-ttu-id="2bbf4-166">ユーザーが Cookie 認証を使用してアプリにサインインする場合を考えてみます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-166">Consider a user who signs into the app using cookie authentication.</span></span> <span data-ttu-id="2bbf4-167">このユーザーは、1 つの Web ファームのノード上にあるアプリにサインインします。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-167">The user signs into the app on one web farm node.</span></span> <span data-ttu-id="2bbf4-168">ユーザーの次の要求が、ユーザーがサインインしたノードと同じノードに届いた場合、アプリは認証 Cookie の暗号化を解除して、アプリのリソースへのアクセスを許可することができます。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-168">If their next request arrives at the same node where they signed in, the app is able to decrypt the authentication cookie and allows access to the app's resource.</span></span> <span data-ttu-id="2bbf4-169">ユーザーの次の要求が異なるノードに届いた場合、アプリはユーザーがサインインしたノードの認証 Cookie の暗号化を解除できず、要求されたリソースに対する認証は失敗します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-169">If their next request arrives at a different node, the app can't decrypt the authentication cookie from the node where the user signed in, and authorization for the requested resource fails.</span></span>

<span data-ttu-id="2bbf4-170">次の現象のいずれかが**断続的に**発生するときは、多くの場合、データ保護またはキャッシュが Web ファーム環境に向けて適切に構成されていないことが問題の原因です。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-170">When any of the following symptoms occur **intermittently**, the problem is usually traced to improper Data Protection or caching configuration for a web farm environment:</span></span>

* <span data-ttu-id="2bbf4-171">認証の中断 &ndash; 認証 Cookie が正しく構成されていない、または暗号化解除できない。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-171">Authentication breaks &ndash; The authentication cookie is misconfigured or can't be decrypted.</span></span> <span data-ttu-id="2bbf4-172">OAuth (Facebook、Microsoft、Twitter) ログインまたは OpenIdConnect ログインが「関連付けできませんでした」というエラーで失敗する。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-172">OAuth (Facebook, Microsoft, Twitter) or OpenIdConnect logins fail with the error "Correlation failed."</span></span>
* <span data-ttu-id="2bbf4-173">承認の中断 &ndash; Id が失われる。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-173">Authorization breaks &ndash; Identity is lost.</span></span>
* <span data-ttu-id="2bbf4-174">セッション状態でデータが失われる。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-174">Session state loses data.</span></span>
* <span data-ttu-id="2bbf4-175">キャッシュされた項目が消える。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-175">Cached items disappear.</span></span>
* <span data-ttu-id="2bbf4-176">TempData が失敗する。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-176">TempData fails.</span></span>
* <span data-ttu-id="2bbf4-177">POST の失敗 &ndash; 偽造防止チェックが失敗する。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-177">POSTs fail &ndash; The anti-forgery check fails.</span></span>

<span data-ttu-id="2bbf4-178">Web ファームの展開に向けたデータ保護の構成について詳しくは、<xref:security/data-protection/configuration/overview> をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-178">For more information on Data Protection configuration for web farm deployments, see <xref:security/data-protection/configuration/overview>.</span></span> <span data-ttu-id="2bbf4-179">Web ファームの展開に向けたキャッシュの構成について詳しくは、「<xref:performance/caching/distributed>」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-179">For more information on caching configuration for web farm deployments, see <xref:performance/caching/distributed>.</span></span>

## <a name="obtain-data-from-apps"></a><span data-ttu-id="2bbf4-180">アプリからデータを取得する</span><span class="sxs-lookup"><span data-stu-id="2bbf4-180">Obtain data from apps</span></span>

<span data-ttu-id="2bbf4-181">Web ファーム アプリが要求に応答できる場合は、ターミナル インライン ミドルウェアを使用して、要求、接続、その他のデータをアプリから取得します。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-181">If the web farm apps are capable of responding to requests, obtain request, connection, and additional data from the apps using terminal inline middleware.</span></span> <span data-ttu-id="2bbf4-182">詳細およびサンプル コードについては、「<xref:test/troubleshoot#obtain-data-from-an-app>」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2bbf4-182">For more information and sample code, see <xref:test/troubleshoot#obtain-data-from-an-app>.</span></span>