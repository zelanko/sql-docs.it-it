---
description: HAS_DBACCESS (Transact-SQL)
title: HAS_DBACCESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HAS_DBACCESS_TSQL
- HAS_DBACCESS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- permissions [SQL Server], user access status
- HAS_DBACCESS
- checking permission status
- verifying permission status
- users [SQL Server], access rights status
- testing permissions
- status information [SQL Server], user access
ms.assetid: 99b43a72-0722-4a7b-a493-bdee1c74c7b9
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 488d2833727f68ec5df9f9ccc9f0ef36b019c7ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422775"
---
# <a name="has_dbaccess-transact-sql"></a>HAS_DBACCESS (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Restituisce informazioni che indicano se l'utente dispone o meno delle autorizzazioni per l'accesso al database specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
HAS_DBACCESS ( 'database_name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argomenti
 '*database_name*'  
 Nome del database di cui l'utente richiede informazioni relative all'accesso. *database_name* è di tipo **sysname**.  
  
## <a name="return-types"></a>Tipi restituiti  
 **int**  
  
## <a name="remarks"></a>Osservazioni  
 HAS_DBACCESS restituisce 1 se l'utente può accedere al database, 0 in caso contrario e NULL se il nome del database non è valido.  
  
 HAS_DBACCESS restituisce 0 se il database è offline o sospetto.  
  
 HAS_DBACCESS restituisce 0 se il database è in modalità utente singolo ed è utilizzato da un altro utente.  
  
## <a name="permissions"></a>Autorizzazioni  
 È richiesta l'appartenenza al ruolo public.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene verificato se l'utente dispone delle autorizzazioni di accesso al database `AdventureWorks2012`.  
  
```  
SELECT HAS_DBACCESS('AdventureWorks2012');  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene verificato se l'utente dispone delle autorizzazioni di accesso al database `AdventureWorksPDW2012`.  
  
```  
SELECT HAS_DBACCESS('AdventureWorksPDW2012');  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [IS_MEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)  
  
  

