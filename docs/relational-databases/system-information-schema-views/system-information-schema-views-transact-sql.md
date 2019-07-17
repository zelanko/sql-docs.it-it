---
title: Viste degli schemi delle informazioni del sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- information schema views
- schemas [SQL Server], information schema views
- metadata [SQL Server], views
- views [SQL Server], information schema
- system views [SQL Server], information schema
ms.assetid: 7e9f1dfe-27e9-40e7-8fc7-bfc5cae6be10
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2d9216686cca6ed35d089130098026d5d958638a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078456"
---
# <a name="system-information-schema-views-transact-sql"></a>Viste degli schemi delle informazioni del sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Una vista dello schema delle informazioni rappresenta uno dei metodi disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ottenere metadati. Le viste degli schemi delle informazioni offrono una panoramica interna dei metadati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] indipendente dalle tabelle di sistema, nonché garantiscono il corretto funzionamento delle applicazioni anche se sono state apportate modifiche significative alle tabelle di sistema sottostanti. Le viste degli schemi delle informazioni incluse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono conformi alla definizione dello standard ISO per INFORMATION_SCHEMA.  
  
> [!IMPORTANT]  
>  Alle viste degli schemi delle informazioni sono state apportate alcune modifiche che non garantiscono la compatibilità con le versioni precedenti. Tali modifiche sono descritte negli argomenti specifici relativi alle viste interessate.  
  
 Per i riferimenti al server corrente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta i nomi composti da tre parti. La stessa convenzione di denominazione viene adottata anche dallo standard ISO. I nomi utilizzati nelle due convenzioni di denominazione sono tuttavia diversi. Le viste degli schemi delle informazioni sono definite in uno schema speciale denominato INFORMATION_SCHEMA. Questo schema è incluso in ogni database. Ogni vista dello schema delle informazioni include metadati per tutti gli oggetti dati archiviati nel database specifico. Nella tabella seguente sono riportate le relazioni tra i nomi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e i nomi SQL standard.  
  
|Nome di SQL Server|Nome SQL standard equivalente|  
|---------------------|-----------------------------------------------|  
|Database|Catalogo|  
|schema|schema|  
|Object|Object|  
|Tipo di dati definito dall'utente|Domain|  
  
 Questa convenzione di mapping dei nomi è valida per le viste di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compatibili con lo standard ISO riportate di seguito.  
  
|||  
|-|-|  
|[CHECK_CONSTRAINTS](../../relational-databases/system-information-schema-views/check-constraints-transact-sql.md)|[REFERENTIAL_CONSTRAINTS](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)|  
|[COLUMN_DOMAIN_USAGE](../../relational-databases/system-information-schema-views/column-domain-usage-transact-sql.md)|[ROUTINES](../../relational-databases/system-information-schema-views/routines-transact-sql.md)|  
|[COLUMN_PRIVILEGES](../../relational-databases/system-information-schema-views/column-privileges-transact-sql.md)|[ROUTINE_COLUMNS](../../relational-databases/system-information-schema-views/routine-columns-transact-sql.md)|  
|[COLUMNS](../../relational-databases/system-information-schema-views/columns-transact-sql.md)|[SCHEMATA](../../relational-databases/system-information-schema-views/schemata-transact-sql.md)|  
|[CONSTRAINT_COLUMN_USAGE](../../relational-databases/system-information-schema-views/constraint-column-usage-transact-sql.md)|[TABLE_CONSTRAINTS](../../relational-databases/system-information-schema-views/table-constraints-transact-sql.md)|  
|[CONSTRAINT_TABLE_USAGE](../../relational-databases/system-information-schema-views/constraint-table-usage-transact-sql.md)|[TABLE_PRIVILEGES](../../relational-databases/system-information-schema-views/table-privileges-transact-sql.md)|  
|[DOMAIN_CONSTRAINTS](../../relational-databases/system-information-schema-views/domain-constraints-transact-sql.md)|[TABLES](../../relational-databases/system-information-schema-views/tables-transact-sql.md)|  
|[DOMAINS](../../relational-databases/system-information-schema-views/domains-transact-sql.md)|[VIEW_COLUMN_USAGE](../../relational-databases/system-information-schema-views/view-column-usage-transact-sql.md)|  
|[KEY_COLUMN_USAGE](../../relational-databases/system-information-schema-views/key-column-usage-transact-sql.md)|[VIEW_TABLE_USAGE](../../relational-databases/system-information-schema-views/view-table-usage-transact-sql.md)|  
|[PARAMETERS](../../relational-databases/system-information-schema-views/parameters-transact-sql.md)|[VIEWS](../../relational-databases/system-information-schema-views/views-transact-sql.md)|  
  
 Alcune viste contengono inoltre riferimenti a classi di dati diverse, ad esempio dati di tipo carattere o dati binari.  
  
 Quando si fa riferimento alle viste dello schema delle informazioni, è necessario utilizzare un nome completo che includa il nome schema `INFORMATION_SCHEMA`. Ad esempio:  
  
```  
SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = N'Product';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Viste di sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
