---
title: DATABASE_PRINCIPAL_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 337e64e16e1d1c2ab1d0130fde056eb0ef22df30
ms.sourcegitcommit: 869d4de6c807a37873b66e5479d2c5ceff9efb85
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2019
ms.locfileid: "67559435"
---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Questa funzione restituisce il numero ID di un'entità nel database corrente. Per altre informazioni sulle entità, vedere [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintassi  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>Argomenti  
*principal_name*  
Espressione di tipo **sysname** che rappresenta l'entità. Se *principal_name* viene omesso, `DATABASE_PRINCIPAL_ID` restituisce l'ID dell'utente corrente. `DATABASE_PRINCIPAL_ID` richiede le parentesi.
  
## <a name="return-types"></a>Tipi restituiti
**int**  
NULL se l'entità di database non esiste.
  
## <a name="remarks"></a>Remarks  
Usare `DATABASE_PRINCIPAL_ID` in un elenco di selezione, una clausola WHERE o in qualsiasi posizione che consente un'espressione. Per altre informazioni, vedere [Espressioni &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).
  
## <a name="examples"></a>Esempi  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>A. Recupero dell'ID dell'utente corrente  
In questo esempio viene restituito l'ID dell'entità di database per l'utente corrente.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. Recupero dell'ID di un'entità di database specifica  
In questo esempio viene restituito l'ID dell'entità di database per il ruolo di database `db_owner`.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche
[Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[Gerarchia delle autorizzazioni &#40;motore di database&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
