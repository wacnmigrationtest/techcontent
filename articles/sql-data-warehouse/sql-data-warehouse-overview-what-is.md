<!-- Remove portal -->
<properties
   pageTitle="什么是 Azure SQL 数据仓库 | Azure"
   description="企业级分布式数据库，可处理 PB 量级的关系数据和非关系数据。它是行业首个云数据仓库，可以在数秒内增长、收缩和暂停。"
   services="sql-data-warehouse"
   documentationCenter="NA"
   authors="lodipalm"
   manager="barbkess"
   editor=""/>

<tags
   ms.service="sql-data-warehouse"
   ms.date="06/07/2016"
   wacn.date="07/25/2016"/>


# 什么是 Azure SQL 数据仓库？

Azure SQL 数据仓库是一种基于云的向外扩展数据库，可以处理大量数据（关系数据和非关系数据）。SQL 数据仓库在大规模并行处理 (MPP) 体系结构的基础上构建，可以处理你的企业工作负荷。

SQL 数据仓库：

- 将经验证的 SQL Server 关系数据库与 Azure 云向外扩展功能相结合。你可以在几秒钟内增加、减少、暂停或恢复计算。你可通过在需要时向外扩展 CPU，并在非高峰时段削减使用量，来节省成本。
- 利用我们的 Azure 平台。它易于部署、无缝维护并由于自动备份而完全容错。
- 它是 SQL Server 生态系统的补充。你可以使用熟悉的 SQL Server T-SQL 和工具进行开发。

继续阅读以了解有关 SQL 数据仓库的主要功能的详细信息。

## 大规模并行处理 (MPP) 体系结构

SQL 数据仓库使用 Microsoft 的大规模并行处理 (MPP) 体系结构，其设计目的是要运行一些世界上最大的本地数据仓库。

目前，我们的 MPP 体系结构将数据分布在 60 个无共享的存储和处理单元上。数据存储在高级本地冗余存储中，并链接到用于执行查询的计算节点。使用此体系结构，SQL 数据仓库采用分而治之的方法来运行复杂的 T-SQL 查询。进行处理时，控制节点将优化每个查询，然后将工作传递给计算节点，每个计算节点并行“攻克”其数据部分。

通过将 MPP 体系结构与 Azure 存储空间功能相结合，SQL 数据仓库可以：

- 独立于计算，扩大或缩小存储空间。
- 无需移动数据，即可增加或减少计算。
- 具有暂停计算功能，同时保持数据不变。
- 具有随时恢复计算功能。

下面将详细介绍该体系结构。

![SQL 数据仓库体系结构][1]


- **控制节点：**控制节点管理和优化查询。它是与所有应用程序和连接进行交互的前端。在 SQL 数据仓库中，控制节点由 SQL 数据库提供支持，并且连接到它时它看起来就像 SQL 数据库。表面之下，控制节点协调对分布式数据运行并行查询所需的所有数据移动和计算。当你将 TSQL 查询提交到 SQL 数据仓库时，控制节点会将其转换为可在每个计算节点上并行运行的单独查询。

- **计算节点：**计算节点将充当 SQL 数据仓库背后的强大功能。它们是用于存储数据并处理查询的 SQL 数据库。当你添加数据时，SQL 数据仓库向计算节点分配行。计算节点是对数据运行并行查询的工作节点。在处理后，它们将结果传递回控制节点。若要完成查询，控制节点聚合结果并返回最终结果。

- **存储：**你的数据存储在 Azure 存储 Blob 中。当计算节点与数据进行交互时，它们直接将数据写入到 blob 存储中并直接从 blob 存储读取数据。由于 Azure 存储空间可透明和无限地扩展，因此 SQL 数据仓库也可同样做到。由于计算与存储是独立的，因此 SQL 数据仓库可自动将缩放存储与缩放计算分开进行，反之亦然。Azure 存储空间还可以完全容错，并简化了备份和还原过程。

- **数据移动服务：**数据移动服务 (DMS) 是在节点之间移动数据的技术。DMS 向计算节点提供访问进行联接和聚合所需数据的权限。DMS 不是一项 Azure 服务。它是在所有节点上与 SQL 数据库一起运行的 Windows 服务。由于 DMS 在后台运行，因此你不会直接与它交互。但是，当你查看查询计划时，你会注意到它们包括某些 DMS 操作，因为在并行运行每个查询时数据移动是以某种形式必需的。


## 优化查询性能

此 MPP 方法得益于许多数据仓库特定性能优化方法，包括：

