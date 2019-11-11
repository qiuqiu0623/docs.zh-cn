---
title: 可观测性模式
description: 适用于云原生应用程序的可观察性模式
ms.date: 09/23/2019
ms.openlocfilehash: 23320144c03278d631b8a1fcc1d1c0954e907296
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "73841065"
---
# <a name="observability-patterns"></a><span data-ttu-id="a7168-103">可观测性模式</span><span class="sxs-lookup"><span data-stu-id="a7168-103">Observability patterns</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="a7168-104">正如为了帮助应用程序中的代码布局而开发的模式一样，以可靠方式为操作应用程序提供模式。</span><span class="sxs-lookup"><span data-stu-id="a7168-104">Just as patterns have been developed to aid in the layout of code in applications, there are patterns for operating applications in a reliable way.</span></span> <span data-ttu-id="a7168-105">维护应用程序的三种有用模式已经出现：日志记录、监视和警报。</span><span class="sxs-lookup"><span data-stu-id="a7168-105">Three useful patterns in maintaining applications have emerged: logging, monitoring, and alerts.</span></span>

## <a name="when-to-use-logging"></a><span data-ttu-id="a7168-106">何时使用日志记录</span><span class="sxs-lookup"><span data-stu-id="a7168-106">When to use logging</span></span>

<span data-ttu-id="a7168-107">无论如何，应用程序在生产中几乎总是以意想不到的方式运行。</span><span class="sxs-lookup"><span data-stu-id="a7168-107">No matter how careful we are, applications almost always behave in unexpected ways in production.</span></span> <span data-ttu-id="a7168-108">当用户报告应用程序出现问题时，如果出现问题，可以查看应用程序的情况非常有用。</span><span class="sxs-lookup"><span data-stu-id="a7168-108">When users report problems with an application, it's extremely useful to be able to see what was going on with the app when the problem occurred.</span></span> <span data-ttu-id="a7168-109">捕获有关应用程序在运行时所做操作的信息的一种最尝试和真正的方法是让应用程序记下正在执行的操作。</span><span class="sxs-lookup"><span data-stu-id="a7168-109">One of the most tried and true ways of capturing information about what an application is doing while it's running is to have the application write down what it's doing.</span></span> <span data-ttu-id="a7168-110">此过程称为日志记录。</span><span class="sxs-lookup"><span data-stu-id="a7168-110">This process is known as logging.</span></span> <span data-ttu-id="a7168-111">在生产环境中出现故障或问题时，目标应该是在非生产环境中重现发生失败的情况。</span><span class="sxs-lookup"><span data-stu-id="a7168-111">Anytime failures or problems occur in production, the goal should be to reproduce the conditions under which the failures occurred, in a non-production environment.</span></span> <span data-ttu-id="a7168-112">准备好的日志记录可为开发人员提供一个路线图，以便在可通过测试和 vspackage 的环境中重现问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-112">Having good logging in place provides a roadmap for developers to follow in order to duplicate problems in an environment that can be tested and experimented with.</span></span>

### <a name="logging-in-cloud-native-applications"></a><span data-ttu-id="a7168-113">云本机应用程序中的日志记录</span><span class="sxs-lookup"><span data-stu-id="a7168-113">Logging in cloud-native applications</span></span>

<span data-ttu-id="a7168-114">每种编程语言都有允许编写日志的工具，通常，写入这些日志的开销也很低。</span><span class="sxs-lookup"><span data-stu-id="a7168-114">Every programming language has tooling that permits writing logs, and typically the overhead for writing these logs is low.</span></span> <span data-ttu-id="a7168-115">许多日志记录库提供了记录不同种类的重要性，可在运行时进行优化。</span><span class="sxs-lookup"><span data-stu-id="a7168-115">Many of the logging libraries provide logging different kinds of criticalities, which can be tuned at run time.</span></span> <span data-ttu-id="a7168-116">例如，Serilog 库是适用于 .NET 的常用结构化日志记录库，提供以下日志记录级别</span><span class="sxs-lookup"><span data-stu-id="a7168-116">For instance, the Serilog library is a popular structured logging library for .NET that provides the following logging levels</span></span>

