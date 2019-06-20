---
title: Aggiornamento di Reporting Services problemi (Upgrade Advisor) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: de69a25d1689883fdcbce8796d3cdcd30374a8f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092576"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Problemi di aggiornamento di Reporting Services (Preparazione aggiornamento)
  Gli argomenti seguenti descrivono le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] problemi che potrebbero influire sull'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Vengono illustrate le azioni che è possibile eseguire per ridurre l'effetto di queste modifiche nell'ambiente.  
  
 Con Preparazione aggiornamento viene analizzata un'installazione del server di report. Se sono installati solo i componenti client (ad esempio se Progettazione report è l'unico componente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato nel computer), non verrà segnalato alcun problema.  
  
 A seconda della modalità di configurazione dell'installazione, è possibile che vengano rilevati altri problemi non segnalati da Preparazione aggiornamento. Tali problemi non impediscono il corretto aggiornamento di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], ma possono influire sull'esecuzione di report e applicazioni al termine di un aggiornamento. Per ulteriori informazioni su questi problemi, vedere "Compatibilità con le versioni precedenti Reporting Services" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se non è possibile utilizzare il programma di installazione per aggiornare un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], installare una nuova istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ed eseguire la migrazione dell'installazione esistente alla nuova istanza. Per altre informazioni, vedere "Eseguire l'aggiornamento ed eseguire la migrazione di Reporting Services" nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Negli argomenti seguenti vengono descritti i problemi noti segnalati da Preparazione aggiornamento e viene illustrato come modificare l'installazione esistente per consentire l'esecuzione di un aggiornamento.  
  
> [!IMPORTANT]  
>  Per analizzare un'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è necessario aver installato Preparazione aggiornamento nel server di report. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non supporta l'analisi remota.  
>   
>  Per altre informazioni, vedere [installazione di preparazione aggiornamento](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Certificati client sul sito web del server di report &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [Estensioni personalizzate rilevate nel server di report &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Sono stati rilevati elementi del report personalizzati nel server di report &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Non sono stati rilevati componenti di compatibilità con le versioni precedenti di IIS &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [Rilevata restrizione degli indirizzi IP &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [Filtri ISAPI rilevati sul sito del server di report &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [Sono state rilevate estensioni obsolete nel computer del server di report &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [Database del server di report non è configurato &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [Rilevato un gruppo di servizi di SQL Server 2005 Report Server Web &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [Sono state specificate directory virtuali &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [Directory virtuale metodo di autenticazione non supportato &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [Modifiche ai limiti della CPU e memoria per SQL Server Standard ed Enterprise &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [Gli account di dominio richiesti per la farm di SharePoint &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [Esplorazione diretta nel Server di Report di &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007 è installato &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server SharePoint servizio condiviso Reporting Services è installato Side-by sul lato &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [Le regole di confronto di Database incompatibili motore Server &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [Altri problemi di aggiornamento di Reporting Services](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
