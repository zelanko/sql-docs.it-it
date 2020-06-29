---
title: sys. external_library_files (Transact-SQL) | Microsoft Docs
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 8068df01ade7361c542150a3ee1f98ac137110e8
ms.sourcegitcommit: a0ebbcb717f09d3614de5ce9eb9f3c00f0a45f81
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85409360"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

Elenca una riga per ogni file che costituisce una libreria esterna.

|Nome colonna |Tipo di dati |Descrizione|
|------|------|-----|
|external_library_id | INT |ID dell'oggetto libreria esterna. |
|contenuto |varbinary(max) |Contenuto dell'elemento del file di libreria esterno. |
|Piattaforma |TINYINT |ID della piattaforma host in cui è installato SQL Server. |
|platform_desc | nvarchar(60) |Nome della piattaforma host. I valori validi sono ' WINDOWS ',' LINUX '. |

### <a name="see-also"></a>Vedi anche  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CREA LIBRERIA ESTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
