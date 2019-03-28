---
title: sp_link_publication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 94d074985848bb510c15907f6b17dc492904f5c0
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537838"
---
# <a name="splinkpublication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Imposta le informazioni di configurazione e sicurezza utilizzate dai trigger di sincronizzazione dei server di sottoscrizione ad aggiornamento immediato durante la connessione al server di pubblicazione. Questa stored procedure viene eseguita nel database di sottoscrizione del Sottoscrittore.  
  
> [!IMPORTANT]
>  Quando si configura un server di pubblicazione con un server di distribuzione remoto, i valori specificati per tutti i parametri, inclusi *job_login* e *job_password*, vengono inviati al server di distribuzione come testo normale. È consigliabile crittografare la connessione tra il server di pubblicazione e il server di distribuzione remoto prima di eseguire questa stored procedure. Per altre informazioni, vedere [Abilitare le connessioni crittografate al motore di database &#40;Gestione configurazione SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
> 
> [!IMPORTANT]
>  In determinate condizioni, questa stored procedure può non riuscire se il sottoscrittore sta eseguendo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 o versione successivo e il server di pubblicazione è in esecuzione una versione precedente. In caso di esito negativo della stored procedure in questo scenario, aggiornare il server di pubblicazione a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 o versioni successive.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @publisher = ] 'publisher'` È il nome del server di pubblicazione a cui collegarsi. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publisher_db = ] 'publisher_db'` È il nome del database di pubblicazione a cui collegarsi. *publisher_db* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @publication = ] 'publication'` È il nome della pubblicazione a cui collegarsi. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
`[ @security_mode = ] security_mode` La modalità di sicurezza utilizzata dal sottoscrittore per la connessione al server di pubblicazione remoto per l'aggiornamento immediato. *security_mode* viene **int**, i possibili valori sono i seguenti. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|Viene utilizzato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'autenticazione con l'account di accesso specificato in questa stored procedure come *login* e *password*.<br /><br /> Nota: Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questa opzione viene utilizzata per specificare una chiamata di procedura remota (RPC) dinamica.|  
|**1**|Utilizza il contesto di sicurezza (autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o autenticazione di Windows) dell'utente che esegue la modifica nel Sottoscrittore.<br /><br /> Nota: È inoltre necessario che tale account esista nel server di pubblicazione e disponga di privilegi sufficienti. Se si utilizza l'autenticazione di Windows è necessario che sia supportata la delega degli account di sicurezza.|  
|**2**|Usa un accesso server collegato esistente definito dall'utente creato usando **sp_link_publication**.|  
  
`[ @login = ] 'login'` È l'account di accesso. *login* è di tipo **sysname** e il valore predefinito è NULL. Questo parametro deve essere specificato quando si specifica *security_mode* viene **0**.  
  
`[ @password = ] 'password'` È la password. *la password* viene **sysname**, con un valore predefinito è NULL. Questo parametro deve essere specificato quando si specifica *security_mode* viene **0**.  
  
`[ @distributor = ] 'distributor'` È il nome del server di distribuzione. *server di distribuzione* viene **sysname**, con un valore predefinito è NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_link_publication** viene usato dalle sottoscrizioni ad aggiornamento immediato nella replica transazionale.  
  
 **sp_link_publication** può essere usato per le sottoscrizioni push e pull. Questa stored procedure può essere chiamata prima o dopo la creazione della sottoscrizione. Una voce viene inserita o aggiornata nel [MSsubscription_properties &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) la tabella di sistema.  
  
 Per le sottoscrizioni push, la voce può essere svuotata dal [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). Per le sottoscrizioni pull, la voce può essere svuotata dal [sp_droppullsubscription &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) oppure [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md). È inoltre possibile chiamare **sp_link_publication** con una password NULL per eliminare la voce nella [MSsubscription_properties &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabella di sistema per motivi di sicurezza.  
  
 La modalità predefinita utilizzata in un Sottoscrittore ad aggiornamento immediato per la connessione al server di pubblicazione non consente la connessione tramite l'autenticazione di Windows. Per eseguire la connessione con questa modalità di autenticazione, è necessario configurare un server collegato per il server di pubblicazione e il Sottoscrittore ad aggiornamento immediato deve utilizzare questa connessione per l'aggiornamento del Sottoscrittore. Questa operazione richiede la **sp_link_publication** da eseguire con *security_mode* = **2**. Se si utilizza l'autenticazione di Windows è necessario che sia supportata la delega degli account di sicurezza.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server possono eseguire **sp_link_publication**.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