- 针对所有数据的分布式查询优化器和一组复杂的统计数据。使用有关数据大小和分布的信息，服务就能够通过评估特定分布式查询操作的成本来优化查询。

- 集成到数据移动进程中的高级算法和技术，可以根据需要有效地在计算资源之间移动数据，以便执行查询。这些数据移动操作是内置的，并且对数据移动服务的所有优化是自动进行的。

- 默认情况下，为聚集列存储索引。与传统的行导向存储相比，使用基于列的存储时，SQL 数据仓库最大可将压缩率提高 5 倍，将查询性能提高 10 倍。需要扫描大量行的分析查询非常适合使用列存储索引。

## 可缩放

SQL 数据仓库的体系结构引入了独立的存储和计算功能，可单独进行缩放。SQL 数据库的快速简单部署结构可以实现即时附加计算。可以借助 Azure 存储 Blob 来实现这项功能。使用 Blob 不仅提供稳定的复制存储，而且还提供低成本的轻松扩展基础结构。SQL 数据仓库运用云规模的存储和 Azure 计算的组合形式，允许你只在需要时支付查询性能存储的费用。更改计算量<!-- 就像是在 Azure 门户中将滑块向左或向右移动一样简单，但也-->可以使用 T-SQL 和 PowerShell 进行计划。

SQL 数据仓库提供独立于存储且可完全控制计算量的功能，可让你完全暂停数据仓库。在保留存储位置的同时，所有计算资源将释放到 Azure 的主池，立即为你节省费用。必要时，你只需恢复计算，让工作负荷使用数据和计算资源即可。

## 数据仓库单位

SQL 数据仓库的计算用量是使用 SQL 数据仓库单位 (DWU) 来计量的。DWU 是数据仓库拥有的基本能力度量，旨在确保在任何指定的时间拥有与仓库相关联的标准性能数量。具体而言，我们使用 DWU 来确保：

- 可以轻松缩放数据仓库，而不必考虑基础硬件或软件。

- 在更改数据仓库的大小之前，可以预测 DWU 级别的性能改进。

- 可以更改或移动实例的基础硬件与软件，而不影响工作负荷性能

- 我们可以调整服务的基础体系结构，而不影响工作负荷的性能。

- 当我们快速提升 SQL 数据仓库的性能时，我们可以确保以可缩放及适度影响系统的方式实现此目的。

具体而言，我们将数据仓库单位视为与数据仓库工作负荷性能高度相关的三个精确度量的度量值。我们对于一般可用性的目标是这些关键工作负荷度量值以针对数据仓库选择的 DWU 进行线性缩放。

**扫描/聚合：**此工作负荷度量值采用标准数据仓库查询，该查询扫描大量的行，然后执行复杂聚合。这是一种 IO 和 CPU 密集型操作。

**负载：**此度量值度量将数据引入服务的能力。PolyBase 从 Azure 存储 Blob 加载具代表性的数据集时完成负载。此度量值会增加服务的网络和 CPU 方面的压力。

**CREATE TABLE AS SELECT (CTAS)：**CTAS 度量创建表副本的能力。这涉及到从存储读取数据、跨设备的节点分发，以及重新写入到存储。这是一种 CPU 和网络密集型操作。

## 按需暂停和缩放

当你需要更快的结果时，可以增加 DWU 并为较高的性能付费。当你需要较小的计算能力时，可以减少 DWU 并且仅针对需要的项目付费。在下列情况下你可能会考虑更改 DWU：

- 在你无需运行查询时，可能是在晚上或周末，停止你的查询，然后暂停计算资源，以避免在不需要 DWU 时仍为它们付费。

- 当系统的资源需求较低时，考虑将 DWU 减少到较小大小，以允许用户访问数据，将此作为重要的节约成本的方法。

- 执行繁重的数据加载或转换操作时，你可能想要增加 DWU 以便可以更快地数据。

- 若要了解理想的 DWU 值，请尝试在加载数据之后增加和减少 DWU 并运行几个查询。由于缩放很快就能完成，你可以尝试一些不同级别的性能，不用超过一小时即可得知。

> [AZURE.NOTE] 请注意，由于 SQL 数据仓库的体系结构，在数据量不多的情况下，你可能看不到预期的性能能力。我们建议从大于或等于 1 TB 的数据卷开始，以便获得性能收益的真实指示。

## 在 SQL Server 的基础上构建

