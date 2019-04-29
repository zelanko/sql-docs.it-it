---
title: sp_syscollector_create_collection_item (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_item
- sp_syscollector_create_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_create_collection_item
- data collector [SQL Server], stored procedures
ms.assetid: 60dacf13-ca12-4844-b417-0bc0a8bf0ddb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1e155fb51bd5f78a3c4a639e9233746131ddf6f5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63004148"
---
# <a name="spsyscollectorcreatecollectionitem-transact-sql"></a>sp_syscollector_create_collection_item (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un elemento della raccolta in un set di raccolta definito dall'utente. Un elemento della raccolta definisce i dati da raccogliere e la frequenza di raccolta.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_syscollector_create_collection_item   
      [ @collection_set_id = ] collection_set_id   
    , [ @collector_type_uid = ] 'collector_type_uid'  
    , [ @name = ] 'name'   
    , [ [ @frequency = ] frequency ]  
    , [ @parameters = ] 'parameters'  
    , [ @collection_item_id = ] collection_item_id OUTPUT  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @collection_set_id = ] *collection_set_id*  
 Identificatore univoco locale del set di raccolta. *collection_set_id* viene **int**.  
  
 [ @collector_type_uid = ] '*collector_type_uid*'  
 GUID che identifica il tipo di agente di raccolta dati da utilizzare per questo elemento *collector_type_uid* viene **uniqueidentifier** non prevede alcun valore predefinito... Per un elenco di tipi di agenti di raccolta, eseguire una query sulla vista di sistema syscollector_collector_types.  
  
 [ @name =] '*nome*'  
 Nome dell'elemento della raccolta. *nome* viene **sysname** e non può essere una stringa vuota o NULL.  
  
 *nome* devono essere univoci. Per un elenco dei nomi degli elementi della raccolta correnti, eseguire una query sulla vista di sistema syscollector_collection_items.  
  
 [ @frequency =] *frequenza*  
 Utilizzato per specificare la frequenza di raccolta dei dati da parte di questo elemento della raccolta, espressa in secondi. *frequenza* viene **int**, con un valore predefinito è 5. Il valore minimo che è possibile specificare è 5 secondi.  
  
 Se il set di raccolta è impostato sulla modalità non in cache, la frequenza viene ignorata in quanto in questa modalità la raccolta e il caricamento dei dati vengono eseguiti in base alla pianificazione specificata per il set di raccolta. Per visualizzare la modalità di raccolta del set di raccolta, eseguire una query di [syscollector_collection_sets](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md) vista di sistema.  
  
 [ @parameters =] '*parametri*'  
 Parametri di input per il tipo agente di raccolta. *i parametri* viene **xml** con valore predefinito è NULL. Il *parametri* dello schema deve corrispondere allo schema di parametri del tipo di agente di raccolta.  
  
 [ @collection_item_id = ] *collection_item_id*  
 Identificatore univoco che identifica l'elemento del set di raccolta. *collection_item_id* viene **int** e ha OUTPUT.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="remarks"></a>Note  
 È necessario eseguire sp_syscollector_create_collection_item nel contesto del database di sistema msdb.  
  
 Il set di raccolta al quale viene aggiunto l'elemento deve essere arrestato prima della creazione dell'elemento della raccolta. Non è possibile aggiungere elementi della raccolta ai set di raccolta di sistema.  
  
## <a name="permissions"></a>Permissions  
 Per eseguire questa procedura, è richiesta l'appartenenza al ruolo predefinito del database dc_admin (con autorizzazione EXECUTE) .  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creato un elemento della raccolta basato sul tipo di raccolta `Generic T-SQL Query Collector Type` e successivamente tale elemento viene aggiunto al set di raccolta denominato `Simple collection set test 2`. Per creare la raccolta specificata impostata, eseguire l'esempio B nel [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
```  
USE msdb;  
GO  
DECLARE @collection_item_id int;  
DECLARE @collection_set_id int = (SELECT collection_set_id   
                                  FROM syscollector_collection_sets  
                                  WHERE name = N'Simple collection set test 2');  
DECLARE @collector_type_uid uniqueidentifier =   
    (SELECT collector_type_uid  
     FROM syscollector_collector_types  
     WHERE name = N'Generic T-SQL Query Collector Type');  
DECLARE @params xml =   
    CONVERT(xml, N'\<ns:TSQLQueryCollector xmlns:ns="DataCollectorType">  
            <Query>  
                <Value>SELECT * FROM sys.objects</Value>  
                <OutputTable>MyOutputTable</OutputTable>  
            </Query>  
            <Databases>   
                <Database> UseSystemDatabases = "true"   
                           UseUserDatabases = "true"  
                </Database>  
            </Databases>  
         \</ns:TSQLQueryCollector>');  
  
EXEC sp_syscollector_create_collection_item  
    @collection_set_id = @collection_set_id,  
    @collector_type_uid = @collector_type_uid,  
    @name = 'My custom TSQL query collector item',  
    @frequency = 6000,  
    @parameters = @params,  
    @collection_item_id = @collection_item_id OUTPUT;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)   
 [sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)   
 [syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)   
 [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
