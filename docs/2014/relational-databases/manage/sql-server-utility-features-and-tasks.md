---
title: Attività e funzionalità di Utilità SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server utility [SQL Server]
- utility control point
- Utility growth rate
- Multiserver management
- UCP
- Multi-server management [SQL Server]
ms.assetid: 6e6cbd25-6b1c-4e21-9ade-4584e243fd8f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d3f61904a1a820df58583212dcbd2e998dbabbd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63190432"
---
# <a name="sql-server-utility-features-and-tasks"></a>Attività e funzionalità di Utilità SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necessitano di gestire l'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel suo complesso e questa esigenza viene soddisfatta in questa versione tramite il concetto di gestione delle applicazioni e multiserver in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="benefits-of-the-sql-server-utility"></a>Vantaggi di Utilità SQL Server  
 Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di modellare le entità relative all'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di un'organizzazione in una visualizzazione unificata. I punti di visualizzazione di Esplora utilità e Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) offrono agli amministratori una visualizzazione olistica dell'integrità delle risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che funge da punto di controllo dell'utilità. La combinazione di dati riepilogativi e dettagliati visualizzata nel punto di controllo dell'utilità sia per i criteri di sottoutilizzo che per quelli di sovrautilizzo e per vari parametri principali consente di identificare facilmente le possibilità di consolidamento delle risorse e il sovrautilizzo delle risorse. I criteri di integrità sono configurabili e possono essere modificati per impostare soglie di utilizzo delle risorse più alte o più basse. È possibile modificare i criteri di monitoraggio globali o configurare criteri di monitoraggio singoli per ogni entità gestita in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="getting-started-with-sql-server-utility"></a><a name="typical_scenarios"></a> Introduzione a Utilità SQL Server  
 Lo scenario utente tipico prevede innanzitutto la creazione di un punto di controllo dell'utilità che stabilisce il punto ragionevole centrale per Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il punto di controllo dell'utilità fornisce una visualizzazione consolidata dell'integrità delle risorse raccolta da istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In seguito alla creazione del punto di controllo dell'utilità, le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono registrate in Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modo che possano essere gestite dal punto di controllo dell'utilità.  
  
 Ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e applicazione del livello dati gestita da Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere monitorata in base alle definizioni dei criteri globali o alle definizioni dei criteri singoli.  
  
## <a name="related-tasks"></a>Attività correlate  
 Utilizzare gli argomenti seguenti per iniziare a utilizzare Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Vengono descritte le considerazioni per configurare un server per l'esecuzione di set di raccolta dell'utilità e non appartenenti all'utilità nella stessa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|[Considerazioni per l'esecuzione di set di raccolta dell'utilità e non appartenenti all'utilità nella stessa istanza di SQL Server](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)|  
|Viene descritto come creare un punto di controllo di Utilità SQL Server|[Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md)|  
|Viene descritto come effettuare la connessione a Utilità SQL Server.|[Effettuare la connessione a Utilità SQL Server.](connect-to-a-sql-server-utility.md)|  
|Viene descritto come registrare un'istanza di SQL Server con un punto di controllo dell'utilità.|[Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)|  
|Viene descritto come utilizzare Esplora utilità per gestire Utilità SQL Server.|[Usare Esplora utilità per gestire Utilità SQL Server](use-utility-explorer-to-manage-the-sql-server-utility.md)|  
|Viene descritto come monitorare le istanze di SQL Server in Utilità SQL Server.|[Monitoraggio di istanze di SQL Server in Utilità SQL Server](monitor-instances-of-sql-server-in-the-sql-server-utility.md)|  
|Viene descritto come visualizzare i risultati dei criteri di integrità delle risorse.|[Visualizzare i risultati dei criteri di integrità delle risorse &#40;SQL Server Utility&#41;](view-resource-health-policy-results-sql-server-utility.md)|  
|Viene descritto come modificare una definizione dei criteri di integrità delle risorse.|[Modificare una definizione dei criteri di integrità delle risorse &#40;Utilità SQL Server&#41;](modify-a-resource-health-policy-definition-sql-server-utility.md)|  
|Viene descritto come configurare il data warehouse del punto di controllo dell'utilità.|[Configurare il data warehouse del punto di controllo dell'utilità &#40;Utilità SQL Server&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)|  
|Viene descritto come configurare i criteri di integrità dell'utilità.|[Configurare i criteri di integrità &#40;Utilità SQL Server&#41;](configure-health-policies-sql-server-utility.md)|  
|Viene descritto come regolare l'attenuazione nei criteri di utilizzo della CPU.|[Riduzione delle segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)|  
|Viene descritto come rimuovere un'istanza di SQL Server da un punto di controllo dell'utilità.|[Rimuovere un'istanza di SQL Server da Utilità SQL Server](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)|  
|Viene descritto come modificare l'account proxy per l'agente di raccolta dati dell'utilità in un'istanza gestita di SQL Server.|[Modificare l'account proxy per il set di raccolta dell'utilità in un'istanza gestita di SQL Server &#40;Utilità SQL Server&#41;](change-proxy-account-for-utility-collection-on-managed-sql-server.md)|  
|Viene descritto come spostare un punto di controllo dell'utilità da un'istanza di SQL Server a un'altra.|[Spostare un punto di controllo dell'utilità da un'istanza di SQL Server a un'altra &#40;Utilità SQL Server&#41;](move-a-ucp-from-one-instance-of-sql-server-to-another-sql-server-utility.md)|  
|Viene descritto come rimuovere un punto di controllo dell'utilità.|[Rimuovere un punto di controllo dell'utilità &#40;Utilità SQL Server&#41;](remove-a-utility-control-point-sql-server-utility.md)|  
|Viene descritto come risolvere i problemi relativi a Utilità SQL Server.|[Attività e funzionalità di Utilità SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)|  
|Viene descritto come risolvere i problemi relativi all'integrità delle risorse di SQL Server.|[Risolvere i problemi relativi all'integrità delle risorse di SQL Server &#40;Utilità SQL Server&#41;](troubleshoot-sql-server-resource-health-sql-server-utility.md)|  
|Collegamenti agli argomenti della Guida sensibile al contesto di Gestione Utilità.|[Guida sensibile al contesto di Gestione Utilità](utility-explorer-f1-help.md)|  
  
  
