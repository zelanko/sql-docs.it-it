---
title: Attività Pulizia contenuto cronologia (Piano di manutenzione) | Microsoft Docs
description: Informazioni su come eliminare la cronologia di backup/ripristino, la cronologia processo SQL Server Agent e la cronologia del piano di manutenzione dal database msdb utilizzando l'attività Pulizia contenuto cronologia.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: a8fecc3eb56a015ac420ca2cd5167098bbce84ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85667054"
---
# <a name="history-cleanup-task-maintenance-plan"></a>Attività Pulizia contenuto cronologia (Piano di manutenzione)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare la finestra di dialogo **Attività Pulizia contenuto cronologia** per eliminare le informazioni cronologiche meno recenti dalle tabelle del database msdb. Questa attività supporta l'eliminazione della cronologia delle operazioni di backup e ripristino, della cronologia processo agente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e della cronologia del piano di manutenzione.  
  
 Questa istruzione usa le istruzioni **sp_purge_jobhistory** e **sp_delete_backuphistory** .  
  
## <a name="ui-element-list"></a>Elenco di elementi dell'interfaccia utente  
 **Connection**  
 Consente di selezionare la connessione server da utilizzare per l'esecuzione dell'attività.  
  
 **Nuovo**  
 Consente di creare una nuova connessione server da utilizzare per l'esecuzione dell'attività. La finestra di dialogo **Nuova connessione** viene descritta più avanti in questo argomento.  
  
 **Cronologia operazioni di backup e ripristino**  
 Se si mantengono i record relativi alla data di creazione di backup recenti, è possibile semplificare la creazione di un piano di recupero da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in caso si desideri ripristinare un database. Il periodo di memorizzazione deve essere almeno pari alla frequenza dei backup completi del database.  
  
 **Cronologia processo di SQL Server Agent**  
 Questa cronologia si rivela utile per risolvere problemi relativi a processi non riusciti o per individuare le cause di determinate azioni sul database.  
  
 **Cronologia piano di manutenzione**  
 Questa cronologia si rivela utile per risolvere problemi relativi a processi del piano di manutenzione non riusciti o per individuare le cause di determinate azioni sul database.  
  
 **Rimuovi dati presenti nella cronologia da più di**  
 Specifica il periodo di permanenza nella cronologia oltre il quale gli elementi devono essere eliminati.  
  
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
 Consente di connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] di SQL Server utilizzando l'autenticazione di Microsoft Windows.  
  
 **Usa nome utente e password specifici**  
 Consente di connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] di SQL Server utilizzando l'autenticazione di SQL Server. Questa opzione non è disponibile.  
  
 **Nome utente**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [sp_delete_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)  
  
  
