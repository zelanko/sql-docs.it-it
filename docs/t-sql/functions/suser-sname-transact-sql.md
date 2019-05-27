---
title: SUSER_SNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 80defa93fb82a5a6b451acd00c8336a74a06ba34
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948192"
---
# <a name="susersname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce il nome dell'account di accesso associato a un ID di sicurezza (SID).  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>Argomenti  
 *server_user_sid*  
**Si applica a**: da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Numero identificativo di sicurezza facoltativo dell'account di accesso. *server_user_sid* è di tipo **varbinary(85)** . *server_user_sid* può essere l'ID di sicurezza (SID) di qualsiasi account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o di qualsiasi utente o gruppo di [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Se non si specifica *server_user_sid*, vengono restituite informazioni sull'utente corrente. Se nel parametro è inclusa la parola NULL, verrà restituito NULL.  
  
## <a name="return-types"></a>Tipi restituiti  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Remarks  
 La funzione SUSER_SNAME può essere utilizzata come vincolo DEFAULT nell'istruzione ALTER TABLE o CREATE TABLE. È possibile utilizzare SUSER_SNAME nell'elenco di selezione, nella clausola WHERE e in tutti i casi in cui è consentita un'espressione. SUSER_SNAME deve essere sempre seguita da una coppia di parentesi, anche se non si specifica alcun parametro.  
  
 Se chiamata senza argomenti, la funzione SUSER_SNAME restituisce il nome del contesto di sicurezza corrente. Se chiamata senza argomenti all'interno di un batch che ha cambiato contesto tramite EXECUTE AS, la funzione SUSER_SNAME restituisce il nome del contesto rappresentato. Se chiamata da un contesto rappresentato, ORIGINAL_LOGIN restituisce il nome del contesto originale.  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-remarks"></a>Osservazioni su [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
 SUSER_NAME restituisce sempre il nome dell'account di accesso per il contesto di sicurezza corrente.  
  
 L'istruzione SUSER_SNAME non supporta l'esecuzione con un contesto di sicurezza rappresentato tramite EXECUTE AS.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-susersname"></a>A. Utilizzo di SUSER_SNAME  
 Nell'esempio seguente viene restituito il nome dell'account di accesso per il contesto di sicurezza corrente.  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-susersname-with-a-windows-user-security-id"></a>B. Utilizzo della funzione SUSER_SNAME con l'ID di sicurezza di un utente di Windows  
 Nell'esempio seguente viene restituito il nome dell'account di accesso associato a un ID di sicurezza di Windows.  
  
**Si applica a**: da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-susersname-as-a-default-constraint"></a>C. Utilizzo della funzione SUSER_SNAME come vincolo DEFAULT  
 Nell'esempio seguente la funzione `SUSER_SNAME` viene utilizzata come vincolo `DEFAULT` in un'istruzione `CREATE TABLE`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-susersname-in-combination-with-execute-as"></a>D. Chiamata della funzione SUSER_SNAME in combinazione con EXECUTE AS  
 In questo esempio viene illustrato il funzionamento della funzione SUSER_SNAME quando viene chiamata da un contesto rappresentato.  
  
**Si applica a**: da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 Risultato:  
  
 ```
sa  
WanidaBenShoof  
sa
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-susersname"></a>E. Utilizzo di SUSER_SNAME  
 Nell'esempio seguente viene restituito il nome dell'account di accesso corrispondente all'ID di sicurezza `0x01`.  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. Restituzione dell'account di accesso corrente  
 L'esempio seguente restituisce il nome dell'account di accesso corrente.  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Entità &#40;motore di database&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

