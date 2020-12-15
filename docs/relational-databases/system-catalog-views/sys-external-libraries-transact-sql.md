---
description: sys.external_libraries (Transact-SQL)
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: 540420eee8f6de671df54ace8af9fbe1fe0c501d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477502"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Supporta la gestione di librerie di pacchetti correlate a runtime esterni, ad esempio R, Python e Java.

> [!NOTE]
> In SQL Server 2017 sono supportati il linguaggio R e la piattaforma Windows. R, Python e Java nelle piattaforme Windows e Linux sono supportati in SQL Server 2019 e versioni successive. In Istanza gestita SQL di Azure sono supportati R e Python.

## <a name="sysexternal_libraries"></a>sys.external_libraries

Nella vista del catalogo sys.external_libraries viene elencata una riga per ogni libreria esterna che è stata caricata nel database.

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
+ [Installare nuovi pacchetti R](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [Installare nuovi pacchetti Python](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  