* <span data-ttu-id="a7168-117">详细</span><span class="sxs-lookup"><span data-stu-id="a7168-117">Verbose</span></span>
* <span data-ttu-id="a7168-118">调试</span><span class="sxs-lookup"><span data-stu-id="a7168-118">Debug</span></span>
* <span data-ttu-id="a7168-119">信息</span><span class="sxs-lookup"><span data-stu-id="a7168-119">Information</span></span>
* <span data-ttu-id="a7168-120">警告</span><span class="sxs-lookup"><span data-stu-id="a7168-120">Warning</span></span>
* <span data-ttu-id="a7168-121">Error</span><span class="sxs-lookup"><span data-stu-id="a7168-121">Error</span></span>
* <span data-ttu-id="a7168-122">出现</span><span class="sxs-lookup"><span data-stu-id="a7168-122">Fatal</span></span>

<span data-ttu-id="a7168-123">这些不同的日志级别提供日志记录的粒度。</span><span class="sxs-lookup"><span data-stu-id="a7168-123">These different log levels provide granularity in logging.</span></span> <span data-ttu-id="a7168-124">当应用程序在生产环境中正常运行时，可以将其配置为仅记录重要的消息。</span><span class="sxs-lookup"><span data-stu-id="a7168-124">When the application is functioning properly in production, it may be configured to only log important messages.</span></span> <span data-ttu-id="a7168-125">当应用程序行为不好时，可以增加日志级别，以便收集更详细的日志。</span><span class="sxs-lookup"><span data-stu-id="a7168-125">When the application is misbehaving, then the log level can be increased so more verbose logs are gathered.</span></span> <span data-ttu-id="a7168-126">这会平衡性能，使其易于调试。</span><span class="sxs-lookup"><span data-stu-id="a7168-126">This balances performance against ease of debugging.</span></span>

<span data-ttu-id="a7168-127">日志记录工具的高性能和详细级别的 tunability 应鼓励开发人员经常记录。</span><span class="sxs-lookup"><span data-stu-id="a7168-127">The high performance of logging tools and the tunability of verbosity should encourage developers to log frequently.</span></span> <span data-ttu-id="a7168-128">很多倾向于记录每个方法的输入和退出的模式。</span><span class="sxs-lookup"><span data-stu-id="a7168-128">Many favor a pattern of logging the entry and exit of each method.</span></span> <span data-ttu-id="a7168-129">这种方法可能听起来像是多余，但开发人员很少需要更少的日志记录。</span><span class="sxs-lookup"><span data-stu-id="a7168-129">This approach may sound like overkill, but it's infrequent that developers will wish for less logging.</span></span> <span data-ttu-id="a7168-130">事实上，出于将日志记录添加到有问题的方法的唯一目的，执行部署并不少见。</span><span class="sxs-lookup"><span data-stu-id="a7168-130">In fact, it's not uncommon to perform deployments for the sole purpose of adding logging around a problematic method.</span></span> <span data-ttu-id="a7168-131">错误记录一侧，而不太少。</span><span class="sxs-lookup"><span data-stu-id="a7168-131">Err on the side of too much logging and not on too little.</span></span> <span data-ttu-id="a7168-132">请注意，某些工具可用于自动提供此类日志记录。</span><span class="sxs-lookup"><span data-stu-id="a7168-132">Note that some tools can be used to automatically provide this kind of logging.</span></span>

