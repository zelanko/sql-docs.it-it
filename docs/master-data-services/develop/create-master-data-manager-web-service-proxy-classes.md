---
title: Creare le classi proxy del servizio Web Gestione dati master
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d0313c5dd8fcb1dd8dac5bc436bdf024d044dd5a
ms.sourcegitcommit: 903856818acc657e5c42faa16d1c770aeb4e1d1b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2020
ms.locfileid: "83730520"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Creare le classi proxy del servizio Web Gestione dati master

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Il servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] consente di utilizzare a livello di codice le caratteristiche di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] da qualsiasi computer che può accedere al sito Web di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Prima di iniziare a scrivere il codice per accedere al servizio Web, è necessario generare le classi proxy. La classe proxy principale utilizzata per eseguire le operazioni del servizio Web è la classe <xref:Microsoft.MasterDataServices.ServiceClient>, che implementa l'interfaccia <xref:Microsoft.MasterDataServices.IService>.  
  
## <a name="enable-web-service-metadata-publishing"></a>Abilitare la pubblicazione dei metadati del servizio Web  
 Prima di generare le classi proxy, è necessario abilitare la pubblicazione dei metadati del servizio Web. A tale scopo, effettuare le operazioni seguenti:  
  
1.  Aprire il file Web.config di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in un editor di testo. Il file Web.config si trova nella cartella WebApplication del percorso di installazione di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Trovare la sezione **mdsWsHttpBehavior** in **\<serviceBehaviors>**. Per l'elemento ** \<>serviceMetadata** , impostare **HttpGetEnabled** su **true**.  
  
    > [!NOTE]  
    >  Se si desidera abilitare i servizi Web tramite Transport Layer Security (TLS), precedentemente noti come Secure Sockets Layer (SSL), impostare **HttpsGetEnabled** su **true** nella sezione **mdsWsHttpBehavior** del file web.config. È anche necessario modificare **mdsWsHTTPBinding** in modo che sia configurato anche per TLS e impostare come commento la sezione non TLS.  
  
3.  Salvare le modifiche apportate al file.  
  
4.  Testare la pubblicazione dei metadati passando all'URL del servizio, ad esempio: `https://yourserver/MDS/service/service.svc`. Se la pubblicazione dei metadati è abilitata, viene visualizzata una pagina che inizia con   
    "È stato creato un servizio".  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Creazione di classi proxy tramite Visual Studio  
 Se è installato Visual Studio 2010, il modo più semplice per generare le classi proxy è aggiungere un **Riferimento al servizio** al progetto. L'indirizzo del riferimento al servizio è l'URL dell'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aggiunto a /service/service.svc, Ad esempio: `https://yourserver/MDS/service/service.svc`. Per altre informazioni, vedere [Procedura: Aggiungere, aggiornare o rimuovere un riferimento al servizio](https://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Creazione di classi proxy tramite Svcutil.exe  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] Per avere Svcutil.exe nel computer in uso, è necessario che sia installato il Windows SDK. Se si utilizza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], per eseguire il comando sarà necessario utilizzare il prompt dei comandi di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per altre informazioni, vedere [Strumento ServiceModel Metadata Utility (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) e [Generazione di un client WCF dai metadati del servizio](https://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Per creare un set di classi proxy in C# tramite Svcutil.exe, utilizzare un comando analogo al seguente:  
  
```  
svcutil.exe https://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Dove:  
  
-   *servername*:*port* corrispondono al nome del computer e al numero della porta del computer host di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
-   *virtual_path* è il percorso virtuale di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] in Internet Information Services (IIS).  
  
-   *proxy_name* è il nome del file proxy generato.  
  
## <a name="see-also"></a>Vedere anche  
 [Operazioni del servizio Web per categoria &#40;Master Data Services&#41;](../../master-data-services/develop/categorized-web-service-operations-master-data-services.md)  
  
  
