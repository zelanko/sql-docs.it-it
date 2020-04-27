---
title: Piani di manutenzione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- SQL12.AG.MAINTPLAN.LEGACY.F1
helpviewer_keywords:
- maintenance plans [SQL Server], about database maintenance plans
- maintenance plans [SQL Server], database compatibility level displayed in designer
- maintenance plans [SQL Server]
ms.assetid: 5982ca65-74fe-44e3-aef9-00a65a0db169
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0643c6fbf8e9a6aa649d4d335117bcb4f5b35208
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68206847"
---
# <a name="maintenance-plans"></a>Piani di manutenzione
  Con i piani di manutenzione è possibile creare un flusso di lavoro per le attività necessarie per assicurare prestazioni ottimali del database, eseguire regolarmente il backup del database e verificare che nel database non siano presenti incoerenze. Sebbene sia possibile utilizzare anche Creazione guidata piano di manutenzione per creare i piani di manutenzione principali, la creazione manuale dei piani offre una maggiore flessibilità.  
  
## <a name="benefits-of-maintenance-plans"></a>Vantaggi di piani di manutenzione  
 In [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)], i piani di manutenzione vengono creati come pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], eseguiti tramite un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. I piani di manutenzione possono essere eseguiti manualmente o automaticamente in base a intervalli pianificati.  
  
 I piani di manutenzione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] offrono le funzionalità seguenti:  
  
-   Creazione del flusso di lavoro tramite una vasta gamma di normali attività di manutenzione. È inoltre possibile creare script [!INCLUDE[tsql](../../includes/tsql-md.md)] personalizzati.  
  
-   Gerarchie concettuali. Ogni piano consente di creare o modificare i flussi di lavoro delle attività. Le attività in ogni piano possono essere raggruppate in sottopiani, per i quali è possibile pianificare l'esecuzione in momenti diversi.  
  
-   Supporto di piani multiserver utilizzabili in ambienti con server master/server di destinazione.  
  
-   Supporto della registrazione della cronologia del piano in server remoti.  
  
-   Supporto dell'autenticazione di Windows e dell'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="maintenace-plan-functionality"></a>Funzionalità del piano di manutenzione  
 È possibile creare piani di manutenzione per eseguire le attività seguenti:  
  
-   Riorganizzazione dei dati e delle pagine di indice mediante la ricompilazione degli indici con un nuovo fattore di riempimento. Questa operazione assicura che le pagine di database includano una quantità di dati e di spazio libero equamente distribuita per consentire in futuro un più rapido aumento delle dimensioni. Per altre informazioni, vedere [Specificare un fattore di riempimento per un indice](../indexes/specify-fill-factor-for-an-index.md).  
  
-   Compressione dei file di dati mediante la rimozione delle pagine di database vuote.  
  
-   Aggiornamento delle statistiche dell'indice per garantire che Query Optimizer disponga di informazioni aggiornate sulla distribuzione dei valori di dati nelle tabelle. In tal modo Query Optimizer può scegliere il metodo di accesso ai dati più indicato perché sono disponibili più informazioni sui dati archiviati nel database. Sebbene le statistiche dell'indice vengano aggiornate automaticamente e periodicamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa opzione può forzare l'aggiornamento immediato delle statistiche.  
  
-   Esecuzione dei controlli di coerenza interna dei dati e delle pagine di dati all'interno del database per assicurarsi che i dati non siano stati danneggiati a causa di un problema di sistema o del software.  
  
-   Backup del database e dei file del log delle transazioni. I backup dei database e dei log possono essere mantenuti per un periodo specificato. In tal modo è possibile creare una cronologia dei backup da utilizzare se è necessario ripristinare il database in base allo stato in cui si trovata prima dell'ultimo backup. È anche possibile eseguire backup differenziali.  
  
-   Esecuzione di processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa operazione consente di creare processi che eseguono una serie di operazioni, nonché i piani di manutenzione per l'esecuzione dei processi.  
  
 I risultati generati dalle attività di manutenzione possono essere scritti come report in un file di testo oppure nelle tabelle dei piani di manutenzione (`sysmaintplan_log` e `sysmaintplan_logdetail`) in `msdb`. Per visualizzare i risultati nel visualizzatore file di log, fare clic con il pulsante destro del mouse su **Piani di manutenzione** e quindi scegliere **Visualizza cronologia**.  
  
## <a name="related-tasks"></a>Attività correlate  
 Utilizzare i seguenti argomenti per avere un'introduzione ai piani di manutenzione.  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Viene illustrata la creazione di un piano di manutenzione tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].|[Creare un piano di manutenzione](create-a-maintenance-plan.md)|  
|Viene illustrata la creazione di un piano di manutenzione tramite l'area di progettazione del piano di manutenzione.|[Creare un piano di manutenzione &#40;area di progettazione del piano di manutenzione&#41;](create-a-maintenance-plan-maintenance-plan-design-surface.md)|  
|Documenta la funzionalità del piano di manutenzione disponibile in Esplora oggetti.|[Nodo Piani di manutenzione &#40;Esplora oggetti&#41;](../../ssms/object/object-explorer.md)|  
  
  
