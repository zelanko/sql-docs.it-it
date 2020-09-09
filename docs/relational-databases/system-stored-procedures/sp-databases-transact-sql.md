---
description: sp_databases (Transact-SQL)
title: sp_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 90fbcbf710f1779ad011163641aa61b14b33c65b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549897"
---
# <a name="sp_databases-transact-sql"></a>sp_databases (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elenca i database disponibili in un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o accessibili tramite un gateway di database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 Nessuno  
  
## <a name="result-sets"></a>Set di risultati  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|Nome del database. In [!INCLUDE[ssDE](../../includes/ssde-md.md)] questa colonna rappresenta il nome del database archiviato nella vista del catalogo **sys. databases** .|  
|**DATABASE_SIZE**|**int**|Dimensioni del database in kilobyte.|  
|**COMMENTI**|**varchar (254)**|In [!INCLUDE[ssDE](../../includes/ssde-md.md)] questo campo restituisce sempre NULL.|  
  
## <a name="remarks"></a>Osservazioni  
 I nomi di database restituiti possono essere utilizzati come parametri nell'istruzione USE per modificare il contesto del database corrente.  
  
 **sp_databases** non ha un equivalente in Open Database Connectivity (ODBC).  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'autorizzazione CREATE DATABASE, ALTER ANY DATABASE o VIEW ANY DEFINITION ed è necessario disporre dell'autorizzazione di accesso al database. Non è possibile negare l'autorizzazione VIEW ANY DEFINITION.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrata l'esecuzione di `sp_databases`.  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;&#41;Transact-SQL ](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
