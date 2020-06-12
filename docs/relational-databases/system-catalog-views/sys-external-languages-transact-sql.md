---
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
ms.openlocfilehash: 053a7cdcf21775525b0eb8d46bbbfdf03098e03c
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627276"
---
# <a name="sysexternal_languages-transact-sql"></a>sys. external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

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
