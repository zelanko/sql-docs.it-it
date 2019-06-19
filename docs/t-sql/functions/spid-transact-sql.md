---
title: '@@SPID (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@SPID'
- '@@SPID_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SPID function'
- session_id
- server process IDs [SQL Server]
- IDs [SQL Server], user processes
- SPID
- session IDs [SQL Server]
- process ID of current user process
ms.assetid: df955d32-8194-438e-abee-387eebebcbb7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7be3bc3a5d49dc7ef978c6bc2dba98f97258d5cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65947716"
---
# <a name="x40x40spid-transact-sql"></a>&#x40;&#x40;SPID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce l'ID di sessione del processo utente corrente.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
@@SPID  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 **smallint**  
  
## <a name="remarks"></a>Remarks  
 È possibile usare la funzione @@SPID per identificare il processo utente corrente nell'output di **sp_who**.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene restituito l'ID, il nome dell'account di accesso e il nome utente della sessione utente corrente.  
  
```  
SELECT @@SPID AS 'ID', SYSTEM_USER AS 'Login Name', USER AS 'User Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Login Name                     User Name                       
------ ------------------------------ ------------------------------  
54     SEATTLE\joanna                 dbo                             
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene restituito l'ID sessione di [!INCLUDE[ssDW](../../includes/ssdw-md.md)], l'ID sessione del nodo di controllo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il nome di accesso e il nome utente per il processo utente corrente.  
  
```  
SELECT SESSION_ID() AS ID, @@SPID AS 'Control ID', SYSTEM_USER AS 'Login Name', USER AS 'User Name';  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di configurazione](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  

