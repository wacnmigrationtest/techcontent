## <a name="what-is"> </a>什么是表服务

Azure 表存储服务可存储大量结构化数据。该服务是一个 NoSQL 数据存储，接受来自 Azure 云内部和外部的通过验证的呼叫。Azure 表最适合存储结构化非关系型数据。表服务的常见用途包括：

-   存储 TB 量级的结构化数据，能够为 Web 规模应用程序提供服务
-   存储无需复杂联接、外键或存储过程，并且可以对其进行非规范化以实现快速访问的数据集
-   使用聚集索引快速查询数据
-   使用 OData 协议和 LINQ 查询以及 WCF 数据服务 .NET 库
    访问数据

您可以使用表服务来存储和查询大型结构化非关系型数据集，并且您的表会随着需求的增加而扩展。

## <a name="concepts"> </a>概念

表服务包含以下组件：

![Table1][Table1]

-   **URL 格式：**代码使用此地址格式对帐户中的表
    进行寻址：   
    http://`<storage account>`.table.core.chinacloudapi.cn/`<table>`  
      
    您可以直接使用此地址和 OData 协议来访问 Azure 表。有关详细信息，请参阅 [OData.org][]

-   **存储帐户:** 对 Azure 存储空间进行的所有访问都要 都要通过存储帐户完成。有关存储帐户容量的详细信息，请参见 [Azure 存储可伸缩性和性能目标](http://msdn.microsoft.com/zh-cn/library/dn249410.aspx)。

-   **表**：表是实体的集合。表不对实体强制实施架构，这意味着单个表可以包含具有不同属性集的实体。一个存储帐户可以包含的表数仅受存储帐户容量限制。

-   **实体**：与数据库行类似，一个实体就是一组属性。一个实体的大小可达 1 MB。

-   **属性**：属性是名称/值对。每个实体最多可包含 252 个用于存储数据的属性。每个实体还包含 3 个 系统属性，分别指定分区键、行键和时间戳。对具有相同分区键的实体的查询速度将更快，并且可以在原子操作中插入/更新这些实体。一个实体的行键是它在一个分区内的唯一标识符。


  
  [Table1]: ./media/storage-java-how-to-use-table-storage/table1.png
  [OData.org]: http://www.odata.org/
<!--HONumber=41-->
