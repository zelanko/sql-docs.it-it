---
title: Estensioni di Reporting Services | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- SQL Server Reporting Services, extending
- extensions [Reporting Services], about extensions
- SSIS, extending
- Reporting Services, extending
- extensions [Reporting Services]
ms.assetid: 2bf17ae4-2292-4a58-a1f0-56e99abd9b69
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d0cf0ab94a17883f9721701b13725e34745a7875
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "63193819"
---
# <a name="reporting-services-extensions"></a>Estensioni di Reporting Services
  L'architettura modulare di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è progettata per offrire estendibilità. È disponibile un'API in codice gestito che consente di sviluppare, installare e gestire in modo semplice le estensioni usate da numerosi componenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . È possibile creare assembly privati o condivisi usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e aggiungere nuove funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per soddisfare le esigenze aziendali in continua evoluzione.  
  
 L'architettura unica di estendibilità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] consente agli sviluppatori di estendere caratteristiche specifiche del prodotto e dei relativi componenti. Attualmente, è disponibile ampio supporto per l'estensione delle funzionalità di elaborazione dati di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. L'API di elaborazione dati include convenzioni e costrutti del provider di dati [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] comuni che consentono agli sviluppatori di compilare funzionalità aggiuntive di elaborazione dati in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Queste estensioni per l'elaborazione dati aggiungono funzionalità sia al server di report che a Progettazione report e consentono una perfetta integrazione dei dati personalizzati nei report.  
  
 Un'altra estensione supportata è quella per il recapito. L'API di recapito è completamente integrata nell'architettura di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e consente l'utilizzo di un'ampia gamma di meccanismi di recapito per l'invio di notifiche dei report agli utenti. È possibile estendere il server di report per offrire agli utenti recapito personalizzato, nonché estendere le pagine di gestione delle sottoscrizioni di Gestione report per consentite l'utilizzo di estensioni per il recapito personalizzate per le sottoscrizioni.  
  
 Un'altra estensione del server di report, RDCE (Report Definition Customization Extension) consente di personalizzare in modo dinamico la definizione di un report prima che venga passata al motore di elaborazione. È possibile personalizzare i report in base a fattori come gli utenti o le lingue. È ad esempio possibile implementare viste diverse per utenti diversi, ad esempio amministratori o membri di un reparto, oppure personalizzare un report con layout diversi a seconda che ne venga eseguito il rendering in francese o in arabo.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Considerazioni sulla sicurezza per le estensioni](../../reporting-services/extensions/security-considerations-for-extensions.md)  
 Vengono descritti i problemi di sicurezza relativi allo sviluppo e alla distribuzione delle estensioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementazione di un'estensione per l'elaborazione dati](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)  
 Vengono descritti i requisiti e i passaggi per l'implementazione di un'estensione per l'elaborazione dati per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementazione di un'estensione per il recapito](../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)  
 Vengono descritti i requisiti e i passaggi per l'implementazione di un'estensione per il recapito per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Implementazione di un'estensione per il rendering](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)  
 Viene fornita un'introduzione allo sviluppo delle estensioni per il rendering.  
  
 [Implementazione di un'estensione di sicurezza](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  
 Vengono descritti i requisiti e i passaggi per l'implementazione di un'estensione di sicurezza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Libreria di estensioni di Reporting Services](../../reporting-services/extensions/reporting-services-extension-library.md)  
 Vengono forniti riferimenti per la programmazione per la libreria di API di estensione per le caratteristiche di estendibilità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
  
