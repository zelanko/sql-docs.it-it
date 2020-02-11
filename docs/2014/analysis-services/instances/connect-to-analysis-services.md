---
title: Connetti a Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- instances of Analysis Services, connections
ms.assetid: 73ee8171-3379-4384-bfc8-071b3eebbc8f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 654d659900d01ae9d5caf5188b9146510de483ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080115"
---
# <a name="connect-to-analysis-services"></a>Connetti ad Analysis Services
  In questa sezione sono contenute le informazioni sulle proprietà della stringa di connessione, sulle librerie client usate per le connessioni, quali metodi di autenticazione sono supportati da Analysis Services e come impostare o cancellare le connessioni prima di disconnettere un server.  
  
## <a name="analysis-services-connections"></a>Connessioni ad Analysis Services  
 In Analysis Services TCP e XML for Analysis (XMLA) vengono utilizzati rispettivamente come protocollo di rete e protocollo di comunicazione. Tutte le librerie client fornite con Analysis Services implementano almeno XMLA-over-TCP. Sebbene sia possibile compilare applicazioni basate su XMLA non elaborato, la maggior parte delle applicazioni e degli sviluppatori di applicazioni utilizza librerie client per sfruttare i modelli a oggetti e i relativi vantaggi per quanto concerne la scrittura di codice. Per le connessioni client di Analysis Services, è possibile usare IIS come connessione intermedia se non è possibile usare TCP attraverso lo stack. Uno dei vantaggi dell'usare l'accesso HTTP tramite IIS consiste nella possibilità di connettersi da applicazioni che passano le credenziali nella stringa di connessione.  
  
 Qualsiasi trattazione della connettività prevede in genere che si tenga conto dell'autenticazione. A differenza di altre funzionalità di SQL Server, Analysis Services usa esclusivamente le credenziali di Windows. Non è possibile usare l'autenticazione del database SQL Server, l'autenticazione basata su attestazioni, l'autenticazione basata su moduli o il digest per la connessione back-end per Analysis Services. In questa sezione sono disponibili ulteriori informazioni sull'autenticazione.  
  
##  <a name="bkmk_clientApps"></a>Attività di connessione  
  
|Collegamento|Descrizione dell'attività|  
|----------|----------------------|  
|[Connettersi dalle applicazioni client &#40;Analysis Services&#41;](connect-from-client-applications-analysis-services.md)|Se non si ha familiarità con Analysis Services, leggere questo argomento per un'introduzione agli strumenti e alle applicazioni di uso più comune con Analysis Services.|  
|[Proprietà della stringa di connessione &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)|Analysis Services include numerose proprietà di server e database che consentono di personalizzare una connessione per un'applicazione specifica indipendentemente dalla configurazione dell'istanza o del database.|  
|[Metodologie di autenticazione supportate da Analysis Services](authentication-methodologies-supported-by-analysis-services.md)|Questo argomento offre una sintetica introduzione ai metodi di autenticazione utilizzati da Analysis Services.|  
|[Configurare Analysis Services per la delega vincolata Kerberos](configure-analysis-services-for-kerberos-constrained-delegation.md)|Per molte soluzioni di Business Intelligence è necessaria la rappresentazione per assicurare che a ogni utente vengano restituiti solo dati autorizzati. In questo argomento sono disponibili informazioni sull'utilizzo della rappresentazione. In questo argomento vengono inoltre descritti i passaggi per configurare Analysis Services per la delega vincolata Kerberos.|  
|[Registrazione del nome SPN per un'istanza di Analysis Services](spn-registration-for-an-analysis-services-instance.md)|L'autenticazione Kerberos richiede un nome SPN valido per i servizi che rappresentano o delegano le identità utente in soluzioni multiserver. Utilizzare le informazioni contenute in questo argomento per apprendere la costruzione e i passaggi per la registrazione del nome SPN per Analysis Services.|  
|[Configurare l'accesso HTTP per Analysis Services in Internet Information Services &#40;IIS&#41; 8,0](configure-http-access-to-analysis-services-on-iis-8-0.md)|L'autenticazione di base e i limiti tra domini rappresentano due motivi importanti per configurare Analysis Services per l'accesso HTTP.|  
|[Provider di dati utilizzati per le connessioni Analysis Services](data-providers-used-for-analysis-services-connections.md)|Analysis Services offre tre librerie client per accedere alle operazioni server o ai dati di Analysis Services. Questo argomento offre una sintetica introduzione ad ADOMD.NET, agli oggetti di gestione di Analysis Services (AMO) e al provider OLE DB di Analysis Services (MSOLAP).|  
|[Disconnettere utenti e sessioni nel server Analysis Services](disconnect-users-and-sessions-on-analysis-services-server.md)|Cancellare le connessioni e le sessioni esistenti prima di portare un server offline o eseguire test delle prestazioni di base.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione post-installazione &#40;Analysis Services&#41;](post-install-configuration-analysis-services.md)   
 [Configurare le proprietà del server in Analysis Services](../server-properties/server-properties-in-analysis-services.md)   
 [Creazione di script per attività amministrative in Analysis Services](../script-administrative-tasks-in-analysis-services.md)  
  
  
