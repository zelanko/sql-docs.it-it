---
description: Tabelle di backup e ripristino (Transact-SQL)
title: Tabelle di backup e ripristino (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system tables [SQL Server], backup tables
- backup system tables [SQL Server]
- system tables [SQL Server], restore tables
- restore system tables [SQL Server]
ms.assetid: aa615add-54e6-40f5-8b55-3728b26884ee
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a1d5e0638338cdf53d33eed310d23f1a124a7415
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463909"
---
# <a name="backup-and-restore-tables-transact-sql"></a>Tabelle di backup e ripristino (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Negli argomenti di questa sezione vengono descritte le tabelle di sistema in cui sono archiviate le informazioni utilizzate dalle operazioni di backup e ripristino di database.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)  
 Contiene una riga per ogni file di dati o di log di un database.  
  
 [backupfilegroup](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
 Contiene una riga per ogni filegroup in un database al momento del backup.  
  
 [backupmediafamily](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
 Contiene una riga per ogni gruppo di supporti.  
  
 [backupmediaset](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
 Contiene una riga per ogni set di supporti di backup.  
  
 [backupset](../../relational-databases/system-tables/backupset-transact-sql.md)  
 Contiene una riga per ogni set di backup.  
  
 [logmarkhistory](../../relational-databases/system-tables/logmarkhistory-transact-sql.md)  
 Contiene una riga per ogni transazione contrassegnata di cui è stato eseguito il commit.  
  
 [restorefile](../../relational-databases/system-tables/restorefile-transact-sql.md)  
 Contiene una riga per ogni file ripristinato, compresi i file ripristinati in modo indiretto in base al nome del filegroup.  
  
 [restorefilegroup](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)  
 Contiene una riga per ogni filegroup ripristinato.  
  
 [restorehistory](../../relational-databases/system-tables/restorehistory-transact-sql.md)  
 Contiene una riga per ogni operazione di ripristino.  
  
 [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md)  
 Contiene una riga per ogni pagina che ha restituito un errore 824 (con un limite massimo di 1.000 righe).  
  
 [sysopentapes](../../relational-databases/system-tables/sysopentapes-transact-sql.md)  
 Contiene una riga per ogni dispositivo nastro attualmente aperto.  
  
  
