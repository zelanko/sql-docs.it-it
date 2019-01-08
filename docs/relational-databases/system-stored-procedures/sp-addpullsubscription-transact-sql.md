---
title: sp_addpullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c003b103c7957e737f53eb8733022e68073b3aef
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52802503"
---
# <a name="spaddpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aggiunge una sottoscrizione pull a una pubblicazione snapshot o transazionale. Questa stored procedure viene eseguita nel Sottoscrittore nel database in cui deve essere creata la sottoscrizione pull.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>Argomenti  
 [  **@publisher=**] **'***publisher***'**  
 Nome del server di pubblicazione. *server di pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 Nome del database del server di pubblicazione. *publisher_db* viene **sysname**, con un valore predefinito è NULL. *publisher_db* viene ignorata dal server di pubblicazione Oracle.  
  
 [  **@publication=**] **'***pubblicazione***'**  
 Nome della pubblicazione. *pubblicazione* viene **sysname**, non prevede alcun valore predefinito.  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 Specifica se per la pubblicazione è disponibile un agente di distribuzione autonomo. *independent_agent* viene **nvarchar(5**, con un valore predefinito è TRUE. Se **true**, è disponibile un agente di distribuzione autonomo per la pubblicazione. Se **false**, è associato un agente di distribuzione per ogni coppia database del server di pubblicazione/database sottoscrittore. *independent_agent* è una proprietà della pubblicazione e deve avere lo stesso valore qui perché contiene server di pubblicazione.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 Tipo di sottoscrizione. *subscription_type* viene **nvarchar(9)**, il valore predefinito è **anonimo**. È necessario specificare un valore pari **pull** per *subscription_type*, a meno che non si desidera creare una sottoscrizione senza registrarla nel server di pubblicazione. In questo caso, è necessario specificare un valore pari **anonimo**. Ciò è necessario in casi in cui non è possibile stabilire una connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al server di pubblicazione durante la configurazione della sottoscrizione.  
  
 [  **@description=**] **'***descrizione***'**  
 Descrizione della pubblicazione. *Descrizione* viene **nvarchar(100)**, con un valore predefinito è NULL.  
  
 [  **@update_mode=**] **'***update_mode***'**  
 Tipo di aggiornamento. *update_mode* viene **nvarchar(30)**, e può essere uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**di sola lettura** (impostazione predefinita)|La sottoscrizione è di sola lettura. Le modifiche apportate nel Sottoscrittore non vengono ritrasmesse al server di pubblicazione. È consigliabile utilizzare questo valore quando non sono previsti aggiornamenti nel Sottoscrittore.|  
|**Synctran**|Abilita il supporto per sottoscrizioni ad aggiornamento immediato.|  
|**in coda tran**|Abilita la sottoscrizione per l'aggiornamento in coda. Le modifiche dei dati possono essere apportate nel Sottoscrittore, archiviate in una coda e quindi distribuite al server di pubblicazione.|  
|**failover**|Abilita la sottoscrizione per l'aggiornamento immediato sostituito dall'aggiornamento in coda in caso di failover. Le modifiche dei dati possono essere apportate nel Sottoscrittore e distribuite immediatamente al server di pubblicazione. Se il server di pubblicazione e il Sottoscrittore non sono connessi, le modifiche apportate ai dati nel Sottoscrittore possono essere archiviate in una coda fino al ripristino della connessione tra il Sottoscrittore e il server di pubblicazione.|  
|**failover in coda**|Abilita la sottoscrizione come sottoscrizione con aggiornamento in coda con la possibilità di passare alla modalità di aggiornamento immediato. Le modifiche ai dati possono essere apportate nel Sottoscrittore e archiviate in una coda fino alla riconnessione del Sottoscrittore e del server di pubblicazione. Quando viene ristabilita una connessione continua, la modalità di aggiornamento può essere modificata nella modalità di aggiornamento immediato. *Non supportato per il server di pubblicazione Oracle*.|  
  
 [  **@immediate_sync =**] *immediate_sync*  
 Indica se i file di sincronizzazione vengono creati o ricreati a ogni esecuzione dell'agente snapshot. *immediate_sync* viene **bit** con valore predefinito è 1 e deve essere impostato sullo stesso valore come *immediate_sync* nella **sp_addpublication**. *immediate_sync* è una proprietà della pubblicazione e deve avere lo stesso valore qui perché contiene server di pubblicazione.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 **sp_addpullsubscription** viene utilizzata nella replica snapshot e transazionale.  
  
> [!IMPORTANT]  
>  Per le sottoscrizioni ad aggiornamento in coda utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le connessioni ai Sottoscrittori e specificare un account diverso per la connessione a ogni Sottoscrittore. Quando si crea una sottoscrizione pull che supporta l'aggiornamento in coda, la replica imposta sempre la connessione per l'utilizzo dell'autenticazione di Windows. Per le sottoscrizioni pull, il sistema di replica non è in grado di accedere ai metadati nel Sottoscrittore necessari per l'utilizzo dell'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questo caso, è necessario eseguire [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) per modificare la connessione da utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticazione dopo aver configurata la sottoscrizione.  
  
 Se il [MSreplication_subscriptions &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabella non esiste nel Sottoscrittore **sp_addpullsubscription** lo crea. Aggiunge anche una riga per il [MSreplication_subscriptions &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabella. Per le sottoscrizioni pull [sp_addsubscription &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) deve essere chiamato prima del server di pubblicazione.  
  
## <a name="example"></a>Esempio  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo i membri del **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database possono eseguire **sp_addpullsubscription**.  
  
## <a name="see-also"></a>Vedere anche  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create an Updatable Subscription to a Transactional Publication](../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) [sottoscrivere le pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