<span data-ttu-id="a7168-133">在传统的应用程序中，日志文件通常存储在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="a7168-133">In traditional applications, log files were typically stored on the local machine.</span></span> <span data-ttu-id="a7168-134">事实上，在类似 Unix 的操作系统上，有一个文件夹结构定义为保存任何日志，通常在 `/var/log`下。</span><span class="sxs-lookup"><span data-stu-id="a7168-134">In fact, on Unix-like operating systems, there's a folder structure defined to hold any logs, typically under `/var/log`.</span></span> <span data-ttu-id="a7168-135">在云环境中，将日志记录到单台计算机上的平面文件的有用性大大减少。</span><span class="sxs-lookup"><span data-stu-id="a7168-135">The usefulness of logging to a flat file on a single machine is vastly reduced in a cloud environment.</span></span> <span data-ttu-id="a7168-136">生成日志的应用程序可能无法访问本地磁盘或本地磁盘，因为容器是在物理计算机上无序的。</span><span class="sxs-lookup"><span data-stu-id="a7168-136">Applications producing logs may not have access to the local disk or the local disk may be highly transient as containers are shuffled around physical machines.</span></span>

<span data-ttu-id="a7168-137">使用微服务体系结构开发的云本机应用程序还会对基于文件的记录器带来一些挑战。</span><span class="sxs-lookup"><span data-stu-id="a7168-137">Cloud-native applications developed using a microservices architecture also pose some challenges for file-based loggers.</span></span> <span data-ttu-id="a7168-138">用户请求现在可能跨在不同计算机上运行的多个服务，可能包括无服务器函数，根本不能访问本地文件系统。</span><span class="sxs-lookup"><span data-stu-id="a7168-138">User requests may now span multiple services that are run on different machines, and may include serverless functions with no access to a local file system at all.</span></span> <span data-ttu-id="a7168-139">将用户或会话中的日志与许多服务和计算机的关联起来非常困难。</span><span class="sxs-lookup"><span data-stu-id="a7168-139">It would be very challenging to correlate the logs from a user or a session across these many services and machines.</span></span>

<span data-ttu-id="a7168-140">最后，某些云本机应用程序中的用户数很高。</span><span class="sxs-lookup"><span data-stu-id="a7168-140">Finally, the number of users in some cloud-native applications is high.</span></span> <span data-ttu-id="a7168-141">假设每个用户登录到应用程序时都会生成几百行的日志消息。</span><span class="sxs-lookup"><span data-stu-id="a7168-141">Imagine that each user generates a hundred lines of log messages when they log into an application.</span></span> <span data-ttu-id="a7168-142">隔离，这是可管理的，但会将超过100000的用户和日志量相乘。</span><span class="sxs-lookup"><span data-stu-id="a7168-142">In isolation, that is manageable, but multiply that over 100,000 users and the volume of logs becomes large.</span></span>

<span data-ttu-id="a7168-143">幸运的是，有一些更好的替代方法使用基于文件系统的日志记录。</span><span class="sxs-lookup"><span data-stu-id="a7168-143">Fortunately, there are some fantastic alternatives to using file system-based logging.</span></span> <span data-ttu-id="a7168-144">所有日志都发送到其中的集中式日志服务器，可解决所有这些问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-144">A centralized log server to which all logs are sent, fixes all these problems.</span></span> <span data-ttu-id="a7168-145">日志由应用程序收集，并发送到一个集中式日志记录应用程序，用于索引和存储日志。</span><span class="sxs-lookup"><span data-stu-id="a7168-145">Logs are collected by the applications and shipped to a central logging application which indexes and stores the logs.</span></span> <span data-ttu-id="a7168-146">此类系统每天可以引入数十个千兆字节的日志。</span><span class="sxs-lookup"><span data-stu-id="a7168-146">This class of system can ingest tens of gigabytes of logs every day.</span></span>

