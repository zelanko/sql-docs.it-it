---
title: change_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4432d4c45bdecc6f5e1804427770d005adde0cd5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081286"
---
# <a name="cdcchangetables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce una riga per ogni tabella delle modifiche del database. Una tabella delle modiche viene creata quando l'acquisizione dei dati delle modifiche è abilitata in una tabella di origine. È consigliabile non eseguire una query direttamente sulle tabelle di sistema. Eseguire invece i [Sys. sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) stored procedure.  
  |Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID della tabella delle modifiche. Valore univoco all'interno di un database.|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], questa colonna restituisce sempre un valore 0.|  
|**source_object_id**|**int**|ID della tabella di origine abilitata per l'acquisizione dei dati delle modifiche.|  
|**capture_instance**|**sysname**|Nome dell'istanza di acquisizione utilizzata per denominare gli oggetti per il rilevamento specifici dell'istanza. Per impostazione predefinita, il nome è derivato dal nome dello schema di origine più il nome della tabella di origine nel formato *schemaname_sourcename*.|  
|**start_lsn**|**binary(10)**|Numero di sequenza del file di log (LSN) che rappresenta l'endpoint inferiore quando si esegue una query sui dati delle modifiche nella tabelle delle modifiche.<br /><br /> NULL = l'endpoint inferiore non è stato stabilito.|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] questa colonna restituisce sempre un valore NULL.|  
|**supports_net_changes**|**bit**|Il supporto per l'esecuzione di una query sulle modifiche totali è abilitato per la tabella delle modifiche.|  
|**has_drop_pending**|**bit**|Il processo di acquisizione ha ricevuto la notifica che la tabella di origine è stata eliminata.|  
|**role_name**|**sysname**|Nome del ruolo del database utilizzato per controllare l'accesso ai dati delle modifiche.<br /><br /> NULL = non è utilizzato un ruolo.|  
|**index_name**|**sysname**|Nome dell'indice utilizzato per identificare in modo univoco le righe nella tabella di origine. **index_name** è il nome dell'indice di chiave primaria della tabella di origine o il nome di un indice univoco specificato quando change data capture è stato abilitato nella tabella di origine.<br /><br /> NULL = la tabella di origine non ha avuto una chiave primaria quando l'acquisizione dei dati delle modifiche è stata abilitata e un indice univoco non è stato specificato quando l'acquisizione dei dati delle modifiche è stata abilitata.<br /><br /> Nota: Se change data capture è abilitato in una tabella in cui è presente una chiave primaria, la funzionalità change data capture utilizza l'indice indipendentemente dal fatto che le modifiche totali è abilitato o meno. Dopo l'abilitazione di Change Data Capture, sulla chiave primaria non è consentita alcuna modifica. Se nella tabella non è presente una chiave primaria, è ancora possibile abilitare la funzionalità Change Data Capture, ma solo se le modifiche totali sono impostate su false. Dopo l'abilitazione di Change Data Capture, è possibile creare una chiave primaria. È inoltre possibile modificare la chiave primaria perché la funzionalità Change Data Capture non la utilizza.|  
|**filegroup_name**|**sysname**|Nome del database filegroup contenente la tabella delle modifiche specificata.<br /><br /> NULL = la tabella delle modifiche si trova nel filegroup predefinito del database.|  
|**create_date**|**datetime**|Data in cui la tabella di origine è stata abilitata.|  
|**partition_switch**|**bit**|Indica se il **SWITCH PARTITION** del comando **ALTER TABLE** può essere eseguita in una tabella abilitata per change data capture. 0 indica che il cambio della partizione viene bloccato. Tramite le tabelle non partizionate viene restituito sempre 1.|  
  
## <a name="see-also"></a>Vedere anche  
 [Sys. sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
