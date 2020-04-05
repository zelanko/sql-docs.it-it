---
title: sys.external_libraries (Transact-SQL) Documenti Microsoft
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6b1bfc00b403fa76f692db78593ed4c0e6b53ce8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664428"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Supporta la gestione delle librerie di pacchetti correlate a runtime esterni, ad esempio R, Python e Java.

> [!NOTE]
> In SQL Server 2017 sono supportati il linguaggio R e la piattaforma Windows. R, Python e Java nelle piattaforme Windows e Linux sono supportati in SQL Server 2019 e versioni successive.

## <a name="sysexternal_libraries"></a>sys.external_libraries

La vista del catalogo sys.external_libraries elenca una riga per ogni libreria esterna caricata nel database.

|Nome colonna |Tipo di dati | Descrizione|
|------|------|------|
|external_library_id |INT | ID dell'oggetto libreria esterno. |
|name |sysname |Nome della libreria esterna. È univoco all'interno del database per proprietario.|
|principal_id |INT |ID dell'entità proprietaria della libreria esterna. |
|Linguaggio | sysname | Nome della lingua o del runtime che supporta la libreria esterna. I valori validi sono 'R', 'Python' e 'Java'. Ulteriori runtime potrebbero essere aggiunti in futuro.|
|scope |INT |0 per l'ambito pubblico; 1 per ambito privato |  
|scope_desc |varchar(7) |Indica se il pacchetto è pubblico o privato|

## <a name="see-also"></a>Vedere anche  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREA LIBRERIA ESTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Installare nuovi pacchetti R in SQL Server](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [Installare nuovi pacchetti Python in SQL Server](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  