---
title: Sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
ms.openlocfilehash: d56d0c69b9e3bae87dda9b55d241a1c040210ca9
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583054"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Supporta la gestione delle librerie di pacchetti correlati al runtime esterni, ad esempio R, Python e Java.

> [!NOTE]
> In SQL Server 2017 sono supportati il linguaggio R e la piattaforma Windows. R, Python e Java nelle piattaforme Windows e Linux sono supportati in SQL Server 2019 CTP 2.4.

## <a name="sysexternallibraries"></a>sys.external_libraries

Sys.external_libraries la vista del catalogo include una riga per ogni libreria esterna a cui è stato caricato nel database.

|Nome colonna |Tipo di dati | Descrizione|
|------|------|------|
|external_library_id |INT | ID dell'oggetto libreria esterna. |
|NAME |sysname |Nome della libreria esterna. È univoco all'interno del database per proprietario.|
|principal_id |INT |ID dell'entità che possiede questa libreria esterna. |
|language | sysname | Nome del linguaggio o runtime che supporta la libreria esterna. I valori validi sono 'R', 'Python' e 'Java'. I runtime aggiuntivi possono essere aggiunti in futuro.|
|ambito |INT |0 per ambito pubblico. 1 per l'ambito privato |  
|scope_desc |varchar(7) |Indica se il pacchetto è pubblica o privata|

## <a name="see-also"></a>Vedere anche  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Installare nuovi pacchetti R in SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [Installare nuovi pacchetti Python in SQL Server](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  