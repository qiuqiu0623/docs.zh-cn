---
ms.openlocfilehash: a02887327390afb6859c0d5f78a8875bff9539e6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2020
ms.locfileid: "70997558"
---
### <a name="product-versioning-changes-in-the-net-framework-46-and-later-versions"></a>.NET Framework 4.6 和更高版本中产品版本控制的更改

|   |   |
|---|---|
|详细信息|产品版本控制已从早期版本的 .NET Framework 进行了更改，特别是 .NET Framework 4、4.5、4.5.1 和 4.5.2。 以下是详细更改：<ul><li><code>Version</code> 键的 <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full</code> 项的值在 .NET Framework 4.6 及其子版本中已更改为 <code>4.6.xxxxx</code>，在 .NET Framework 4.7 和 4.7.1 中已更改为 <code>4.7.xxxxx</code>。 在 .NET Framework 4.5、4.5.1 和 4.5.2 中，它的格式为 <code>4.5.xxxxx</code>。</li><li>.NET Framework 文件的文件和产品版本控制在 .NET Framework 4.6 及其子版本中已从 4.0.30319.x 的早期版本控制方案更改为 4.6.X.0，在 .NET Framework 4.7 和 4.7.1 中已更改为 4.7.X.0。 右键单击某个文件后，查看文件的“属性”时可以看到这些新值。</li><li>在 .NET Framework 4.6 及其子版本中，托管程序集的 <xref:System.Reflection.AssemblyFileVersionAttribute> 和 <xref:System.Reflection.AssemblyInformationalVersionAttribute> 特性的版本值格式为 4.6.X.0，在 .NET Framework 4.7 和 4.7.1 中，格式为 4.7.X.0。</li><li>在 .NET Framework 4.6、4.6.1、4.6.2、4.7 和 4.7.1 中，<xref:System.Environment.Version?displayProperty=nameWithType> 属性将返回修正后的版本字符串 <code>4.0.30319.42000</code>。 在 .NET Framework 4、4.5、4.5.1 和 4.5.2 中，它返回格式为 <code>4.0.30319.xxxxx</code> 的版本字符串（例如“4.0.30319.18010”）。 请注意，我们不建议应用程序代码对 Environment.Version 属性产生任何新的依赖关系。</li></ul>有关详细信息，请参阅[如何：确定安装了哪些 .NET Framework 版本](~/docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。|
|建议|一般情况下，应用程序应依赖于用于检测诸如 .NET Framework 的运行时版本和安装目录等内容的推荐技术：<ul><li>若要检测 .NET Framework 的运行时版本，请参阅[如何：确定安装了哪些 .NET Framework 版本](~/docs/framework/migration-guide/how-to-determine-which-versions-are-installed.md)。</li><li>若要确定 .NET Framework 的安装路径，请使用 <code>InstallPath</code> 密钥中的 <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full</code> 条目的值。</li></ul> <blockquote> [!IMPORTANT] 子项名称是 <code>NET Framework Setup</code>，而不是 <code>.NET Framework Setup</code>。</blockquote> <ul><li>若要确定.NET Framework 公共语言运行时的目录路径，请调用 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetRuntimeDirectory?displayProperty=nameWithType> 方法。</li><li>若要获取 CLR 版本，请调用 <xref:System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion?displayProperty=nameWithType> 方法。 对于 .NET Framework 4 及其子版本（.NET Framework 4.5、4.5.1、4.5.2 以及 .NET Framework 4.6、4.6.1、4.6.2、4.7 和 4.7.1），它将返回字符串 v4.0.30319。</li></ul>|
|范围|次要|
|Version|4.6|
|类型|运行时|
