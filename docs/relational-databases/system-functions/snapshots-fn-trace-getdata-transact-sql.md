---
title: snapshots.fn_trace_getdata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: rothja
ms.author: jroth
ms.openlocfilehash: a85a911d4c9f5cd4565e9839f3be44a4e2366079
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067748"
---
# <a name="snapshotsfntracegetdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Questa funzione restituisce tutti gli eventi acquisiti per la traccia specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>Argomenti  
 *trace_info_id*  
 L'identificatore univoco per la chiave primaria nella tabella trace_info nei dati di gestione del data warehouse database. *trace_info_id* viene **int**.  
  
 *start_time*  
 Ora di avvio della traccia. *start_time* viene **datetime**.  
  
 *end_time*  
 Ora di fine della traccia. *end_time* viene **datetime**.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|\<Tutte le colonne di traccia >|\<Varia in base >|Dati di traccia della tabella snapshots.trace_data nel database del data warehouse di gestione.<br /><br /> È possibile ottenere un elenco di colonne per la traccia specificata mediante la query seguente:<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **Nota:** Le colonne restituite dalla funzione snapshots corrispondono ai valori nella colonna name della vista di sistema trace_columns. L'unica differenza è che la colonna GroupID non viene restituita dalla funzione.|  
  
## <a name="permissions"></a>Permissions  
 Richiede l'autorizzazione SELECT per mdw_reader.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
