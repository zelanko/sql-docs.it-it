---
title: Attività Aggiorna statistiche (Piano di manutenzione) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.statistics.f1
helpviewer_keywords:
- Updates Statistics Task dialog box
ms.assetid: 22902fd0-eb39-4f18-af94-3fcb69d2a3a4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d63b9d5d864dc9027eaf6b19a4e4964895699feb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115506"
---
# <a name="update-statistics-task-maintenance-plan"></a>Attività Aggiorna statistiche (Piano di manutenzione)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Usare la finestra di dialogo **Attività Aggiorna statistiche** per aggiornare le informazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sui dati contenuti nelle tabelle e negli indici. Questa attività consente di eseguire un nuovo campionamento delle statistiche di distribuzione di tutti gli indice creati per le tabelle utente del database. Le statistiche di distribuzione vengono utilizzate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ottimizzare le operazioni di navigazione tra le tabelle durante l'elaborazione delle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] . Per compilare automaticamente le statistiche di distribuzione, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue, per ogni indice, un campionamento periodico dei dati della tabella corrispondente La dimensione del campione è basata sul numero di righe della tabella e sulla frequenza di modifica dei dati. Questa opzione consente di eseguire un ulteriore campionamento utilizzando una determinata percentuale di dati delle tabelle. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa queste informazioni per creare piani di query più efficienti.  
  
Questa attività esegue l'istruzione `UPDATE STATISTICS`.  
  
## <a name="options"></a>Opzioni  
 **Connessione**  
 Consente di selezionare la connessione server da utilizzare per l'esecuzione dell'attività.  
  
 **Nuova**  
 Consente di creare una nuova connessione server da utilizzare per l'esecuzione dell'attività. La finestra di dialogo **Nuova connessione** è descritta di seguito.  
  
 **Database**  
 Consente di specificare i database su cui verrà eseguita l'attività.  
  
-   **Tutti i database**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione su tutti i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad eccezione di tempdb.  
  
-   **Tutti i database di sistema**  
  
     Consente di generare un piano di manutenzione per l'esecuzione di attività di manutenzione su ogni database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad eccezione di tempdb. Non vengono eseguite attività di manutenzione sui database creati dall'utente.  
  
-   **Tutti i database utente**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione su tutti i database creati dall'utente. Nessuna attività di manutenzione viene eseguita sui database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Database specifici**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione solo sui database selezionati. Se si sceglie questa opzione, è necessario selezionare almeno un database nell'elenco.  
  
 > [!NOTE]
 > I piani di manutenzione vengono eseguiti solo nei database per i quali è impostato un livello di compatibilità 80 o superiore. I database per cui è impostato un livello di compatibilità 70 o inferiore non vengono visualizzati.  
  
 **Oggetto**  
 Consente di limitare la griglia **Selezione** per visualizzare tabelle, viste o entrambe.  
  
 **Selezione**  
 Specificare le tabelle o gli indici su cui verrà eseguita l'attività. Questa opzione non è disponibile quando si seleziona **Tabelle e viste** nella casella Oggetto.  
  
 **Tutte le statistiche esistenti**  
 Consente di aggiornare le statistiche sia per le colonne che per gli indici.  
  
 **Solo statistiche colonne**  
 Consente di aggiornare soltanto le statistiche relative alle colonne.  
  
 **Solo statistiche indici**  
 Consente di aggiornare soltanto le statistiche relative agli indici.  
  
 **Tipo analisi**  
 Tipo di analisi utilizzata per raccogliere statistiche aggiornate.  
  
 **Analisi completa**  
 Consente di leggere tutte le righe della tabella o della vista per raccogliere le statistiche.  
  
 **Campionamento per**  
 Specificare la percentuale della tabella o della vista indicizzata o il numero di righe da utilizzare come campione durante la raccolta di statistiche per tabelle o viste di grandi dimensioni.  
  
 **Visualizza codice T-SQL**  
 Consente di visualizzare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite sul server per questa attività, in base alle opzioni selezionate.  
  
> [!NOTE]  
> Se il numero di oggetti interessato dall'attività è elevato, la visualizzazione del codice potrebbe richiedere una considerevole quantità di tempo.  
  
## <a name="new-connection-dialog-box"></a>Finestra di dialogo Nuova connessione  
 **Nome connessione**  
 Consente di immettere un nome per la nuova connessione.  
  
 **Selezionare o immettere il nome di un server**  
 Consente di selezionare il server a cui connettersi per l'esecuzione dell'attività.  
  
 **Aggiorna**  
 Consente di aggiornare l'elenco dei server disponibili.  
  
 **Immettere le informazioni per l'accesso al server**  
 Consente di specificare le opzioni di autenticazione per l'accesso al server.  
  
 **Usa la sicurezza integrata di Windows NT**  
 Consente di connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Usa nome utente e password specifici**  
 Consente di connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione non è disponibile.  
  
 **User name**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)    
 [sp_updatestats](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)    
 [Adaptive Index Defrag](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) (Deframmentazione dell'indice adattativo)
