---
title: Problemi di aggiornamento Reporting Services (preparazione aggiornamento) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 75c3bda5d15e3930fcdeba9ca73d70128fd90336
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952065"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Problemi di aggiornamento di Reporting Services (Preparazione aggiornamento)
  Negli argomenti seguenti vengono descritti i problemi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che potrebbero influire sull'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Vengono illustrate le azioni che è possibile eseguire per ridurre l'effetto di queste modifiche nell'ambiente.  
  
 Con Preparazione aggiornamento viene analizzata un'installazione del server di report. Se sono installati solo i componenti client (ad esempio se Progettazione report è l'unico componente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato nel computer), non verrà segnalato alcun problema.  
  
 A seconda della modalità di configurazione dell'installazione, è possibile che vengano rilevati altri problemi non segnalati da Preparazione aggiornamento. Tali problemi non impediscono il corretto aggiornamento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ma possono influire sull'esecuzione di report e applicazioni al termine di un aggiornamento. Per ulteriori informazioni su questi problemi, vedere "Compatibilità con le versioni precedenti Reporting Services" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se non è possibile utilizzare il programma di installazione per aggiornare un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], installare una nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ed eseguire la migrazione dell'installazione esistente alla nuova istanza. Per ulteriori informazioni, vedere "aggiornamento e migrazione Reporting Services" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [aggiornamento e migrazione Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Negli argomenti seguenti vengono descritti i problemi noti segnalati da Preparazione aggiornamento e viene illustrato come modificare l'installazione esistente per consentire l'esecuzione di un aggiornamento.  
  
> [!IMPORTANT]  
>  Per analizzare un'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è necessario aver installato Preparazione aggiornamento nel server di report. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non supporta l'analisi remota.  
>   
>  Per ulteriori informazioni, vedere [installazione di preparazione aggiornamento](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Certificati client in preparazione aggiornamento sito &#40;Web del server di report&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [Sono state rilevate estensioni personalizzate in &#40;preparazione aggiornamento del server di report&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Sono stati rilevati elementi del report personalizzati &#40;in preparazione aggiornamento del server di report&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Preparazione aggiornamento non rilevati &#40;componenti di compatibilità con le versioni precedenti di IIS&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [Preparazione aggiornamento rilevata &#40;dalla restrizione degli indirizzi IP&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [Filtri ISAPI rilevati in preparazione aggiornamento &#40;sito del server di report&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [Sono state rilevate estensioni obsolete in &#40;preparazione aggiornamento computer del server di report&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [Il database del server di report &#40;non è configurato per preparazione aggiornamento&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [SQL Server 2005 di preparazione aggiornamento rilevato &#40;dal gruppo di servizi Web ReportServer&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [Le directory virtuali non sono &#40;specificate in preparazione aggiornamento&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [La directory virtuale ha un metodo &#40;di autenticazione non supportato preparazione aggiornamento&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [Modifiche ai limiti della CPU e della memoria per SQL Server Standard &#40;ed Enterprise Upgrade Advisor&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [Account di dominio necessari per preparazione &#40;aggiornamento della farm di SharePoint&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [Esplorazione diretta di preparazione aggiornamento &#40;al server di report&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007 è installato &#40;preparazione aggiornamento&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services servizio SharePoint Shared è installato side-by &#40;-Side Upgrade Advisor&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [Preparazione &#40;aggiornamento regole di confronto motore di database server non compatibile&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [Altri problemi di aggiornamento di Reporting Services](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
