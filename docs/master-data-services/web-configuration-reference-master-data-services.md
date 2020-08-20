---
description: Guida di riferimento alla configurazione Web (Master Data Services)
title: Guida di riferimento alla configurazione Web
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- web configuration file [Master Data Services]
ms.assetid: b8cc9a35-97ab-4fe0-ab4b-c07f13d9793a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 34e3e849a86cb23c3974b32b9d3d8c0721601274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456762"
---
# <a name="web-configuration-reference-master-data-services"></a>Guida di riferimento alla configurazione Web (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] usa un file Web.config per le impostazioni di configurazione che consentono a Internet Information Services (IIS) di ospitare il servizio Web e l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Questo file Web.config si trova nella cartella WebApplication nel percorso di installazione [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Per altre informazioni sul percorso e le autorizzazioni, vedere [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md).  
  
## <a name="webconfig-elements"></a>Elementi di Web.Config  
 Il file di Web.config contiene un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] elemento personalizzato, **\<masterDataServices>** , oltre agli elementi di configurazione standard IIS, .NET Framework, ASP.NET e Windows Communication Foundation (WCF). Nella tabella seguente vengono descritti gli elementi inclusi nel file Web.config.  
  
|Elemento di configurazione|Descrizione|  
|---------------------------|-----------------|  
|**masterDataServices**|Elemento Custom. Connette il servizio Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] a un database di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**connectionStrings**|Elemento ASP.NET. Per altre informazioni, vedere [Elemento connectionStrings (schema delle impostazioni ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178347) in MSDN Library.|  
|**System. Web**|Elemento ASP.NET. Per altre informazioni, vedere [Elemento system.web (schema delle impostazioni ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178348) in MSDN Library.|  
|**avvio**|Elemento .NET Framework. Per ulteriori informazioni, vedere l' [ \<startup> elemento](https://go.microsoft.com/fwlink/?LinkId=178349) in MSDN Library.|  
|**Runtime**|Elemento .NET Framework. Per ulteriori informazioni, vedere l' [ \<runtime> elemento](https://go.microsoft.com/fwlink/?LinkId=178350) in MSDN Library.|  
|**system.codedom**|Elemento .NET Framework. Per ulteriori informazioni, vedere l' [ \<system.codedom> elemento](https://go.microsoft.com/fwlink/?LinkId=178351) in MSDN Library.|  
|**System. Web. Extensions**|Elemento ASP.NET. Per altre informazioni, vedere [Elemento system.web.extensions (schema delle impostazioni ASP.NET)](https://go.microsoft.com/fwlink/?LinkId=178352) in MSDN Library.|  
|**system.webServer**|Gruppo di sezioni che contiene gli elementi IIS. Per altre informazioni, vedere [system.webServer Section Group \[IIS 7 Settings Schema\]](https://go.microsoft.com/fwlink/?LinkId=178353) (Gruppo di sezioni system.webServer (schema delle impostazioni IIS 7)) in MSDN Library.|  
|**system.serviceModel**|Elemento WCF. Per ulteriori informazioni, vedere [\<system.serviceModel>](https://go.microsoft.com/fwlink/?LinkId=178354) in MSDN Library.|  
|**system.diagnostics**|Elemento .NET Framework. Per ulteriori informazioni, vedere l' [ \<system.diagnostics> elemento](https://go.microsoft.com/fwlink/?LinkId=178355) in MSDN Library.|  
|**appSettings**|Elemento ASP.NET. Per altre informazioni, vedere [Elemento appSettings (schema delle impostazioni generali)](https://go.microsoft.com/fwlink/?LinkId=178356) in MSDN Library.|  
  
## <a name="masterdataservices-element"></a>Elemento masterdataservices  
 L' **\<masterDataServices>** elemento è un elemento personalizzato usato per connettere un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] servizio Web a un [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database.  
  
### <a name="syntax"></a>Sintassi  
  
```  
<masterDataServices>  
   <instance virtualPath="path" siteName="name" connectionName="name" serviceName="name" />  
</masterDataServices>  
```  
  
### <a name="elements-and-attributes"></a>Elementi e attributi  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|**instance**|Elemento figlio. Contiene gli attributi che specificano le informazioni per la stringa di connessione al database e al servizio Web.|  
|**virtualPath**|Attributo. Specifica il percorso virtuale del servizio e dell'applicazione Web di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Corrisponde all'attributo **path** dell' **\<application>** elemento sotto l' **\<site>** elemento nel file di ApplicationHost.config IIS.|  
|**siteName**|Attributo. Specifica il nome del sito che ospita il servizio e l'applicazione Web di [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Corrisponde all'attributo **Name** dell' **\<site>** elemento **\<sites>** in nel file di ApplicationHost.config IIS.|  
|**connectionName**|Attributo. Specifica il nome della connessione da utilizzare. Corrisponde all'attributo **Name** dell' **\<add>** elemento sotto l' **\<connectionStrings>** elemento in Web.config.|  
|**serviceName**|Attributo. Specifica il nome del servizio Web. Corrisponde all'attributo **Name** dell' **\<service>** elemento sotto l' **\<services>** elemento in Web.config.|  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato un servizio denominato MDS1 nel sito di Contoso e nel percorso /MDS mediante una stringa di connessione specificata da MDSDB.  
  
```  
<masterDataServices>  
   <instance virtualPath="/MDS" siteName="Contoso" connectionName="MDSDB" serviceName="MDS1" />  
</masterDataServices>  
```  
  
  
