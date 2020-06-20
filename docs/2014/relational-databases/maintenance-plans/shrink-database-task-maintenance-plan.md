---
title: Attività Compatta database (Piano di manutenzione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.shrink.f1
- Shrink Database Task
- Shrink Database(s) Task
helpviewer_keywords:
- Shrink Database Task dialog box
ms.assetid: a9874cac-cded-4145-9c38-8aafd267dbee
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b8ee6060a4ee6ca3272434cf3d9115638a675e62
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023933"
---
# <a name="shrink-database-task-maintenance-plan"></a>Attività Compatta database (Piano di manutenzione)
  Usare la finestra di dialogo **Attività Compatta database** per creare un'attività che cerchi di ridurre le dimensioni dei database selezionati. Le opzioni illustrate di seguito consentono di definire la quantità di spazio non utilizzato che deve rimanere nel database dopo la compattazione. Maggiore è la percentuale specificata, minore sarà il livello di compattazione del database. Il valore è basato sulla percentuale dei dati effettivi presenti nel database. Compattando ad esempio un database da 100 MB contenente 60 MB di dati e 40 MB di spazio disponibile con una percentuale di spazio disponibile del 50%, si ottiene un database con 60 MB di dati e 30 MB di spazio disponibile, perché il 50% di 60 MB è pari a 30 MB. Viene eliminato dal database solo lo spazio in eccesso. I valori validi sono compresi tra 0 e 100.  
  
 Compattando i file di dati si recupera spazio spostando le pagine di dati dalla fine del file allo spazio non occupato più vicino all'inizio del file. Quando alla fine del file viene creato sufficiente spazio libero, le pagine di dati possono essere deallocate e restituite al file system.  
  
> [!WARNING]  
>  I dati spostati per ridurre un file possono essere dispersi in qualsiasi percorso disponibile nel file, provocando la frammentazione dell'indice e rallentando le prestazioni di query che eseguono ricerche in un intervallo dell'indice Per eliminare la frammentazione, valutare la possibilità di ricompilare gli indici sul file dopo la compattazione.  
  
 Questa attività esegue l'istruzione DBCC SHRINKDATABASE.  
  
## <a name="options"></a>Opzioni  
 **Connection**  
 Consente di selezionare la connessione server da utilizzare per l'esecuzione dell'attività.  
  
 **Nuovo**  
 Consente di creare una nuova connessione server da utilizzare per l'esecuzione dell'attività. La finestra di dialogo **Nuova connessione** è descritta di seguito.  
  
 **Database**  
 Consente di specificare i database su cui verrà eseguita l'attività.  
  
-   **Tutti i database**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione su tutti i database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad eccezione di tempdb.  
  
-   **Tutti i database di sistema**  
  
     Consente di generare un piano di manutenzione per l'esecuzione di attività di manutenzione su ogni database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad eccezione di tempdb. Non vengono eseguite attività di manutenzione sui database creati dall'utente.  
  
-   **Tutti i database utente**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione su tutti i database creati dall'utente. Nessuna attività di manutenzione viene eseguita sui database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **I database seguenti**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione solo sui database selezionati. Se si sceglie questa opzione, è necessario selezionare almeno un database nell'elenco.  
  
    > [!NOTE]  
    >  I piani di manutenzione vengono eseguiti solo nei database per i quali è impostato un livello di compatibilità 80 o superiore. I database per cui è impostato un livello di compatibilità 70 o inferiore non vengono visualizzati.  
  
 **Compatta database quando le dimensioni superano**  
 Specificare le dimensioni in megabyte che causano l'esecuzione dell'attività.  
  
 **Spazio che deve rimanere disponibile dopo la compattazione**  
 Consente di arrestare l'operazione di compattazione quando lo spazio disponibile nei file di database raggiunge le dimensioni specificate.  
  
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
 Consente di connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Usa nome utente e password specifici**  
 Consente di connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questa opzione non è disponibile.  
  
 **Nome utente**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql)  
  
  
