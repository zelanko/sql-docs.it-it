---
title: Creare le classi proxy del servizio Web Gestione dati master | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 8bdab026-a0c0-41f3-9d36-f3919c23247f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c44e1830b1f04b1a7686bf7db1efea4549ae143e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479546"
---
# <a name="create-master-data-manager-web-service-proxy-classes"></a>Creare le classi proxy del servizio Web Gestione dati master
  Il servizio Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] consente di utilizzare a livello di codice le caratteristiche di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] da qualsiasi computer che può accedere al sito Web di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Prima di iniziare a scrivere il codice per accedere al servizio Web, è necessario generare le classi proxy. La classe proxy principale utilizzata per eseguire le operazioni del servizio Web è la classe <xref:Microsoft.MasterDataServices.ServiceClient>, che implementa l'interfaccia <xref:Microsoft.MasterDataServices.IService>.  
  
## <a name="enable-web-service-metadata-publishing"></a>Abilitare la pubblicazione dei metadati del servizio Web  
 Prima di generare le classi proxy, è necessario abilitare la pubblicazione dei metadati del servizio Web. A tale scopo, effettuare le operazioni seguenti:  
  
1.  Aprire il file Web.config di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] in un editor di testo. Il file Web.config si trova nella cartella WebApplication del percorso di installazione di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Trovare la `mdsWsHttpBehavior` sezione in ** \<serviceBehaviors>**. Per l' ** \<elemento>serviceMetadata** , impostare `httpGetEnabled` su `true`.  
  
    > [!NOTE]  
    >  Se si desidera abilitare servizi Web tramite Secure Sockets Layer (SSL), impostare invece `httpsGetEnabled` su `true` nella sezione `mdsWsHttpBehavior` del file web.config. È inoltre necessario modificare `mdsWsHTTPBinding` in modo tale che sia configurato per SSL e impostare come commento la sezione non SSL.  
  
3.  Salvare le modifiche apportate al file.  
  
4.  Testare la pubblicazione dei metadati passando all'URL del servizio, ad esempio: http://yourserver/MDS/service/service.svc. Se la pubblicazione dei metadati è abilitata, viene visualizzata una pagina che inizia con   
    "È stato creato un servizio".  
  
## <a name="creating-proxy-classes-by-using-visual-studio"></a>Creazione di classi proxy tramite Visual Studio  
 Se è installato Visual Studio 2010, il modo più semplice per generare le classi proxy è aggiungere un **Riferimento al servizio** al progetto. L'indirizzo del riferimento al servizio è l'URL dell'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] aggiunto a /service/service.svc, Ad esempio: http://yourserver/MDS/service/service.svc. Per altre informazioni, vedere [Procedura: Aggiungere, aggiornare o rimuovere un riferimento al servizio](https://go.microsoft.com/fwlink/?LinkId=221167).  
  
## <a name="creating-proxy-classes-by-using-svcutilexe"></a>Creazione di classi proxy tramite Svcutil.exe  
 Per avere Svcutil. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] exe nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] computer in uso, è necessario che sia installato il Windows SDK o. Se si utilizza [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], per eseguire il comando sarà necessario utilizzare il prompt dei comandi di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per altre informazioni, vedere [Strumento ServiceModel Metadata Utility (Svcutil.exe)](https://go.microsoft.com/fwlink/?LinkId=165027) e [Generazione di un client WCF dai metadati del servizio](https://go.microsoft.com/fwlink/?LinkId=164821).  
  
 Per creare un set di classi proxy in C# tramite Svcutil.exe, utilizzare un comando analogo al seguente:  
  
```  
svcutil.exe http://<server_name:port>/<virtual_path>/Service/Service.svc   
/out:<proxy_name>.cs /messageContract /tcv:Version35   
/noconfig /ct:System.Collections.ObjectModel.Collection`1   
/namespace:*,Microsoft.MasterDataServices  
```  
  
 Dove:  
  
-   *nomeserver*: la*porta* è il nome del computer e il numero di porta del [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]computer che ospita.  
  
-   *virtual_path* è il percorso virtuale di [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] in Internet Information Services (IIS).  
  
-   *proxy_name* è il nome del file proxy generato.  
  
## <a name="see-also"></a>Vedere anche  
 [Operazioni del servizio Web categorizzate &#40;Master Data Services&#41;](categorized-web-service-operations-master-data-services.md)  
  
  
