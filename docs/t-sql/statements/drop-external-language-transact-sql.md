---
title: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3767bec1807b68df3eb3f82287a5c871d653a286
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68892979"
---
# <a name="drop-external-library-transact-sql"></a>DROP EXTERNAL LIBRARY (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Elimina un linguaggio esterno esistente.

## <a name="syntax"></a>Sintassi

```text
DROP EXTERNAL LANGUAGE <language_name>
```

### <a name="arguments"></a>Argomenti

**language_name**

I linguaggi sono oggetti con ambito di database. I nomi dei linguaggi devono essere univoci all'interno del database.

## <a name="permissions"></a>Autorizzazioni

Per eliminare un linguaggio è necessario il privilegio ALTER ANY EXTERNAL LANGUAGE. Per impostazione predefinita, anche un proprietario del database o il proprietario dell'oggetto può eliminare un linguaggio esterno.

> [!NOTE]
> Si noti che prima di rimuovere un linguaggio esterno, è necessario rimuovere le librerie esterne che fanno riferimento al linguaggio esterno.

### <a name="return-values"></a>Valori restituiti

Se l'istruzione ha esito positivo viene restituito un messaggio informativo.

## <a name="remarks"></a>Osservazioni

Prima di poter eliminare un linguaggio esterno, è necessario eliminare tutte le librerie esterne per il linguaggio specificato.

## <a name="examples"></a>Esempi

Creare un linguaggio esterno **Java**:

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

Eliminare il linguaggio esterno:

```sql
DROP EXTERNAL LANGUAGE Java;
```

## <a name="see-also"></a>Vedere anche

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
