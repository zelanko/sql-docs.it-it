---
title: Attività Notifica operatori (piano di manutenzione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.notifyoperator.f1
helpviewer_keywords:
- Notify Operator Task dialog box
ms.assetid: 39c0797c-ad2b-4591-85c9-a23a7f902895
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ef94ed9e296c588b70789ace0bbbbe79bc8008f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205959"
---
# <a name="notify-operator-task-maintenance-plan"></a>Attività Notifica operatori (Piano di manutenzione)
  Utilizzare la finestra di dialogo **attività Notifica operatori** per aggiungere una notifica automatica a questo piano di manutenzione. Per utilizzare questa attività, è necessario disporre di posta elettronica database abilitata e configurata correttamente con msdb come database host della [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] posta elettronica e disporre di un operatore Agent con un indirizzo di posta elettronica valido.  
  
 Questa attività utilizza la stored procedure sp_notify_operator.  
  
## <a name="options"></a>Opzioni  
 **Connessione**  
 Consente di selezionare la connessione server da utilizzare per l'esecuzione dell'attività.  
  
 **Nuovo**  
 Consente di creare una nuova connessione server da utilizzare per l'esecuzione dell'attività. La finestra di dialogo **Nuova connessione** è descritta di seguito.  
  
 **Operatori da notificare**  
 Consente di specificare il destinatario del messaggio di posta elettronica.  
  
 **Oggetto del messaggio di notifica**  
 Consente di specificare il testo da includere nella riga dell'oggetto del messaggio di notifica.  
  
 **Corpo del messaggio di notifica**  
 Consente di specificare il testo da includere nel corpo del messaggio di notifica.  
  
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
 Connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] con [!INCLUDE[msCoName](../../includes/msconame-md.md)] l'autenticazione di Windows.  
  
 **Usa nome utente e password specifici**  
 Connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizzando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione di. Questa opzione non è disponibile.  
  
 **Nome utente**  
 Consente di specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
 **Password**  
 Consente di specificare una password da utilizzare per l'autenticazione. Questa opzione non è disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../database-mail/database-mail.md)   
 [sp_notify_operator &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)  
  
  
