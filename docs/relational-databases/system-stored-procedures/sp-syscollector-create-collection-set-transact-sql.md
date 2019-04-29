---
title: sp_syscollector_create_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be818ed92a3c5a7f9522a6142f5acc815077bd10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004288"
---
# <a name="spsyscollectorcreatecollectionset-transact-sql"></a>sp_syscollector_create_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un nuovo set di raccolta. È possibile utilizzare questa stored procedure per creare un set di raccolta personalizzato per la raccolta di dati.  
  
> [!WARNING]  
>  Nei casi in cui l'account di Windows configurato come proxy è un utente interattivo o non interattivo non ancora connesso, la directory di profilo non sarà presente e la creazione della directory di gestione temporanea non riuscirà. Se pertanto si utilizza un account proxy in un controller di dominio, è necessario specificare un account interattivo utilizzato almeno una volta in modo da assicurare la creazione della directory di profilo.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argomenti  
`[ @name = ] 'name'` È il nome del set di raccolta. *nome* viene **sysname** e non può essere una stringa vuota o NULL.  
  
 *nome* devono essere univoci. Per un elenco dei nomi dei set di raccolta correnti, eseguire una query sulla vista di sistema syscollector_collection_sets.  
  
`[ @target = ] 'target'` Riservato per utilizzi futuri. *nome* viene **nvarchar (128)** con un valore predefinito NULL.  
  
`[ @collection_mode = ] collection_mode` Specifica il modo in cui i dati vengono raccolti e archiviati. *collection_mode* viene **smallint** e può avere uno dei valori seguenti:  
  
 0 - Modalità cache. La raccolta e il caricamento dei dati seguono una pianificazione differente. Specificare la modalità cache per la raccolta continua.  
  
 1 - Modalità non in cache. La raccolta e il caricamento dei dati seguono la stessa pianificazione. Specificare la modalità non in cache per la raccolta ad hoc o snapshot.  
  
 Il valore predefinito per *collection_mode* è 0. Quando *collection_mode* è 0, *valore schedule_uid* oppure *schedule_name* deve essere specificato.  
  
`[ @days_until_expiration = ] days_until_expiration` È il numero di giorni per cui i dati raccolti vengono salvati nel data warehouse di gestione. *days_until_expiration* viene **smallint** con valore predefinito è 730 (due anni). *days_until_expiration* deve essere 0 o un numero intero positivo.  
  
`[ @proxy_id = ] proxy_id` È l'identificatore univoco per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account proxy dell'agente. *proxy_id* viene **int** con un valore predefinito NULL. Se specificato, *proxy_name* deve essere NULL. Per ottenere *proxy_id*, eseguire query sulla tabella di sistema sysproxies. Per accedere al proxy, il ruolo predefinito del database dc_admin deve disporre dell'autorizzazione appropriata. Per altre informazioni, vedere [creare un Proxy di SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
`[ @proxy_name = ] 'proxy_name'` È il nome dell'account proxy. *proxy_name* viene **sysname** con un valore predefinito NULL. Se specificato, *proxy_id* deve essere NULL. Per ottenere *proxy_name*, eseguire query sulla tabella di sistema sysproxies.  
  
`[ @schedule_uid = ] 'schedule_uid'` È il GUID che punta a una pianificazione. *valore schedule_uid* viene **uniqueidentifier** con un valore predefinito NULL. Se specificato, *schedule_name* deve essere NULL. Per ottenere *valore schedule_uid*, eseguire query sulla tabella di sistema sysschedules.  
  
 Quando *collection_mode* è impostata su 0, *valore schedule_uid* oppure *schedule_name* deve essere specificato. Quando *collection_mode* è impostato su 1, *valore schedule_uid* oppure *schedule_name* viene ignorato se specificato.  
  
`[ @schedule_name = ] 'schedule_name'` È il nome della pianificazione. *schedule_name* viene **sysname** con un valore predefinito NULL. Se specificato, *valore schedule_uid* deve essere NULL. Per ottenere *schedule_name*, eseguire query sulla tabella di sistema sysschedules.  
  
`[ @logging_level = ] logging_level` È il livello di registrazione. *logging_level* viene **smallint** con uno dei valori seguenti:  
  
 0 - Informazioni di esecuzione del log ed eventi [!INCLUDE[ssIS](../../includes/ssis-md.md)] che tengono traccia degli elementi seguenti:  
  
-   Avvio/arresto dei set di raccolta  
  
-   Avvio/arresto dei pacchetti  
  
-   Informazioni sugli errori  
  
 1 - Registrazione di livello 0 e dei seguenti elementi:  
  
-   Statistiche di esecuzione  
  
-   Stato di avanzamento della raccolta in esecuzione continua  
  
-   Eventi di avviso da [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - Registrazione di livello 1 e di informazioni dettagliate sugli eventi di [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 Il valore predefinito per *logging_level* è 1.  
  
`[ @description = ] 'description'` Rappresenta la descrizione del set di raccolta. *Descrizione* viene **nvarchar (4000)** con un valore predefinito NULL.  
  
`[ @collection_set_id = ] collection_set_id` È l'identificatore univoco locale del set di raccolta. *collection_set_id* viene **int** con OUTPUT ed è obbligatorio.  
  
`[ @collection_set_uid = ] 'collection_set_uid'` È il GUID del set di raccolta. *collection_set_uid* viene **uniqueidentifier** con OUTPUT e il valore predefinito NULL.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario eseguire sp_syscollector_create_collection_set nel contesto del database di sistema msdb.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>A. Creazione di un set di raccolta utilizzando valori predefiniti  
 Nell'esempio seguente viene creato un set di raccolta specificando solo i parametri obbligatori. `@collection_mode` non è obbligatorio, ma per la modalità di raccolta predefinita (cache) è necessario specificare un ID oppure un nome della pianificazione.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>B. Creazione di un set di raccolta utilizzando valori specificati  
 Nell'esempio seguente viene creato un set di raccolta specificando i valori per numerosi parametri.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [Creare un set di raccolta personalizzato che usa il tipo agente di raccolta Query T-SQL generico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Stored procedure dell'agente di raccolta dati &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
