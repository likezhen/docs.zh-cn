---
title: COR_GC_STATS 结构
ms.date: 03/30/2017
api_name:
- COR_GC_STATS
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- COR_GC_STATS
helpviewer_keywords:
- COR_GC_STATS structure [.NET Framework hosting]
ms.assetid: 8d4ff73e-739b-40f6-9349-359fbc99c2f9
topic_type:
- apiref
ms.openlocfilehash: 2ab0c38645a8e5fbd9e71b3c1787e88bfe2c0604
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79176521"
---
# <a name="cor_gc_stats-structure"></a>COR_GC_STATS 结构
提供有关通用语言运行时 （CLR） 的垃圾回收机制的统计信息。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct _COR_GC_STATS {  
    ULONG   Flags;
    SIZE_T  ExplicitGCCount;  
    SIZE_T  GenCollectionsTaken[3];  
    SIZE_T  CommittedKBytes;
    SIZE_T  ReservedKBytes;  
    SIZE_T  Gen0HeapSizeKBytes;  
    SIZE_T  Gen1HeapSizeKBytes;  
    SIZE_T  Gen2HeapSizeKBytes;  
    SIZE_T  LargeObjectHeapSizeKBytes;  
    SIZE_T  KBytesPromotedFromGen0;  
    SIZE_T  KBytesPromotedFromGen1;  
} COR_GC_STATS;  
```  
  
## <a name="members"></a>成员  
  
|成员|说明|  
|------------|-----------------|  
|`Flags`|指示应计算和返回哪些字段值。|  
|`ExplicitGCCount`|指示外部请求强制进行的垃圾回收数。|  
|`GenCollectionsTaken`|指示每代执行的垃圾回收数。|  
|`CommittedKBytes`|所有堆中提交的千字节的总数。|  
|`ReservedKBytes`|所有堆中保留的千字节的总数。|  
|`Gen0HeapSizeKBytes`|生成零堆的大小（以千字节为单位）。|  
|`Gen1HeapSizeKBytes`|第一代堆的大小（以千字节为单位）。|  
|`Gen2HeapSizeKBytes`|第二代堆的大小（以千字节为单位）。|  
|`LargeObjectHeapSizeKBytes`|大型对象堆的大小（以千字节为单位）。|  
|`KBytesPromotedFromGen0`|从第 0 代提升到第一代的对象的大小（以千字节为单位）。|  
|`KBytesPromotedFromGen1`|从第一代提升到第二代的对象的大小（以千字节为单位）。|  
  
## <a name="remarks"></a>备注  
 [ICLRGCManager：GetStats](../../../../docs/framework/unmanaged-api/hosting/iclrgcmanager-getstats-method.md)方法要求将`Flags``COR_GC_STATS`结构字段设置为[COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md)枚举的一个或多个值，以指定要设置的统计信息。  
  
 下表将此结构提供的统计信息映射到两[COR_GC_STAT_TYPES](../../../../docs/framework/unmanaged-api/hosting/cor-gc-stat-types-enumeration.md)枚举值`COR_GC_COUNTS`和`COR_GC_MEMORYUSAGE`。  
  
|由COR_GC_COUNTS指定|由COR_GC_MEMORYUSAGE指定|  
|----------------------------------|---------------------------------------|  
|`ExplicitGCCount`<br /><br /> `GenCollectionsTaken`|`CommittedKBytes`<br /><br /> `ReservedKBytes`<br /><br /> `Gen0HeapSizeKBytes`<br /><br /> `Gen1HeapSizeKBytes`<br /><br /> `Gen2HeapSizeKBytes`<br /><br /> `LargeObjectHeapSizeKBytes`<br /><br /> `KBytesPromotedFromGen0`<br /><br /> `KBytesPromotedFromGen1`|  
  
 使用的示例如下：  
  
```cpp  
COR_GC_STATS GCStats;  
GCStats.Flags = COR_GC_COUNTS | COR_GC_MEMORYUSAGE;  
pCLRGCManager->GetStats(&GCStats);  
```  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标题：** GCHost.idl  
  
 **库：** 作为资源包含在 MSCorEE.dll 中  
  
 **.NET 框架版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [承载结构](../../../../docs/framework/unmanaged-api/hosting/hosting-structures.md)
- [自动内存管理](../../../standard/automatic-memory-management.md)
- [垃圾回收](../../../standard/garbage-collection/index.md)
