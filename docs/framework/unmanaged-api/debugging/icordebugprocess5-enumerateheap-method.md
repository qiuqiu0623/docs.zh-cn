---
title: ICorDebugProcess5::EnumerateHeap 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.EnumerateHeap
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::EnumerateHeap
helpviewer_keywords:
- EnumerateHeap method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::EnumerateHeap method [.NET Framework debugging]
ms.assetid: b0192104-6073-4089-a4df-dc29ee033074
topic_type:
- apiref
ms.openlocfilehash: 780f9eb0984e35c4487d770b5e7ff33917cf07ed
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2020
ms.locfileid: "76792417"
---
# <a name="icordebugprocess5enumerateheap-method"></a>ICorDebugProcess5::EnumerateHeap 方法
获取托管堆上的对象的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT EnumerateHeap(  
    [out] ICorDebugHeapEnum **ppObjects  
);  
```  
  
## <a name="parameters"></a>参数  
 `ppObject`  
 弄指向[ICorDebugHeapEnum](icordebugheapenum-interface.md)接口对象地址的指针，该接口对象是驻留在托管堆上的对象的枚举器。  
  
## <a name="remarks"></a>备注  
 在调用 `ICorDebugProcess5::EnumerateHeap` 方法之前，应调用[ICorDebugProcess5：： GetGCHeapInformation](icordebugprocess5-getgcheapinformation-method.md)方法，并检查返回的[COR_HEAPINFO](cor-heapinfo-structure.md)对象的 `areGCStructuresValid` 字段的值，以确保其当前状态的垃圾回收堆可枚举。 此外，如果在进程的生存期内附加过早，则 `ICorDebugProcess5::EnumerateHeap` 返回 `E_FAIL`，在分配托管堆的内存之前。  
  
 [ICorDebugHeapEnum](icordebugheapenum-interface.md)接口对象是从 ICorDebugEnum 接口派生的标准枚举器，该枚举器可用于枚举[COR_HEAPOBJECT](cor-heapobject-structure.md)的对象。 此方法用提供所有对象的相关信息[COR_HEAPOBJECT](cor-heapobject-structure.md)实例填充[ICorDebugHeapEnum](icordebugheapenum-interface.md)集合对象。 集合还可以包含[COR_HEAPOBJECT](cor-heapobject-structure.md)实例，这些实例提供有关非对象的根对象，但未被垃圾回收器收集的对象的信息。  
  
## <a name="requirements"></a>需求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [ICorDebugProcess5 接口](icordebugprocess5-interface.md)
- [调试接口](debugging-interfaces.md)