<span data-ttu-id="a7168-147">构建跨越许多服务的日志记录时，遵循一些标准做法也是有帮助的。</span><span class="sxs-lookup"><span data-stu-id="a7168-147">It's also helpful to follow some standard practices when building logging that spans many services.</span></span> <span data-ttu-id="a7168-148">例如，在时间较长的交互时生成[相关 ID](https://blog.rapid7.com/2016/12/23/the-value-of-correlation-ids/) ，然后将其记录在与该交互相关的每个消息中，使得搜索所有相关消息变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="a7168-148">For instance, generating a [correlation ID](https://blog.rapid7.com/2016/12/23/the-value-of-correlation-ids/) at the start of a lengthy interaction, and then logging it in each message that is related to that interaction, makes it easier to search for all related messages.</span></span> <span data-ttu-id="a7168-149">只需查找单个消息，然后提取相关 ID 即可查找所有相关的消息。</span><span class="sxs-lookup"><span data-stu-id="a7168-149">One need only find a single message and extract the correlation ID to find all the related messages.</span></span> <span data-ttu-id="a7168-150">另一个示例是确保每个服务的日志格式都是相同的，无论使用何种语言或日志记录库。</span><span class="sxs-lookup"><span data-stu-id="a7168-150">Another example is ensuring that the log format is the same for every service, whatever the language or logging library it uses.</span></span> <span data-ttu-id="a7168-151">这一标准化使得读取日志变得更加容易。</span><span class="sxs-lookup"><span data-stu-id="a7168-151">This standardization makes reading logs much easier.</span></span> <span data-ttu-id="a7168-152">图7-1 演示了微服务体系结构如何利用集中式日志记录作为其工作流的一部分。</span><span class="sxs-lookup"><span data-stu-id="a7168-152">Figure 7-1 demonstrates how a microservices architecture can leverage centralized logging as part of its workflow.</span></span>

<span data-ttu-id="a7168-153">来自各种来源的 ![日志会被引入到一个集中的日志存储中。](./media/centralized-logging.png)
**图 7-1**。</span><span class="sxs-lookup"><span data-stu-id="a7168-153">![Logs from various sources are ingested into a centralized log store.](./media/centralized-logging.png)
**Figure 7-1**.</span></span> <span data-ttu-id="a7168-154">来自各种来源的日志会被引入到一个集中的日志存储中。</span><span class="sxs-lookup"><span data-stu-id="a7168-154">Logs from various sources are ingested into a centralized log store.</span></span>

## <a name="when-to-use-monitoring"></a><span data-ttu-id="a7168-155">何时使用监视</span><span class="sxs-lookup"><span data-stu-id="a7168-155">When to use monitoring</span></span>

<span data-ttu-id="a7168-156">有些应用程序并不关键。</span><span class="sxs-lookup"><span data-stu-id="a7168-156">Some applications aren't mission-critical.</span></span> <span data-ttu-id="a7168-157">也许它们只能在内部使用，并且在出现问题时，用户可以与负责的团队联系，并且可以重新启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="a7168-157">Maybe they're only used internally, and when a problem occurs, the user can contact the team responsible and the application can be restarted.</span></span> <span data-ttu-id="a7168-158">但是，客户通常对其使用的应用程序具有更高的预期。</span><span class="sxs-lookup"><span data-stu-id="a7168-158">However, customers often have higher expectations for the applications they consume.</span></span> <span data-ttu-id="a7168-159">如果你需要了解应用程序在用户执行*之前*或用户通知之前出现的问题，则需要监视其当前状态。</span><span class="sxs-lookup"><span data-stu-id="a7168-159">If you need to know when problems occur with your application *before* users do, or before users notify you, you need to monitor its current state.</span></span> <span data-ttu-id="a7168-160">正确实现后，监视可以让你了解将导致问题的条件，让你可以在这些条件导致用户影响之前解决这些问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-160">Implemented properly, monitoring can let you know about conditions that will lead to problems, letting you address underlying conditions before they result in any user impact.</span></span>

## <a name="monitoring-considerations"></a><span data-ttu-id="a7168-161">监视注意事项</span><span class="sxs-lookup"><span data-stu-id="a7168-161">Monitoring considerations</span></span>

