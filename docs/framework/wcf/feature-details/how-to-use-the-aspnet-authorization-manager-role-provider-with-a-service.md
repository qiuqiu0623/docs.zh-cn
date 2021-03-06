---
title: 如何：将 ASP.NET 授权管理器角色提供程序与服务一起使用
ms.date: 03/30/2017
ms.assetid: f21deb81-91ef-49ef-94d6-494785143271
ms.openlocfilehash: 009b96defdf27591ddb98afaa684745b5fcbe0d4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184801"
---
# <a name="how-to-use-the-aspnet-authorization-manager-role-provider-with-a-service"></a>如何：将 ASP.NET 授权管理器角色提供程序与服务一起使用
当ASP.NET托管 Web 服务时，可以将授权管理器集成到应用程序中，以向服务提供授权。 授权管理器允许应用程序开发人员定义各个操作，这些操作可组织在一起形成任务。 然后管理员可以授权角色执行特定任务或各个操作。 授权管理器提供管理工具，并将其作为 Microsoft 管理控制台 (MMC) 管理单元来管理角色、任务、操作和用户。 管理员在 XML 文件、Active Directory 或 Active Directory 应用程序模式 (ADAM) 存储区中配置授权管理器策略存储区。  
  
 授权管理器通过为托管 Web 服务ASP.NET应用程序配置授权管理器ASP.NET角色提供程序集成到应用程序中。 与其他ASP.NET角色提供程序一样，授权管理器ASP.NET角色提供程序使用<>`providers`元素进行配置。  
  
 下面的代码示例是 Web 服务配置文件的一部分，该 Web 服务将授权管理器集成到应用程序中。  
  
```xml  
<system.web>  
    <roleManager enabled="true" defaultProvider="AzManRoleProvider">  
      <providers>  
        <add name="AzManRoleProvider"  
             type="System.Web.Security.AuthorizationStoreRoleProvider, System.Web, Version=2.0.0.0, Culture=neutral, publicKeyToken=b03f5f7f11d50a3a"  
             connectionStringName="AzManPolicyStoreConnectionString"
             applicationName="SecureService"/>  
      </providers>  
    </roleManager>  
</system.web>  
```  
  
 有关将ASP.NET角色提供程序与 WCF 应用程序集成的详细信息，请参阅[：将ASP.NET角色提供程序与服务一起](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)使用。 有关将授权管理器与ASP.NET一起使用的详细信息，请参阅[：将授权管理器 （AzMan） 与 2.0 ASP.NET 。](https://docs.microsoft.com/previous-versions/msp-n-p/ff649313(v=pandp.10))  
  
## <a name="see-also"></a>另请参阅

- [如何：将 ASP.NET 角色提供程序与服务一起使用](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-role-provider-with-a-service.md)
