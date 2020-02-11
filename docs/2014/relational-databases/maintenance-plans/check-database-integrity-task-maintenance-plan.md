---
title: Attività Controlla integrità database (piano di manutenzione) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.maintplanproperties.integrity.f1
- sql12.swb.maint.integrity.f1
helpviewer_keywords:
- Check Database Integrity Task dialog box
ms.assetid: 3534494a-5dfe-4738-b49a-e7fabd731c47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 42fa69e6456b23f95d6a203062b580bd04f443fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63144673"
---
# <a name="check-database-integrity-task-maintenance-plan"></a>Attività Controlla integrità database (Piano di manutenzione)
  Utilizzare la finestra di dialogo **attività Controlla integrità database** per controllare l'allocazione e l'integrità strutturale delle tabelle utente e di sistema e degli indici nel `DBCC CHECKDB` [!INCLUDE[tsql](../../includes/tsql-md.md)] database eseguendo l'istruzione. L'esecuzione di `DBCC` consente di individuare gli eventuali problemi di integrità nel database, in modo che l'amministratore di sistema o il proprietario del database possa analizzarli e correggerli in un secondo momento.  
  
## <a name="options"></a>Opzioni  
 **Connessione**  
 Consente di selezionare la connessione server da utilizzare per l'esecuzione dell'attività.  
  
 **Nuovo**  
 Consente di creare una nuova connessione server da utilizzare per l'esecuzione dell'attività. La finestra di dialogo **Nuova connessione** è descritta di seguito.  
  
 **Database**  
 Consente di specificare i database su cui verrà eseguita l'attività.  
  
-   **Tutti i database**  
  
     Generare un piano di manutenzione per l'esecuzione di attività [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di manutenzione su tutti i database ad eccezione di **tempdb**.  
  
-   **Tutti i database di sistema**  
  
     Generare un piano di manutenzione per l'esecuzione di attività di manutenzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su ogni database di sistema, ad eccezione di **tempdb**. Non vengono eseguite attività di manutenzione sui database creati dall'utente.  
  
-   **Tutti i database utente**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione su tutti i database creati dall'utente. Nessuna attività di manutenzione viene eseguita sui database di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Questi database specifici**  
  
     Consente di generare un piano per l'esecuzione di attività di manutenzione solo sui database selezionati. Se si sceglie questa opzione, è necessario selezionare almeno un database nell'elenco.  
  
    > [!NOTE]  
    >  I piani di manutenzione vengono eseguiti solo nei database per i quali è impostato un livello di compatibilità 80 o superiore. I database per cui è impostato un livello di compatibilità 70 o inferiore non vengono visualizzati.  
  
 **Includi indici**  
 Viene controllata l'integrità di tutte le pagine di indice, nonché delle pagine dei dati della tabella.  
  
 **Visualizza T-SQL**  
 Consente di visualizzare le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite sul server per questa attività, in base alle opzioni selezionate.  
  
> [!NOTE]  
>  Se il numero di oggetti interessato dall'attività è elevato, la visualizzazione del codice potrebbe richiedere una considerevole quantità di tempo.  
  
## <a name="new-connection-dialog-box"></a>Finestra di dialogo Nuova connessione  
 **Nome connessione**  
 Consente di immettere un nome per la nuova connessione.  
  
 **Selezionare o immettere un nome di server**  
 Consente di selezionare il server a cui connettersi per l'esecuzione dell'attività.  
  
 **Aggiorna**  
 Consente di aggiornare l'elenco dei server disponibili.  
  
 **Immettere le informazioni per l'accesso al server**  
 Consente di specificare le opzioni di autenticazione per l'accesso al server.  
  
 **Usa la sicurezza integrata di Windows**  
 Consente di connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizzando l'autenticazione di Windows.  
  
 **Usa nome utente e password specifici**  
 Connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizzando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di. Questa opzione non è disponibile.  
  
 **Nome utente**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
  