<span data-ttu-id="a7168-162">某些集中式日志记录系统采用额外的角色，在纯粹的日志以外收集遥测数据。</span><span class="sxs-lookup"><span data-stu-id="a7168-162">Some centralized logging systems take on an additional role of collecting telemetry outside of pure logs.</span></span> <span data-ttu-id="a7168-163">它们可以收集指标，例如运行数据库查询所用的时间、来自 web 服务器的平均响应时间，甚至是操作系统报告的 CPU 负载平均值和内存压力。</span><span class="sxs-lookup"><span data-stu-id="a7168-163">They can collect metrics, such as time to run a database query, average response time from a web server, and even CPU load averages and memory pressure as reported by the operating system.</span></span> <span data-ttu-id="a7168-164">这些系统与日志结合使用，可提供系统中节点和整个应用程序的运行状况的整体视图。</span><span class="sxs-lookup"><span data-stu-id="a7168-164">In conjunction with the logs, these systems can provide a holistic view of the health of nodes in the system and the application as a whole.</span></span>

<span data-ttu-id="a7168-165">还可以从应用程序中手动采集监视工具的指标收集功能。</span><span class="sxs-lookup"><span data-stu-id="a7168-165">The metric gathering capabilities of the monitoring tools can also be fed manually from within the application.</span></span> <span data-ttu-id="a7168-166">可能会检测到特别感兴趣的业务流程（如新用户注册或订单），以使其在中央监视系统中递增计数器。</span><span class="sxs-lookup"><span data-stu-id="a7168-166">Business flows that are of particular interest such as new users signing up or orders being placed, may be instrumented such that they increment a counter in the central monitoring system.</span></span> <span data-ttu-id="a7168-167">这会解锁监视工具，不仅监视应用程序的运行状况，而且还会监视业务的运行状况。</span><span class="sxs-lookup"><span data-stu-id="a7168-167">This unlocks the monitoring tools to not only monitor the health of the application but the health of the business.</span></span>

<span data-ttu-id="a7168-168">可以在日志聚合工具中构造查询，以查找特定的统计信息或模式，然后在自定义仪表板上以图形形式显示这些统计信息或模式。</span><span class="sxs-lookup"><span data-stu-id="a7168-168">Queries can be constructed in the log aggregation tools to look for certain statistics or patterns, which can then be displayed in graphical form, on custom dashboards.</span></span> <span data-ttu-id="a7168-169">通常情况下，团队将投资完成与应用程序相关的统计信息。</span><span class="sxs-lookup"><span data-stu-id="a7168-169">Frequently, teams will invest in large, wall-mounted displays that rotate through the statistics related to an application.</span></span> <span data-ttu-id="a7168-170">这样一来，就很容易看到发生的问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-170">This way, it's simple to see the problems as they occur.</span></span>

## <a name="when-to-use-alerts"></a><span data-ttu-id="a7168-171">何时使用警报</span><span class="sxs-lookup"><span data-stu-id="a7168-171">When to use alerts</span></span>

<span data-ttu-id="a7168-172">如果需要对应用程序的问题做出响应，则需要通过某种方式向正确的人员发出警报。</span><span class="sxs-lookup"><span data-stu-id="a7168-172">If you need to react to problems with your application, you need some way to alert the right personnel.</span></span> <span data-ttu-id="a7168-173">这是第三个云本机应用程序可观察性模式，具体取决于日志记录和监视。</span><span class="sxs-lookup"><span data-stu-id="a7168-173">This is the third cloud-native application observability pattern, and depends on logging and monitoring.</span></span> <span data-ttu-id="a7168-174">你的应用程序需要有日志记录，以便能够诊断问题，并在某些情况下进入监视工具。</span><span class="sxs-lookup"><span data-stu-id="a7168-174">Your application needs to have logging in place to allow problems to be diagnosed, and in some cases to feed into monitoring tools.</span></span> <span data-ttu-id="a7168-175">It 需要监视将应用程序指标和运行状况数据聚合到一个位置。</span><span class="sxs-lookup"><span data-stu-id="a7168-175">It needs monitoring to aggregate application metrics and health data in one place.</span></span> <span data-ttu-id="a7168-176">一旦建立了此值，则可以创建规则，当某些指标超出可接受的级别时，会触发警报。</span><span class="sxs-lookup"><span data-stu-id="a7168-176">Once this has been established, rules can be created that will trigger alerts when certain metrics fall outside of acceptable levels.</span></span>

