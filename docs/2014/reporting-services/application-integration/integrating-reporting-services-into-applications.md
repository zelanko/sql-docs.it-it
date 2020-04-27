---
title: Integrazione di Reporting Services nelle applicazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- integrating reports [Reporting Services]
- custom applications [SSRS]
- Reporting Services, application integration
- application integration [Reporting Services]
- reports [Reporting Services], integrating
ms.assetid: 49eb539c-d89b-4291-839a-0ec1a65cd270
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9ad6d24495bb44a7bd1013dbc822eefe346f02d3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63126149"
---
# <a name="integrating-reporting-services-into-applications"></a>Integrazione di Reporting Services nelle applicazioni
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è una piattaforma di creazione di report aperta ed estendibile progettata per fornire agli sviluppatori un set completo di API per lo sviluppo di soluzioni.  
  
 Sono disponibili tre opzioni per l'integrazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] di nelle applicazioni personalizzate: il servizio Web ReportServer, noto anche come API [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SOAP, i controlli ReportViewer per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]e l'accesso con URL. Ogni opzione fornisce un approccio diverso per l'integrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni.  
  
## <a name="report-server-web-service"></a>servizio Web ReportServer  
 Il servizio Web ReportServer è l'interfaccia principale per lo sviluppo in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Sia che si sviluppi codice per gestire il catalogo di report o che si sviluppi codice per il rendering dei report in un formato supportato, il servizio Web espone tutti i metodi necessari per integrare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni. Un esempio di tale applicazione è costituito da Gestione report, incluso in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], che usa il servizio Web per la gestione del database del server di report.  
  
## <a name="reportviewer-controls-for-visual-studio"></a>Controlli ReportViewer per Visual Studio  
 I controlli ReportViewer inclusi in [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] vengono utilizzati per l'integrazione delle funzionalità di visualizzazione dei report nelle applicazioni. Sono disponibili due controlli, uno per le applicazioni basate su Windows Form e uno per le applicazioni Web Form. Ogni controllo fornisce funzionalità per la visualizzazione dei report distribuiti in un server di report e consente di eseguire il rendering dei report presenti in un ambiente in cui non è stato installato un server di report.  
  
## <a name="url-access"></a>Accesso con URL  
 L'accesso con URL rappresenta un'altra opzione per l'integrazione delle funzionalità di visualizzazione dei report nelle applicazioni se non sono disponibili i controlli ReportViewer. L'accesso con URL è inoltre utile per inviare agli utenti collegamenti ai report tramite posta elettronica.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Integrazione di Reporting Services tramite SOAP](../application-integration/integrating-reporting-services-using-soap.md)  
 Viene descritto come integrare le funzionalità di navigazione e gestione dei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni aziendali esistenti utilizzando il servizio Web ReportServer.  
  
 [Integrazione di Reporting Services tramite i controlli ReportViewer](../application-integration/integrating-reporting-services-using-reportviewer-controls.md)  
 Viene descritto come integrare le funzionalità di visualizzazione dei report nelle applicazioni esistenti utilizzando i controlli ReportViewer.  
  
 [Integrazione di Reporting Services tramite l'accesso con URL](../application-integration/integrating-reporting-services-using-url-access.md)  
 Viene descritto come integrare le funzionalità di navigazione dei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni esistenti utilizzando l'accesso con URL.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Scelta tra accesso con URL e SOAP](../../../2014/reporting-services/application-integration/choosing-between-url-access-and-soap.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../../2014/reporting-services/technical-reference-ssrs.md)   
 [Servizio Web ReportServer](../report-server-web-service/report-server-web-service.md)  
  
  
