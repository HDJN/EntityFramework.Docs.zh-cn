---
title: 非跟踪查询的 EF6
author: divega
ms.date: 2016-10-23
ms.prod: entity-framework
ms.author: divega
ms.manager: avickers
ms.technology: entity-framework-6
ms.topic: article
ms.assetid: f80ac260-c2dc-484d-94a3-3424fd862f8b
caps.latest.revision: 3
ms.openlocfilehash: 8310f2dab9e7ed9197a8c3e875e47e4f7b72d279
ms.sourcegitcommit: f05e7b62584cf228f17390bb086a61d505712e1b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2018
ms.locfileid: "39120080"
---
# <a name="no-tracking-queries"></a><span data-ttu-id="782eb-102">非跟踪查询</span><span class="sxs-lookup"><span data-stu-id="782eb-102">No-Tracking Queries</span></span>
<span data-ttu-id="782eb-103">有时你可能想要从查询中返回获取实体，但不是具有由上下文跟踪这些实体。</span><span class="sxs-lookup"><span data-stu-id="782eb-103">Sometimes you may want to get entities back from a query but not have those entities be tracked by the context.</span></span> <span data-ttu-id="782eb-104">查询大量的只读方案中的实体时，可能会导致更好的性能。</span><span class="sxs-lookup"><span data-stu-id="782eb-104">This may result in better performance when querying for large numbers of entities in read-only scenarios.</span></span> <span data-ttu-id="782eb-105">本主题所介绍的方法同样适用于查询使用 Code First 和 EF 设计器创建的模型。</span><span class="sxs-lookup"><span data-stu-id="782eb-105">The techniques shown in this topic apply equally to models created with Code First and the EF Designer.</span></span>  

<span data-ttu-id="782eb-106">新的扩展方法 AsNoTracking 允许在这种方式中运行任何查询。</span><span class="sxs-lookup"><span data-stu-id="782eb-106">A new extension method AsNoTracking allows any query to be run in this way.</span></span> <span data-ttu-id="782eb-107">例如：</span><span class="sxs-lookup"><span data-stu-id="782eb-107">For example:</span></span>  

``` csharp
using (var context = new BloggingContext())
{
    // Query for all blogs without tracking them
    var blogs1 = context.Blogs.AsNoTracking();

    // Query for some blogs without tracking them
    var blogs2 = context.Blogs
                        .Where(b => b.Name.Contains(".NET"))
                        .AsNoTracking()
                        .ToList();
}
```  