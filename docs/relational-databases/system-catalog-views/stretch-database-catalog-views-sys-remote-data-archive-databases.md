---
title: sys. remote_data_archive_databases (Transact-SQL) | Microsoft Docs
description: Informazioni su come sys. remote_data_archive_databases contiene una riga per ogni database remoto che archivia i dati da un database locale abilitato per l'estensione.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: e192a70c1d8f46b7ad89844a3b38019ab6364cc1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248150"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>Viste del catalogo Stretch Database-sys. remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Contiene una riga per ogni database remoto che archivia i dati da un database locale abilitato per l'estensione.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|Identificatore locale generato automaticamente del database remoto.|  
|**remote_database_name**|**sysname**|Nome del database remoto.|  
|**data_source_id**|**int**|Origine dati utilizzata per la connessione al server remoto|  
  
## <a name="see-also"></a>Vedere anche  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
