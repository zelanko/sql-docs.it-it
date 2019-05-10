---
title: Pagina Configurazione Web (Gestione configurazione Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8e9036bbff7302a0580bcbc5370ba8c6e9f7835a
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65485522"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Pagina Configurazione Web (Gestione configurazione Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Usare la pagina **Configurazione Web** per configurare il sito Web e l'applicazione Web. È anche possibile abilitare Data Quality Services.  
  
## <a name="configure-the-web-application"></a>Configurare l'applicazione Web  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Sito Web**|Creare un nuovo sito Web, selezionare il sito Web predefinito o selezionare un altro sito disponibile (se elencato). In questo elenco vengono visualizzati i siti Web definiti in Internet Information Services (IIS) nel computer locale. Quando si crea un nuovo sito Web, viene creata automaticamente una nuova applicazione Web. Quando si seleziona il valore predefinito o un altro sito esistente, è necessario creare manualmente un'applicazione.|  
|**Applicazione Web**|Selezionare un'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] per la configurazione. In questa casella vengono visualizzate solo le applicazioni Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] incluse nel sito Web selezionato.<br /><br /> Se viene visualizzato nulla, fare clic su **Crea** per creare un sito Web.|  
|**Crea**|Consente di aprire la finestra di dialogo **Crea applicazione Web** dalla quale è possibile creare un'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] nel sito selezionato. Questo pulsante viene abilitato solo quando il sito selezionato non contiene un'applicazione Web radice configurata come applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
  
## <a name="associate-application-with-database"></a>Associare un'applicazione a un database  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Select**|Consente di aprire la finestra di dialogo **Connetti al server** dalla quale è possibile connettersi a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selezionare un database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] da associare all'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionata.|  
|**Istanza di SQL Server**|Consente di visualizzare il nome dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] selezionata che ospita il database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Non viene visualizzato alcun nome finché non ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e si seleziona un database.|  
|**Database**|Consente di visualizzare il nome del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] associato all'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selezionata. Non viene visualizzato alcun nome finché non ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e si seleziona un database.|  
  
## <a name="enable-dqs-integration"></a>Abilitare l'integrazione DQS  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Abilitare l'integrazione con Data Quality Services**|Selezionare questa opzione per abilitare le funzionalità di Data Quality Services disponibili nel [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Per altre informazioni, vedere [Abilitare l'integrazione di Data Quality Services con Master Data Services](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## <a name="see-also"></a>Vedere anche  
[Installazione e configurazione di Master Data Services](../master-data-services/master-data-services-installation-and-configuration.md) [Requisiti dell'applicazione Web &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
