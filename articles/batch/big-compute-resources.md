<properties
   pageTitle="批处理和 HPC 工作负荷在云中的资源 | Azure"
   description="列出了旨在帮助你在 Azure 中运行大规模并行批处理和高性能计算 (HPC) 工作负荷的技术资源。"
   services="batch, cloud-services, virtual-machines"
   documentationCenter=""
   authors="dlepow"
   manager="timlt"
   editor=""/>

<tags
   ms.service="multiple"
   ms.date="06/08/2016"
   wacn.date="07/25/2016"/>

# Azure 中的大型计算：用于批处理和高性能计算 (HPC) 的技术资源
这是一份技术资源指南，旨在帮助你在 Azure 中运行大规模并行、批处理和 HPC 工作负荷。在 Azure 中，可以使用各种 Azure 服务将现有的批处理或 HPC 工作负荷扩展到 Azure 云，或者生成新的大型计算解决方案。

## 解决方案选项

了解 Azure 中的大型计算选项，并根据工作负荷和业务需要选择适当的方法。

* [Batch 和 HPC 解决方案](/documentation/articles/batch-hpc-solutions/)


## Azure 批处理

[Batch ](/documentation/services/batch/) 是一种平台服务，可让你轻松地在应用程序中启用云功能和运行作业，而无需设置和管理群集与作业计划程序。使用 SDK 可将不同语言的客户端应用与 Azure Batch 集成相集成，将数据迁移到 Azure，以及生成作业运行管道。

* [文档](/documentation/services/batch/)

* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx)、[Python](http://azure-sdk-for-python.readthedocs.io/latest/)、[Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) 和 [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API 参考

* [Batch management .NET library（Batch 管理 .NET 库）](https://msdn.microsoft.com/library/mt463120.aspx)参考

* [教程：适用于 .NET 的 Azure Batch 库入门](/documentation/articles/batch-dotnet-get-started/)

* [Batch 论坛](https://social.msdn.microsoft.com/Forums/home?forum=azurebatch)

## HPC 群集解决方案

将现有的 Windows 或 Linux HPC 群集部署或扩展到 Azure，以运行计算密集型工作负荷。

### Microsoft HPC Pack

HPC Pack 是在 Azure 和 Windows Server 技术基础之上构建的 Microsoft 免费 HPC 解决方案，它能够运行 Windows 和 Linux HPC 工作负荷。

* [下载 HPC Pack 2012 R2 Update 3](https://www.microsoft.com/zh-cn/download/details.aspx?id=49922)

* [文档](https://technet.microsoft.com/zh-cn/library/jj899572.aspx)

* [使用 HPC Pack 迸发到 Azure 辅助角色实例](https://technet.microsoft.com/library/gg481749.aspx)

* [使用 HPC Pack 迸发到 Azure Batch](https://technet.microsoft.com/library/mt612877.aspx)

* [Windows HPC 论坛](https://social.microsoft.com/Forums/home?category=windowshpc)

### Linux 和 OSS 群集解决方案

使用这些 Azure 模板来部署 Linux HPC 群集。

* [运转 SLURM 群集](http://azure.microsoft.com/documentation/templates/slurm/)和[博客文章](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)

* [运转 Torque 群集](http://azure.microsoft.com/documentation/templates/torque-cluster/)

## Microsoft MPI

[Microsoft MPI](https://msdn.microsoft.com/zh-cn/library/bb524831.aspx) (MS-MPI) 是 Microsoft 实现的消息传递接口标准，用于在 Windows 平台上开发和运行并行应用程序。


* [下载 MS-MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)

* [MS-MPI 参考](https://msdn.microsoft.com/zh-cn/library/dn473458.aspx)

* [MPI 论坛](https://social.microsoft.com/Forums/home?forum=windowshpcmpi)


## 计算密集型实例

* [通过 Microsoft HPC Pack 设置 Windows RDMA 群集以运行 MPI 应用程序](/documentation/articles/virtual-machines-windows-hpcpack-cluster-rdma/)



## 示例和演示

* [Azure Batch C# and Python code samples（Azure Batch C# 和 Python 代码示例）](https://github.com/Azure/azure-batch-samples)

## 相关的 Azure 服务

* [HDInsight](/documentation/services/hdinsight/)

* [虚拟机](/documentation/services/virtual-machines/)

* [云服务](/documentation/services/cloud-services/)

* [媒体服务](/documentation/services/media-services/)

## 体系结构蓝图

* [HPC and data orchestration using Azure Batch and Azure Data Factory（HPC 和数据的业务流程使用 Azure Batch 和 Azure 数据工厂）](http://go.microsoft.com/fwlink/?linkid=717686)(PDF)。

## 行业解决方案

* [Banking and capital markets（银行和资本市场）](https://finance.azure.com/)

* [Engineering simulations（工程模拟）](https://simulation.azure.com/)




## 后续步骤

* 有关最新通告，请参阅 [这些](/what-is-new/)。

<!---HONumber=Mooncake_0704_2016-->