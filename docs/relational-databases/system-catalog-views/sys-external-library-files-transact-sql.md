---
description: sys.external_library_files (Transact-SQL)
title: sys.external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: cfeae68d2895df4fa448a87d81e0fdb85aa74cd1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477452"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Elenca una riga per ogni file che costituisce una libreria esterna.

|Nome colonna |Tipo di dati |Descrizione|
|------|------|-----|
|external_library_id | INT |ID dell'oggetto libreria esterna. |
|contenuto |varbinary(max) |Contenuto dell'elemento del file di libreria esterno. |
|Piattaforma |TINYINT |ID della piattaforma host in cui è installato SQL Server. |
|platform_desc | nvarchar(60) |Nome della piattaforma host. I valori validi sono ' WINDOWS ',' LINUX '. |

### <a name="see-also"></a>Vedere anche  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREA LIBRERIA ESTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
