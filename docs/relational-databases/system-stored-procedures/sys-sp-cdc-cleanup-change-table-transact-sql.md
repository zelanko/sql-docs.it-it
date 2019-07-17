---
title: Sys. sp_cdc_cleanup_change_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
author: rothja
ms.author: jroth
ms.openlocfilehash: dcf68e23652eb81e163722f69d9645c7502af5b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106517"
---
# <a name="sysspcdccleanupchangetable-transact-sql"></a>sys.sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rimuove le righe dalla tabella delle modifiche nel database corrente basato sull'oggetto specificato *low_water_mark* valore. Questa stored procedure è fornita agli utenti che vogliono gestire direttamente il processo di pulizia della tabella delle modifiche. Tuttavia, è necessario fare attenzione poiché la procedura influisce su tutti gli utenti dei dati della tabella delle modifiche.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>Argomenti  
 [ @capture_instance =] '*capture_instance*'  
 Nome dell'istanza di acquisizione associata alla tabella delle modifiche. *capture_instance* viene **sysname**, non prevede alcun valore predefinito e non può essere NULL.  
  
 *capture_instance* deve denominare un'istanza di acquisizione che esiste nel database corrente.  
  
 [ @low_water_mark =] *low_water_mark*  
 Numero di sequenza del log (LSN) che deve essere utilizzato come nuovo limite minimo per il *istanza di acquisizione*. *low_water_mark* viene **binary(10)** , non prevede alcun valore predefinito.  
  
 Se il valore è diverso da null, deve apparire come valore start_lsn di una voce corrente nella [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabella. Se altre voci in cdc.lsn_time_mapping condividono la stessa ora di commit della voce identificata dal nuovo limite minimo, il valore LSN minore associato a tale gruppo di voci viene scelto come limite minimo.  
  
 Se il valore è impostato in modo esplicito su NULL, l'oggetto corrente *limite minimo* per il *istanza di acquisizione* viene usato per definire il limite superiore per l'operazione di pulizia.  
  
 [ @threshold=] '*eliminare soglia*'  
 Numero massimo di voci che possono essere eliminate utilizzando un'unica istruzione nel processo di pulizia. *delete_threshold* viene **bigint**, con un valore predefinito è 5000.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 Nessuna  
  
## <a name="remarks"></a>Note  
 sys.sp_cdc_cleanup_change_table esegue le operazioni seguenti:  
  
1.  Se il @low_water_mark parametro è diverso da NULL, imposta il valore di start_lsn per il *istanza di acquisizione* al nuovo *limite minimo*.  
  
    > [!NOTE]  
    >  Il nuovo limite minimo potrebbe non essere quello specificato nella chiamata alla stored procedure. Se altre voci nella tabella cdc.lsn_time_mapping condividono la stessa ora di commit, il valore start_lsn più piccolo rappresentato nel gruppo di voci viene selezionato come limite minimo modificato. Se il @low_water_mark parametro è NULL o il limite minimo corrente è maggiore di grande del nuovo limite minimo, il valore start_lsn per l'istanza di acquisizione non viene modificato.  
  
2.  Le voci della tabella delle modifiche con valori __$start_lsn inferiori al limite minimo vengono quindi eliminate. La soglia di eliminazione viene utilizzata per limitare il numero di righe eliminate in una singola transazione. Viene restituito un errore sull'eliminazione delle voci, che però non influisce sulle modifiche apportate al limite minimo dell'istanza di acquisizione in base alla chiamata.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Utilizzare sys.sp_cdc_cleanup_change_table nelle circostanze seguenti:  
  
-   I report del processo Cleanup Agent eliminano gli errori.  
  
     Un amministratore può eseguire questa stored procedure in modo esplicito per riprovare un'operazione non riuscita. Per ripetere la pulizia per un'istanza di acquisizione specifica, eseguire Sys. sp_cdc_cleanup_change_table, e si specifica NULL per il @low_water_mark parametro.  
  
-   I criteri basati sulla memorizzazione utilizzati dal processo di Cleanup Agent non sono adeguati.  
  
     Poiché questa stored procedure esegue il processo di pulizia per una singola istanza di acquisizione, è possibile utilizzarla per compilare una strategia di pulizia personalizzata in modo da applicare le regole di pulizia in base alla singola istanza di acquisizione.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al ruolo predefinito del database db_owner.  
  
## <a name="see-also"></a>Vedere anche  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  
