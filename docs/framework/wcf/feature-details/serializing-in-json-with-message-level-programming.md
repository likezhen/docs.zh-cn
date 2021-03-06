---
title: 使用消息级编程在 Json 中序列化
ms.date: 03/30/2017
ms.assetid: 5f940ba2-57ee-4c49-a779-957c5e7e71fa
ms.openlocfilehash: 36459dbc0ddee883678a98a27f9abb74fde78e86
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184500"
---
# <a name="serializing-in-json-with-message-level-programming"></a>使用消息级编程在 Json 中序列化
WCF 支持以 JSON 格式序列化数据。 本主题描述如何使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 告知 WCF 序列化您的类型。  
  
## <a name="typed-message-programming"></a>类型化的消息编程  
 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 或 <xref:System.ServiceModel.Web.WebGetAttribute> 应用于服务操作时使用 <xref:System.ServiceModel.Web.WebInvokeAttribute>。 这两个属性允许您指定 `RequestFormat` 和 `ResponseFormat`。 使用 JSON 进行请求和响应。 将两者设置为`WebMessageFormat.Json`。  要使用 JSON，必须使用 自动配置<xref:System.ServiceModel.WebHttpBinding>的<xref:System.ServiceModel.Description.WebHttpBehavior>。 有关 WCF 序列化的详细信息，请参阅[序列化和反序列化](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md)。 有关 JSON 和 WCF 的详细信息，请参阅[服务站 - 使用 WCF 提供 RESTful 服务简介](https://docs.microsoft.com/archive/msdn-magazine/2009/january/service-station-an-introduction-to-restful-services-with-wcf)。  
  
> [!IMPORTANT]
> 使用 JSON 需要使用 <xref:System.ServiceModel.WebHttpBinding> 和 <xref:System.ServiceModel.Description.WebHttpBehavior>，这两者不支持 SOAP 通信。 与 通信的服务<xref:System.ServiceModel.WebHttpBinding>不支持公开服务元数据，因此您将无法使用 Visual Studio 的"添加服务参考"功能或 svcutil 命令行工具生成客户端代理。 有关如何以编程方式调用使用<xref:System.ServiceModel.WebHttpBinding>的服务的详细信息，请参阅如何使用[WCF 使用 REST 服务](https://docs.microsoft.com/archive/blogs/pedram/how-to-consume-rest-services-with-wcf)。  
  
## <a name="untyped-message-programming"></a>非类型化的消息编程  
 当直接使用非类型化的消息对象时，您必须显式设置非类型化消息的属性，以便将其序列化为 JSON。 下面的代码段演示如何执行此操作。  
  
```csharp
 Message response = Message.CreateMessage(  
                  MessageVersion.None,    // No SOAP message version  
                             "*",                     // SOAP action, ignored since this is JSON  
                             "Response string: JSON format specified", // Message body  
                             new DataContractJsonSerializer(typeof(string))); // Specify DataContractJsonSerializer  
      response.Properties.Add( WebBodyFormatMessageProperty.Name,
                    new WebBodyFormatMessageProperty(WebContentFormat.Json)); // Use JSON format  
```  
  
## <a name="see-also"></a>另请参阅

- [AJAX 集成和 JSON 支持](../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)
- [独立 JSON 序列化](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md)
- [JSON 序列化](../../../../docs/framework/wcf/samples/json-serialization.md)
