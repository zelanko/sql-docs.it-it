---
title: sp_syscollector_update_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7d77ec36f36260226a78136b46656b1e2e8187e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004319"
---
# <a name="spsyscollectorupdatecollectionset-transact-sql"></a>sp_syscollector_update_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Consente di rinominare un set di raccolta definito dall'utente o di modificarne le proprietà.  
  
> [!WARNING]  
>  Nei casi in cui l'account di Windows configurato come proxy è un utente interattivo o non interattivo non ancora connesso, la directory di profilo non sarà presente e la creazione della directory di gestione temporanea non riuscirà. Se pertanto si utilizza un account proxy in un controller di dominio, è necessario specificare un account interattivo utilizzato almeno una volta in modo da assicurare la creazione della directory di profilo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @collection_set_id = ] collection_set_id` È l'identificatore univoco locale del set di raccolta. *collection_set_id* viene **int** e deve avere un valore se *nome* è NULL.  
  
`[ @name = ] 'name'` È il nome del set di raccolta. *nome* viene **sysname** e deve avere un valore se *collection_set_id* è NULL.  
  
`[ @new_name = ] 'new_name'` È il nuovo nome per il set di raccolta. *new_name* viene **sysname**, e se utilizzato, non può essere una stringa vuota. *new_name* devono essere univoci. Per un elenco dei nomi dei set di raccolta correnti, eseguire una query sulla vista di sistema syscollector_collection_sets.  
  
`[ @target = ] 'target'` Riservato per utilizzi futuri.  
  
`[ @collection_mode = ] collection_mode` È il tipo di raccolta dati da utilizzare. *collection_mode* viene **smallint** e può avere uno dei valori seguenti:  
  
 0 - Modalità cache. La raccolta e il caricamento dei dati seguono una pianificazione differente. Specificare la modalità cache per la raccolta continua.  
  
 1 - Modalità non in cache. La raccolta e il caricamento dei dati seguono la stessa pianificazione. Specificare la modalità non in cache per la raccolta ad hoc o snapshot.  
  
 Se si modificano dalla modalità non in cache alla modalità cache (0), è necessario specificare anche *valore schedule_uid* oppure *schedule_name*.  
  
`[ @days_until_expiration = ] days_until_expiration` È il numero di giorni per cui i dati raccolti vengono salvati nel data warehouse di gestione. *days_until_expiration* viene **smallint**. *days_until_expiration* deve essere 0 o un numero intero positivo.  
  
`[ @proxy_id = ] proxy_id` È l'identificatore univoco per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account proxy dell'agente. *proxy_id* viene **int**.  
  
`[ @proxy_name = ] 'proxy_name'` È il nome del proxy. *proxy_name* viene **sysname** e ammette valori null.  
  
`[ @schedule_uid = ] 'schedule_uid'` È il GUID che punta a una pianificazione. *valore schedule_uid* viene **uniqueidentifier**.  
  
 Per ottenere *valore schedule_uid*, eseguire query sulla tabella di sistema sysschedules.  
  
 Quando *collection_mode* è impostata su 0, *valore schedule_uid* oppure *schedule_name* deve essere specificato. Quando *collection_mode* è impostato su 1, *valore schedule_uid* oppure *schedule_name* viene ignorato se specificato.  
  
`[ @schedule_name = ] 'schedule_name'` È il nome della pianificazione. *schedule_name* viene **sysname** e ammette valori null. Se specificato, *valore schedule_uid* deve essere NULL. Per ottenere *schedule_name*, eseguire query sulla tabella di sistema sysschedules.  
  
`[ @logging_level = ] logging_level` È il livello di registrazione. *logging_level* viene **smallint** con uno dei valori seguenti:  
  
 0 - Registrazione di informazioni di esecuzione ed eventi [!INCLUDE[ssIS](../../includes/ssis-md.md)] che tengono traccia dei seguenti elementi:  
  
-   Avvio/arresto dei set di raccolta  
  
-   Avvio/arresto dei pacchetti  
  
-   Informazioni sugli errori  
  
 1 - Registrazione di livello 0 e dei seguenti elementi:  
  
-   Statistiche di esecuzione  
  
-   Stato di avanzamento della raccolta in esecuzione continua  
  
-   Eventi di avviso da [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - Registrazione di livello 1 e di informazioni dettagliate sugli eventi di [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
 Il valore predefinito per *logging_level* è 1.  
  
`[ @description = ] 'description'` Rappresenta la descrizione del set di raccolta. *Descrizione* viene **nvarchar (4000)** .  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario eseguire sp_syscollector_update_collection_set nel contesto del database di sistema msdb.  
  
 Entrambi *collection_set_id* oppure *nome* deve avere un valore, non possono essere entrambi NULL. Per ottenere questi valori, eseguire una query sulla vista di sistema syscollector_collection_sets.  
  
 Se il set di raccolta è in esecuzione, è possibile aggiornare solo *valore schedule_uid* e *descrizione*. Per arrestare il set di raccolta, usare [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è necessaria l'appartenenza al ruolo predefinito del database dc_admin o dc_operator (con autorizzazione EXECUTE). Anche se dc_operator è in grado di eseguire questa stored procedure, i membri di questo ruolo possono modificare solo determinate proprietà. Le proprietà seguenti possono essere modificate solo da dc_admin:  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-renaming-a-collection-set"></a>A. Ridenominazione di un set di raccolta  
 Nell'esempio seguente viene rinominato un set di raccolta definito dall'utente.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. Modifica della modalità di raccolta da non in cache a cache  
 Nell'esempio seguente la modalità di raccolta viene modificata da non in cache a cache. Per eseguire questa modifica, è necessario specificare un ID oppure un nome della pianificazione.  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>C. Modifica di altri parametri del set di raccolta  
 Nell'esempio seguente vengono aggiornate diverse proprietà del set di raccolta denominato "Simple collection set test 2".  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysschedules &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
