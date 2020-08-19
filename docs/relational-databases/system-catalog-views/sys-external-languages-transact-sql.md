---
description: sys. external_languages (Transact-SQL)-SQL Server
title: sys. external_languages (Transact-SQL)-SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f44ce24baf72b5bb93e8d649d8fa4ebed1d6e99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420125"
---
# <a name="sysexternal_languages-transact-sql"></a>sys. external_languages (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Questa vista del catalogo fornisce un elenco delle lingue esterne nel database. **R** e **Python** sono nomi riservati e nessun linguaggio esterno può essere creato con tali nomi specifici.

## <a name="sysexternal_languages"></a>sys.external_languages

La vista del catalogo sys. external_languages elenca una riga per ogni lingua esterna nel database.

|Nome colonna |Tipo di dati | Descrizione|
|------|------|------|
|external_language_id |INT | ID della lingua esterna|
|Linguaggio |sysname |Nome della lingua esterna. Valore univoco all'interno del database. R e Python sono nomi riservati per istanza|
|create_date |datetime2 |Data e ora di creazione|
|principal_id |INT |ID dell'entità a cui appartiene la libreria esterna|

## <a name="see-also"></a>Vedere anche  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREA LINGUA ESTERNA](../../t-sql/statements/create-external-language-transact-sql.md) 
