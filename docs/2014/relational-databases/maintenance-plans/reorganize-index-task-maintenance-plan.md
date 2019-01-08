---
title: Attività Riorganizza indice (Piano di manutenzione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.defrag.f1
helpviewer_keywords:
- Reorganize Index Task dialog box
ms.assetid: e9cbebbd-f36f-4176-9832-382a46ac946c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0f354280da857be236049a564a77716e93cd351
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747423"
---
# <a name="reorganize-index-task-maintenance-plan"></a>Attività Riorganizza indice (Piano di manutenzione)
  Usare la finestra di dialogo **Attività Riorganizza indice** per razionalizzare l'ordine di ricerca delle pagine dell'indice. In questa attività viene utilizzata l'istruzione `ALTER INDEX REORGANIZE` con i database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
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
  
     Consente di generare un piano per l'esecuzione delle attività di manutenzione in ogni database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad eccezione di **tempdb**. Non vengono eseguite attività di manutenzione sui database creati dall'utente.  
  
-   **Tutti i database utente**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione su tutti i database creati dall'utente. Nessuna attività di manutenzione viene eseguita sui database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Database specifici**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione solo sui database selezionati. Se si sceglie questa opzione, è necessario selezionare almeno un database nell'elenco.  
  
 **Oggetto**  
 Consente di limitare la griglia **Selezione** per visualizzare tabelle, viste o entrambe.  
  
 **Selezione**  
 Specificare le tabelle o gli indici su cui verrà eseguita l'attività. Questa opzione non è disponibile quando si seleziona **Tabelle e viste** nella casella **Oggetto** .  
  
 **Compatta oggetti di grandi dimensioni**  
 Dealloca spazio per tabelle e viste, se possibile. Questa opzione utilizza l'istruzione `ALTER INDEX LOB_COMPACTION = ON`  
  
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
 Consente di connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'autenticazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Usa nome utente e password specifici**  
 Consente di connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione non è disponibile.  
  
 **Nome utente**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [DBCC INDEXDEFRAG &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-indexdefrag-transact-sql)  
  
  
