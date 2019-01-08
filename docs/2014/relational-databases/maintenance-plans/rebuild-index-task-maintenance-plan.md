---
title: Attività Ricompila indice (piano di manutenzione) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reindex.f1
- reindex
helpviewer_keywords:
- Rebuild Index Task dialog box
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34bd5a607998c6e37f688ccbadcd4d612d3daea7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52818216"
---
# <a name="rebuild-index-task-maintenance-plan"></a>Attività Ricompila indice (Piano di manutenzione)
  Usare la finestra di dialogo **Attività Ricompila indice** per ricreare gli indici nelle tabelle del database con un nuovo fattore di riempimento. Il fattore di riempimento determina la quantità di spazio vuoto in ogni pagina dell'indice che potrà essere utilizzato per contenere espansioni future. Poiché il fattore di riempimento non viene gestito, a mano a mano che si aggiungono dati alla tabella lo spazio libero disponibile si riduce. La riorganizzazione delle pagine di dati e di indici consente di ristabilire lo spazio libero.  
  
 In **Attività Ricompila indice** viene utilizzata l'istruzione ALTER INDEX.  
  
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
    >  I piani di manutenzione vengono eseguiti solo nei database per i quali è impostato un livello di compatibilità 80 o superiore. I database per cui è impostato un livello di compatibilità 70 o inferiore non vengono visualizzati.  
  
 **Oggetto**  
 Consente di limitare la griglia **Selezione** per visualizzare tabelle, viste o entrambe.  
  
 **Selezione**  
 Specificare le tabelle o gli indici su cui verrà eseguita l'attività. Questa opzione non è disponibile quando si seleziona **Tabelle e viste** nella casella Oggetto.  
  
 **Riorganizza pagine mantenendo la quantità predefinita di spazio libero**  
 Se si seleziona questa opzione, gli indici delle tabelle del database vengono eliminati e quindi ricreati utilizzando il fattore di riempimento specificato al momento della creazione degli indici.  
  
 **Modifica gratuito percentuale di spazio per pagina**  
 Elimina gli indici delle tabelle del database e li ricrea utilizzando un nuovo fattore di riempimento calcolato automaticamente, riservando in tal modo la quantità di spazio disponibile specificata nelle pagine dell'indice. Maggiore è la percentuale, maggiore sarà la quantità di spazio disponibile riservata nelle pagine dell'indice e maggiori saranno le dimensioni dell'indice. I valori validi sono compresi tra 0 e 100.  
  
 **Ordina risultati in tempdb**  
 Usare il `SORT_IN_TEMPDB`opzione che determina dove i risultati intermedi dell'ordinamento, generati durante la creazione dell'indice, vengono memorizzati temporaneamente. Se non è necessario eseguire un'operazione di ordinamento o se l'ordinamento può essere eseguito in memoria, l'opzione `SORT_IN_TEMPDB`viene ignorata.  
  
 **Mantieni indice online durante la reindicizzazione**  
 Utilizzare l'opzione `ONLINE` per consentire agli utenti di accedere alla tabella o ai dati dell'indice cluster sottostanti, nonché agli eventuali indici non cluster associati durante le operazioni sugli indici.  
  
> [!NOTE]  
>  Le operazioni sugli indici online sono disponibili solo in alcune edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **Visualizza codice T-SQL**  
 Consente di visualizzare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite sul server per questa attività, in base alle opzioni selezionate.  
  
> [!NOTE]  
>  Se il numero di oggetti interessato dall'attività è elevato, la visualizzazione del codice potrebbe richiedere una considerevole quantità di tempo.  
  
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
 Consente di connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizzando l'autenticazione di Windows.  
  
 **Usa nome utente e password specifici**  
 Consente di connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione non è disponibile.  
  
 **Nome utente**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [DBCC DBREINDEX &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dbreindex-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [Opzione SORT_IN_TEMPDB per gli indici](../indexes/indexes.md)   
 [Linee guida per operazioni di indice online](../indexes/guidelines-for-online-index-operations.md)   
 [Funzionamento delle operazioni sugli indici online](../indexes/how-online-index-operations-work.md)   
 [Eseguire operazioni online sugli indici](../indexes/perform-index-operations-online.md)  
  
  
