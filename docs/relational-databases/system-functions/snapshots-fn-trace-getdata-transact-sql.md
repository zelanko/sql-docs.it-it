---
description: snapshots.fn_trace_getdata (Transact-SQL)
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
ms.openlocfilehash: f022a27c8a8e47cd12994d0d03ddb5af9a2f920c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464777"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Questa funzione restituisce tutti gli eventi acquisiti per la traccia specificata.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>Argomenti  
 *trace_info_id*  
 Identificatore univoco per la chiave primaria nella tabella snapshots. trace_info nel database di data warehouse di gestione. *trace_info_id* è di **tipo int**.  
  
 *start_time*  
 Ora di avvio della traccia. *start_time* è **DateTime**.  
  
 *end_time*  
 Ora di fine della traccia. *end_time* è **DateTime**.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|\<All trace columns>|\<Varies>|Dati di traccia della tabella snapshots.trace_data nel database del data warehouse di gestione.<br /><br /> È possibile ottenere un elenco di colonne per la traccia specificata mediante la query seguente:<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **Nota:** Le colonne restituite dalla funzione Snapshots. fn_trace_gettable corrispondono ai valori nella colonna Name della vista di sistema sys. trace_columns. L'unica differenza è che la colonna GroupID non viene restituita dalla funzione.|  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede l'autorizzazione SELECT per mdw_reader.  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](../../relational-databases/data-collection/data-collection.md)  
  
  
