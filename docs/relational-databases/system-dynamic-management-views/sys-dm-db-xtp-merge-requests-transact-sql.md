---
title: sys.dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f522fde05ce951575d3e02b3cdc4d3336056bd4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026810"
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

Traccia le richieste di unione del database. La richiesta di unione potrebbe essere stata generata da SQL Server o la richiesta potrebbe essere effettuata da un utente con [Sys. sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md).

> [!NOTE]
> Questa vista a gestione dinamica (DMV), sys.dm_db_xtp_merge_requests, esiste fino a Microsoft SQL Server 2014.
> Tuttavia, a partire da SQL Server 2016 questa DMV non è più valido.

## <a name="columns-in-the-report"></a>Colonne del report

| Nome colonna | Tipo di dati | Descrizione |
| :-- | :-- | :-- |
| request_state | tinyint | Stato della richiesta di unione:<br/>0 = Richiesta<br/>1 = In sospeso<br/>2 = installato<br/>3 = Abbandonata |
| request_state_desc | nvarchar(60) | Significati per lo stato corrente della richiesta:<br/><br/>Richieste - esiste una richiesta di unione.<br/>In sospeso - il merge è in corso l'elaborazione.<br/>Installato: l'unione è stata completata.<br/>Abbandonata - merge. Impossibile completare, forse a causa della mancanza di spazio di archiviazione. |
| destination_file_id | GUID | Identificatore univoco del file di destinazione per l'unione dei file di origine. |
| lower_bound_tsn | bigint | Timestamp minimo per il file di unione di destinazione. Il timestamp minimo per la transazione di tutti i file di origine da unire. |
| upper_bound_tsn | bigint | Timestamp massimo per il file di unione di destinazione. Il timestamp massimo per la transazione di tutti i file di origine da unire. |
| collection_tsn | bigint | Timestamp di raccolta della riga corrente.<br/><br/>Una riga nello stato Installata viene rimossa quando checkpoint_tsn è maggiore di collection_tsn.<br/><br/>Una riga nello stato Abbandonata viene rimossa quando checkpoint_tsn è minore di collection_tsn. |
| checkpoint_tsn | bigint | Ora di avvio del checkpoint.<br/><br/>Tutte le eliminazioni eseguite da transazioni con un timestamp minore di questo vengono incluse nel nuovo file di dati. Le eliminazioni rimanenti vengono spostate nel file differenziale di destinazione. |
| sourcenumber_file_id | GUID | Fino a 16 ID di file interne che identificano i file di origine nell'unione. |

## <a name="permissions"></a>Permissions

È richiesta l'autorizzazione VIEW DATABASE STATE per il database corrente.

## <a name="see-also"></a>Vedere anche

[Tabella con ottimizzazione per la memoria viste a gestione dinamica (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
