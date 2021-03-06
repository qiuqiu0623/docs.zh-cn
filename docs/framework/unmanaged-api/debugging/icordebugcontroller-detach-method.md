---
title: ICorDebugController::Detach 方法
ms.date: 03/30/2017
api_name:
- ICorDebugController.Detach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Detach
helpviewer_keywords:
- Detach method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Detach method [.NET Framework debugging]
ms.assetid: 06fae364-f2c6-4a50-aa7e-3da9f2684dc3
topic_type:
- apiref
ms.openlocfilehash: b98077914d680c908587649fdd517aca9c8dcd40
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73125428"
---
# <a name="icordebugcontrollerdetach-method"></a>ICorDebugController::Detach 方法
将调试器与进程或应用程序域分离。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT Detach ();  
```  
  
## <a name="remarks"></a>备注  
 进程或应用程序域将继续正常执行，但 "ICorDebugProcess" 或 "ICorDebugAppDomain" 对象不再有效，且不会发生进一步的回调。  
  
 在 .NET Framework 版本2.0 中，如果启用了非托管调试，则此方法将因操作系统限制而失败。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅
