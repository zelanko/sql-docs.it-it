---
description: DROP SYNONYM (Transact-SQL)
title: DROP SYNONYM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SYNONYM
- DROP_SYNONYM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting synonyms
- synonyms [SQL Server], removing
- removing synonyms
- DROP SYNONYM statement
- dropping synonyms
ms.assetid: 23578932-e4de-4c39-a5a0-ce45139c4269
author: markingmyname
ms.author: maghan
ms.openlocfilehash: af16b7921358a12b87e9ab2ddbd6acaefee47d13
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379659"
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Rimuove un sinonimo da uno schema specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 *IF EXISTS*  
**Si applica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] alla [versione corrente](https://go.microsoft.com/fwlink/p/?LinkId=299658))
  
 Rimuove in modo condizionale il sinonimo solo se esiste già.  
  
 *schema*  
 Specifica lo schema in cui è contenuto il sinonimo. Se lo schema viene omesso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza lo schema predefinito dell'utente corrente.  
  
 *synonym_name*  
 Nome del sinonimo da eliminare.  
  
## <a name="remarks"></a>Commenti  
 I riferimenti ai sinonimi non sono associati a uno schema. È pertanto possibile eliminare un sinonimo in qualsiasi momento. I riferimenti ai sinonimi eliminati verranno trovati solo in fase di esecuzione.  
  
 È possibile creare, eliminare e fare riferimento ai sinonimi in SQL dinamico.  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eliminare un sinonimo, un utente deve soddisfare almeno una delle condizioni seguenti: L'utente deve essere:  
  
-   Il proprietario corrente di un sinonimo.  
  
-   Un utente autorizzato che dispone dell'autorizzazione CONTROL su un sinonimo.  
  
-   Un utente autorizzato che dispone dell'autorizzazione ALTER SCHEMA sullo schema contenitore.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene prima creato e quindi eliminato il sinonimo `MyProduct`.  
  
```sql  
USE tempdb;  
GO  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
-- Drop synonym MyProduct.  
USE tempdb;  
GO  
DROP SYNONYM MyProduct;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
