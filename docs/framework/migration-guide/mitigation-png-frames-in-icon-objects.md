---
title: 缓解操作：图标对象中的 PNG 帧
ms.date: 03/30/2017
ms.assetid: ca87fefb-7144-4b4e-8832-5a939adbb4b2
ms.openlocfilehash: d661e45bfbbe5e1c5ca5b7eb123e71aa32a096ca
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2020
ms.locfileid: "79181225"
---
# <a name="mitigation-png-frames-in-icon-objects"></a>缓解操作：图标对象中的 PNG 帧
从 .NET Framework 4.6 开始， <xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> 方法成功将带 PNG 帧的图标转换为 <xref:System.Drawing.Bitmap> 对象。  
  
 在面向 .NET Framework 4.5.2 和更早版本的应用中，<xref:System.Drawing.Icon.ToBitmap%2A?displayProperty=nameWithType> 方法在 <xref:System.ArgumentOutOfRangeException> 对象具有 PNG 帧时引发 <xref:System.Drawing.Icon> 异常。  
  
## <a name="impact"></a>影响  
 此更改会影响以下应用：重新编译为面向 .NET Framework 4.6 的应用，以及对在 <xref:System.ArgumentOutOfRangeException> 对象具有 PNG 帧时引发的 <xref:System.Drawing.Icon> 实施特殊处理的应用。 在.NET Framework 4.6 下运行时，转换成功，不再引发 <xref:System.ArgumentOutOfRangeException> ，因此不再调用异常处理程序。  
  
### <a name="mitigation"></a>缓解操作  
 如果不需要此行为，可以在 app.config 文件的 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 部分中添加下面的元素，从而保留旧行为：  
  
```xml  
<AppContextSwitchOverrides
      value="Switch.System.Drawing.DontSupportPngFramesInIcons=true" />  
```  
  
 如果 app.config 文件中已包含 `AppContextSwitchOverrides` 元素，则新的值应与以下形式的 `value` 特性合并：  
  
```xml  
<AppContextSwitchOverrides
      value="Switch.System.Drawing.DontSupportPngFramesInIcons=true;<previous key>=<previous value>" />  
```  
  
## <a name="see-also"></a>另请参阅

- [应用程序兼容性](application-compatibility.md)