## <a name="alerts"></a><span data-ttu-id="a7168-177">警报</span><span class="sxs-lookup"><span data-stu-id="a7168-177">Alerts</span></span>

<span data-ttu-id="a7168-178">您可以对监视工具创建查询以查找已知的故障条件。</span><span class="sxs-lookup"><span data-stu-id="a7168-178">You can craft queries against the monitoring tools to look for known failure conditions.</span></span> <span data-ttu-id="a7168-179">例如，查询可以在传入日志中搜索 HTTP 状态代码500的指示，这表示 web 服务器上存在问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-179">For instance, queries could search through the incoming logs for indications of HTTP status code 500, which indicates a problem on a web server.</span></span> <span data-ttu-id="a7168-180">一旦检测到其中一项，就可以将电子邮件或短信发送给发起调查的原始服务的所有者。</span><span class="sxs-lookup"><span data-stu-id="a7168-180">As soon as one of these is detected, then an e-mail or an SMS could be sent to the owner of the originating service who can begin to investigate.</span></span>

<span data-ttu-id="a7168-181">不过，通常情况下，单个500错误不足以确定是否出现了问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-181">Typically though, a single 500 error isn't sufficient to determine that a problem has occurred.</span></span> <span data-ttu-id="a7168-182">这可能意味着用户键入的密码不正确或输入的数据格式不正确。</span><span class="sxs-lookup"><span data-stu-id="a7168-182">It could mean that a user mistyped their password or entered some malformed data.</span></span> <span data-ttu-id="a7168-183">仅当检测到的500错误的平均数量大于平均数量时，才会触发警报查询。</span><span class="sxs-lookup"><span data-stu-id="a7168-183">The alert queries can be crafted to only fire when a larger than average number of 500 errors are detected.</span></span>

<span data-ttu-id="a7168-184">最有破坏性的警报模式之一就是激发太多的警报，供人们调查。</span><span class="sxs-lookup"><span data-stu-id="a7168-184">One of the most damaging patterns in alerting is to fire too many alerts for humans to investigate.</span></span> <span data-ttu-id="a7168-185">服务所有者很快就会 desensitized 以前调查并发现良性的错误。</span><span class="sxs-lookup"><span data-stu-id="a7168-185">Service owners will rapidly become desensitized to errors that they've previously investigated and found to be benign.</span></span> <span data-ttu-id="a7168-186">如果发生 true 错误，它们将在数百个误报时丢失。</span><span class="sxs-lookup"><span data-stu-id="a7168-186">When true errors occur then they'll be lost in the noise of hundreds of false positives.</span></span> <span data-ttu-id="a7168-187">[Cried 狼](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf)的 parable 经常被告知儿童向儿童发出警告。</span><span class="sxs-lookup"><span data-stu-id="a7168-187">The parable of the [Boy Who Cried Wolf](https://en.wikipedia.org/wiki/The_Boy_Who_Cried_Wolf) is frequently told to children to warn them of this very danger.</span></span> <span data-ttu-id="a7168-188">务必确保触发的警报是真正的问题。</span><span class="sxs-lookup"><span data-stu-id="a7168-188">It's important to ensure that the alerts that do fire are indicative of a real problem.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="a7168-189">[上一页](monitoring-health.md)
>[下一页](logging-with-elastic-stack.md)</span><span class="sxs-lookup"><span data-stu-id="a7168-189">[Previous](monitoring-health.md)
[Next](logging-with-elastic-stack.md)</span></span>