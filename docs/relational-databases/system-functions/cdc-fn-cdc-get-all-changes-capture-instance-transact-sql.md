---
title: cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt;  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cd8520a26b28c16876163cf8f2c0f7a57b3c33ad
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54136031"
---
# <a name="cdcfncdcgetallchangesltcaptureinstancegt--transact-sql"></a>cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt;  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ciascuna modifica applicata alla tabella di origine all'interno dell'intervallo del numero di sequenza del file di log (LSN) specificato. Se a una riga di origine vengono applicate più modifiche durante l'intervallo, ogni modifica è riportata nel set di risultati restituito. Oltre alla restituzione dei dati delle modifiche, quattro colonne di metadati forniscono le informazioni necessarie per applicare le modifiche a un'altra origine dati. Al contenuto delle colonne dei metadati e alle righe restituite nel set di risultati vengono applicate le opzioni di filtro di riga. Quando è specificata l'opzione di filtro di riga 'all', per l'identificazione di ogni modifica è disponibile esattamente una riga. Quando è specificata l'opzione 'all update old', le operazioni di aggiornamento sono rappresentate su due righe: una contiene i valori delle colonne acquisite prima dell'aggiornamento e l'altra contiene i valori delle colonne acquisite dopo l'aggiornamento.  
  
 Questa funzione di enumerazione viene creata nel momento in cui una tabella di origine è abilitata per Change Data Capture. Il nome della funzione è derivato e utilizza il formato **CDC. fn_cdc_get_all_changes _**_capture_instance_ in cui *capture_instance* è il valore specificato per l'acquisizione istanza quando la tabella di origine è abilitata per change data capture.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>Argomenti  
 *from_lsn*  
 Valore LSN che rappresenta l'endpoint inferiore dell'intervallo LSN da includere nel set di risultati. *from_lsn* viene **binary(10)**.  
  
 Solo le righe di [cdc.&#91; capture_instance&#93;CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) con un valore nella tabella delle modifiche **_ $start_lsn** maggiore o uguale a *from_lsn* sono inclusi nel set di risultati.  
  
 *to_lsn*  
 Valore LSN che rappresenta l'endpoint superiore dell'intervallo LSN da includere nel set di risultati. *to_lsn* viene **binary(10)**.  
  
 Solo le righe di [cdc.&#91; capture_instance&#93;CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) con un valore nella tabella delle modifiche **_ $start_lsn** minore o uguale a *from_lsn* o uguale a *to_lsn* sono inclusi nel set di risultati.  
  
 <row_filter_option> ::= { all | all update old }  
 Opzione applicata al contenuto delle colonne dei metadati e alle righe restituite nel set di risultati.  
  
 Le opzioni possibili sono le seguenti:  
  
 all  
 Restituisce tutte le modifiche all'interno dell'intervallo LSN specificato. Per le modifiche dovute a un'operazione di aggiornamento, questa opzione restituisce solo la riga che contiene i nuovi valori dopo l'applicazione dell'aggiornamento.  
  
 all update old  
 Restituisce tutte le modifiche all'interno dell'intervallo LSN specificato. Per le modifiche dovute a un'operazione di aggiornamento, questa opzione restituisce sia la riga che contiene i valori di colonna precedenti l'aggiornamento che la riga che contiene i valori di colonna successivi all'aggiornamento.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|Numero LSN di commit associato alla modifica. Mantiene l'ordine del commit della modifica. Le modifiche di cui è stato eseguito il commit nella stessa transazione condividono lo stesso valore LSN di commit.|  
|**__$seqval**|**binary(10)**|Valore di sequenza utilizzato per ordinare le modifiche a una riga all'interno di una transazione.|  
|**__$operation**|**int**|Identifica l'operazione DML (Data Manipulation Language) necessaria per applicare la riga di dati di modifica all'origine dati di destinazione. I possibili valori sono i seguenti:<br /><br /> 1 = eliminazione<br /><br /> 2 = inserimento<br /><br /> 3 = aggiornamento (i valori di colonna acquisiti sono quelli precedenti l'aggiornamento). Questo valore si applica solo quando è specificata l'opzione di filtro di riga 'all update old'.<br /><br /> 4 = aggiornamento (i valori di colonna acquisiti sono quelli successivi all'aggiornamento).|  
|**__$update_mask**|**varbinary(128)**|Maschera di bit in cui a ogni colonna acquisita identificata per l'istanza di acquisizione corrisponde un bit. Questo valore ha tutti i bit definiti impostata su 1 quando **_ $operation** = 1 o 2. Quando **_ $operation** = 3 o 4, solo i bit corrispondenti a colonne modificate sono impostati su 1.|  
|**\<colonne della tabella di origine acquisite>**|variabile|Le colonne rimanenti restituite dalla funzione sono le colonne acquisite identificate quando l'istanza di acquisizione è stata creata. Se nessuna colonna è stata specificata nell'elenco delle colonne acquisite, vengono restituite tutte le colonne nella tabella di origine.|  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al **sysadmin** ruolo predefinito del server oppure **db_owner** ruolo predefinito del database. Per tutti gli altri utenti, è richiesta l'autorizzazione SELECT su tutte le colonne acquisite nella tabella di origine e, se è stato definito un ruolo di controllo per l'istanza di acquisizione, l'appartenenza a tale ruolo del database. Quando il chiamante non dispone dell'autorizzazione per visualizzare i dati di origine, la funzione restituisce l'errore 229 ("autorizzazione SELECT negata per l'oggetto 'fn_cdc_get_all_changes _...', database '\<DatabaseName >', schema 'cdc'.").  
  
## <a name="remarks"></a>Note  
 Se l'intervallo LSN specificato è esterno alla cronologia di rilevamento delle modifiche per l'istanza di acquisizione, la funzione restituisce l'errore 208 ("Numero di argomenti insufficienti per la procedura o la funzione cdc.fn_cdc_get_all_changes").  
  
 Colonne di tipo di dati **immagine**, **testo**, e **ntext** viene sempre assegnato un valore NULL valore quando **_ $operation** = 1 o **_ $ operazione** = 3. Colonne di tipo di dati **varbinary (max)**, **varchar (max)**, o **nvarchar (max)** vengono assegnati un NULL valore quando **_ $operation** = 3 a meno che la colonna modificata durante l'aggiornamento. Quando **_ $operation** = 1, queste colonne vengono assegnate i rispettivi valori al momento dell'eliminazione. Le colonne calcolate incluse in un'istanza di acquisizione hanno sempre un valore NULL.  
  
## <a name="examples"></a>Esempi  
 Diversi [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono disponibili modelli che illustrano come usare le funzioni di query di change data capture. Questi modelli sono disponibili nel **View** dal menu [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per altre informazioni, vedere [Esplora modelli](../../ssms/template/template-explorer.md).  
  
 In questo esempio viene illustrato il `Enumerate All Changes for Valid Range Template`. Viene utilizzata la funzione `cdc.fn_cdc_get_all_changes_HR_Department` per riportare tutte le modifiche attualmente disponibili per l'istanza di acquisizione `HR_Department`, definita per tabella di origine HumanResources.Department nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [Informazioni su Change Data Capture &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
