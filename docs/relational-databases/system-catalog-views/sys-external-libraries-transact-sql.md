---
title: sys. external_libraries (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: ac6ad0872e813d36d9884a00f979b2a5284cd4a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73536166"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Supporta la gestione di librerie di pacchetti correlate a runtime esterni, ad esempio R, Python e Java.

> [!NOTE]
> In SQL Server 2017 sono supportati il linguaggio R e la piattaforma Windows. R, Python e Java nelle piattaforme Windows e Linux sono supportati in SQL Server 2019 e versioni successive.

## <a name="sysexternal_libraries"></a>sys.external_libraries

La vista del catalogo sys. external_libraries elenca una riga per ogni libreria esterna che è stata caricata nel database.

|Nome colonna |Tipo di dati | Descrizione|
|------|------|------|
|external_library_id |INT | ID dell'oggetto libreria esterna. |
|name |sysname |Nome della libreria esterna. È univoco all'interno del database per proprietario.|
|principal_id |INT |ID dell'entità a cui appartiene la libreria esterna. |
|Linguaggio | sysname | Nome della lingua o del runtime che supporta la libreria esterna. I valori validi sono ' R ',' Python ' è Java '. In futuro potrebbero essere aggiunti altri Runtime.|
|scope |INT |0 per ambito pubblico; 1 per ambito privato |  
|scope_desc |varchar (7) |Indica se il pacchetto è pubblico o privato.|

## <a name="see-also"></a>Vedere anche  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CREA LIBRERIA ESTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Installare nuovi pacchetti R in SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [Installare nuovi pacchetti Python in SQL Server](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  