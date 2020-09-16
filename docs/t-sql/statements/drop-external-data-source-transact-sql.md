---
description: DROP EXTERNAL DATA SOURCE (Transact-SQL)
title: DROP EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8fd681675c2c15caf311bb0e3a132f3b39ea68b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547761"
---
# <a name="drop-external-data-source-transact-sql"></a>DROP EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE [sqlserver2016-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdbmi-asa-pdw.md)]

  Rimuove un'origine dati esterna PolyBase.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *external_data_source_name*  
 Nome dell'origine dati esterna da rimuovere.  
  
## <a name="metadata"></a>Metadati  
 Per visualizzare un elenco delle origini dati esterne, usare la vista di sistema sys.external_data_sources.  
  
```sql  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>Autorizzazioni  
 Richiede ALTER ANY EXTERNAL DATA SOURCE.  
  
## <a name="locking"></a>Blocco  
 Acquisisce un blocco condiviso sull'oggetto origine dati esterna.  
  
## <a name="general-remarks"></a>Osservazioni generali  
 La rimozione di un'origine dati esterna non comporta la rimozione dei dati esterni.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-basic-syntax"></a>R. Uso della sintassi di base  
  
```sql  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

