---
title: Associare un'applicazione Web e un database Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bdd616e6eb59a7db1c22b7007e04db91a288a20a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482970"
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>Associare un'applicazione Web e un database Master Data Services
  Associare l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] a un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] per specificare il database da usare per le operazioni Web.  
  
## <a name="prerequisites"></a>Prerequisiti  
  
-   [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] deve essere installato nel computer locale. Per altre informazioni, vedere [Install Master Data Services](install-master-data-services.md)(Installare Master Data Services).  
  
-   È necessario che sia disponibile un'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] locale. Per altre informazioni, vedere [Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md).  
  
-   È necessario che sia disponibile un database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] locale o remoto. Per altre informazioni, vedere [Creare un database Master Data Services](create-a-master-data-services-database.md).  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>Per associare un'applicazione Web e un database Master Data Services  
  
1.  Aprire [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  Nel riquadro sinistro fare clic su **Configurazione Web**.  
  
3.  Nell'elenco **Sito Web** della pagina **Configurazione Web**, in **Applicazione Web** selezionare il sito Web in cui è inclusa l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
4.  Nella casella **Applicazione Web** selezionare l'applicazione Web in cui è ospitato [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].  
  
5.  In **Associare l'applicazione al database**fare clic su **Seleziona**. Verrà visualizzata la finestra di dialogo **Connetti al database** .  
  
6.  Specificare le informazioni di connessione per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e fare clic su **Connetti**.  
  
7.  Nell'elenco **Database Master Data Services** selezionare il database che si desidera associare all'applicazione Web, quindi scegliere **OK**.  
  
8.  In **Associare l'applicazione al database**verificare che l'istanza e le informazioni del database siano corrette, quindi fare clic su **Applica**.  
  
## <a name="next-steps"></a>Passaggi successivi  
  
-   L'accesso a livello di programmazione ai servizi Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , viene abilitato automaticamente durante la creazione dell'applicazione Web. Per consentire agli sviluppatori di accedere ai metadati del servizio al fine di generare in modo semplice classi proxy per l'accesso a livello di codice, abilitare la pubblicazione dei metadati. Per altre informazioni, vedere [Creare le classi proxy del servizio Web Gestione dati master](../develop/create-master-data-manager-web-service-proxy-classes.md).  
  
-   Aggiungere utenti e gruppi a [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Se a nessun utente o gruppo è stato concesso l'accesso a [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], è necessario aprire [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] utilizzando le credenziali di amministratore del sistema [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Per altre informazioni, vedere [Amministratori &#40;Master Data Services&#41;](../administrators-master-data-services.md) e [Utenti e gruppi &#40;Master Data Services&#41;](../users-and-groups-master-data-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Install Master Data Services](install-master-data-services.md)   
 [Pagina Configurazione Web &#40;Gestione configurazione Master Data Services&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
