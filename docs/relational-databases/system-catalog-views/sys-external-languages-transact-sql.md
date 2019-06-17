---
title: Sys.external_languages (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
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
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1cef52f066a07032240d17f88297b02ba3f7e5fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995119"
---
# <a name="sysexternallanguages-transact-sql"></a>Sys.external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questa vista del catalogo fornisce un elenco delle lingue esterne nel database. **R** e **Python** sono nomi riservati e nessun linguaggio esterno può essere creato con tali nomi specifici.

## <a name="sysexternallanguages"></a>sys.external_languages

Sys.external_languages la vista del catalogo include una riga per ogni lingua esterna nel database.

|Nome colonna |Tipo di dati | Descrizione|
|------|------|------|
|external_language_id |INT | ID della lingua esterna|
|language |sysname |Nome del linguaggio esterno. Valore univoco all'interno del database. R e Python sono nomi riservati per ogni istanza|
|create_date |datetime2 |Data e ora di creazione|
|principal_id |INT |ID dell'entità che possiede questa libreria esterna|

## <a name="see-also"></a>Vedere anche  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREAZIONE DI LINGUAGGIO ESTERNO](../../t-sql/statements/create-external-language-transact-sql.md) 