SQL 数据仓库基于 SQL Server 久经验证的关系数据库引擎，包含你希望企业数据仓库拥有的许多功能。如果你已熟悉 Transact-SQL，则使用 SQL 数据仓库时可以轻松运用这些知识。无论你是高级用户还是新手，都可以从本文档中的示例开始着手。总体上，你可以考虑我们构建 SQL 数据仓库的语言元素的方式，如下所示：

- SQL 数据仓库针对许多操作使用 SQL Server 的 Transact-SQL (TSQL) 语法，并且支持一组广泛的传统 SQL 构造，例如存储过程、用户定义的函式、表分区、索引和排序规则。

- SQL 数据仓库还包含一些最新的 SQL Server 功能，包括群集列存储索引、PolyBase 集成和数据审核（随附威胁评估）。

- SQL 数据仓库仍处于开发阶段，较不常用于数据仓库工作负荷或者比 SQL Server 还新的特定 TSQL 语言元素目前可能无法使用。请参阅我们的[迁移文档][]以获取与此问题相关的详细信息。

借助 SQL Server、SQL 数据仓库、SQL 数据库和分析平台系统之间的 Transact-SQL 与功能共通性，能够开发符合数据需求的解决方案。你可以根据性能、安全和缩放要求，决定存储数据的位置，然后根据需要在不同系统之间传输数据。

## 与 Microsoft 工具相集成

除了采用 SQL Server 的 TSQL 外围应用，SQL 数据仓库还集成了 SQL Server 用户可能很熟悉的许多工具。具体而言，我们着重于与 SQL 数据仓库的几个类别的工具集成，包括：

**传统的 SQL Server 工具：**SQL 数据仓库完全集成了 SQL Server Analysis Services、Integration Services 和 Reporting Services。

**基于云的工具：**SQL 数据仓库可与 Azure 中的多个新工具一起使用，并且与 Azure 的数据工厂、流分析、机器学习和 Power BI 紧密集成。有关我们集成的 Azure 工具列表，请参阅[《Integrated Tools Overview》（集成的工具概述）][]。

**第三方工具：**大量的第三方工具提供商都已确认能够与 SQL 数据仓库集成。有关合作伙伴的完整列表，请参阅[《SQL Data Warehouse solution partners》（SQL 数据仓库解决方案合作伙伴）][]。

## 混合方案

配合 PolyBase 使用 SQL 数据仓库可以给予用户前所未有的能力，在其生态系统之间移动数据，设置采用非关系与本地数据源的高级混合方案。

Polybase 易于使用，可让你通过使用熟悉的 T-SQL 命令来利用不同源中的数据。Polybase 使你可以像查询普通表一样查询 Azure Blob 存储中的非关系数据。使用 Polybase 可以查询非关系数据，或者将非关系数据导入 SQL 数据仓库。

- PolyBase 使用外部表访问非关系数据。表定义存储在 SQL 数据仓库中，可以通过 SQL 和用于访问普通关系数据的工具进行访问。

- Polybase 并不知道其集成状态。它为支持的所有源提供相同的特性和功能。Polybase 可读取各种格式的数据，包括分隔文件或 ORC 文件。

- 使用 PolyBase 可以访问同时用作 HD Insight 群集存储的 Blob 存储，让你像使用关系与非关系工具一样，以最新的方式访问相同的数据。

## 后续步骤

对 SQL 数据仓库有了初步的认识后，请继续了解[数据仓库工作负荷]、[如何预配] SQL 数据仓库，以及[如何加载示例数据]。或者，查看一下以下一些其他 SQL 数据仓库资源。

- [博客] 
- [CAT 团队博客]
- [MSDN 论坛]


<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Create Support Ticket]: /documentation/articles/sql-data-warehouse-get-started-create-support-ticket/
[数据仓库工作负荷]: /documentation/articles/sql-data-warehouse-overview-workload/
[如何加载示例数据]: /documentation/articles/sql-data-warehouse-load-sample-databases/
[如何预配]: /documentation/articles/sql-data-warehouse-get-started-provision-powershell/
[迁移文档]: /documentation/articles/sql-data-warehouse-overview-migrate/
[《SQL Data Warehouse solution partners》（SQL 数据仓库解决方案合作伙伴）]: /documentation/articles/sql-data-warehouse-integrate-solution-partners/
[《Integrated Tools Overview》（集成的工具概述）]: /documentation/articles/sql-data-warehouse-overview-integrate/

<!--MSDN references-->

<!--Other Web references-->
[博客]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[CAT 团队博客]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[MSDN 论坛]: https://social.msdn.microsoft.com/Forums/zh-CN/home?forum=AzureSQLDataWarehouse

<!---HONumber=Mooncake_0718_2016-->