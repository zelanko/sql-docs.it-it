---
title: sys.sp_cdc_scan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1e7651c6df4a277d72a71c0cdb8a5910ae19ba76
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536783"
---
# <a name="sysspcdcscan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esegue l'operazione di analisi del log di Change Data Capture.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>Argomenti  
`[ @maxtrans = ] max_trans` Numero massimo di transazioni da elaborare in ogni ciclo di analisi. *max_trans* viene **int** con valore predefinito è 500.  
  
`[ @maxscans = ] max_scans` Numero massimo di cicli di analisi da eseguire per estrarre tutte le righe dal log. *max_scans* viene **int** con valore predefinito è 10.  
  
`[ @continuous = ] continuous` Indica se la stored procedure deve terminare dopo l'esecuzione di un singolo ciclo di analisi (0) o eseguita in modo continuo, sospendendo l'esecuzione per il periodo di tempo specificato da *polling_interval* prima di rieseguire il ciclo di analisi (1). *Continuous* viene **tinyint** con valore predefinito è 0.  
  
`[ @pollinginterval = ] polling_interval` Numero di secondi tra cicli di analisi di log. *polling_interval* viene **bigint** con valore predefinito è 0.  
  
## <a name="return-code-values"></a>Valori restituiti  
 **0** (esito positivo) o **1** (errore)  
  
## <a name="result-sets"></a>Set di risultati  
 None  
  
## <a name="remarks"></a>Note  
 sys.sp_cdc_scan viene chiamata internamente da sys.sp_MScdc_capture_job se il processo di acquisizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene utilizzato da Change Data Capture. La procedura non può essere eseguita in modo esplicito quando un'operazione di analisi del log di change data capture è già attiva o quando il database è abilitato per la replica transazionale. Questa stored procedure deve essere utilizzata dagli amministratori che desiderano personalizzare il comportamento del processo di acquisizione che viene configurato automaticamente.  
  
## <a name="permissions"></a>Permissions  
 Richiede l'appartenenza al ruolo predefinito del database db_owner.  
  
## <a name="see-also"></a>Vedere anche  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
