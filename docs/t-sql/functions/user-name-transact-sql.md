---
title: USER_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USER_NAME
- USER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- IDs [SQL Server], databases
- USER_NAME function
- users [SQL Server], database username
- names [SQL Server], database users
- identification numbers [SQL Server], databases
- database usernames [SQL Server]
ms.assetid: ab32d644-4228-449a-9ef0-5a975c305775
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21c085bd942b368259444698cabf5dfa44d0fbe1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79526786"
---
# <a name="user_name-transact-sql"></a>USER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Restituisce un nome di un utente del database corrispondente al numero di identificazione specificato.  
  
 ![Icona di collegamento a un articolo](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un articolo") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
USER_NAME ( [ id ] )  
```  
  
## <a name="arguments"></a>Argomenti  
 *id*  
 Numero di identificazione associato a un utente del database. *id* è di tipo **int**. È necessario utilizzare le parentesi.  
  
## <a name="return-types"></a>Tipi restituiti  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Osservazioni  
 Se *id* viene omesso, viene usato l'utente corrente nel contesto corrente. Se nel parametro è inclusa la parola NULL, verrà restituito NULL. Se la funzione USER_NAME viene chiamata senza specificare *id* dopo un'istruzione EXECUTE AS, viene restituito il nome dell'utente rappresentato. Se un'entità di Windows accede al database in base all'appartenenza a un gruppo, USER_NAME restituisce il nome dell'entità di Windows anziché il gruppo.  
 
> [!NOTE]
> Sebbene la funzione USER_NAME sia supportata nel database SQL di Azure, l'uso di *Execute As* con USER_NAME non è supportato nel database SQL di Azure. 
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-user_name"></a>R. Utilizzo di USER_NAME  
 Nell'esempio seguente viene restituito il nome utente per l'ID utente `13`.  
  
```  
SELECT USER_NAME(13);  
GO  
```  
  
### <a name="b-using-user_name-without-an-id"></a>B. Utilizzo di USER_NAME senza un ID  
 Nell'esempio seguente viene restituito il nome dell'utente corrente senza specificare un ID.  
  
```  
SELECT USER_NAME();  
GO  
```  
  
 Set di risultati (per un utente membro del ruolo predefinito del server sysadmin):  
  
 ```
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="c-using-user_name-in-the-where-clause"></a>C. Utilizzo di USER_NAME nella clausola WHERE  
 Nell'esempio seguente viene restituita la riga di `sysusers` contenente un nome che corrisponde al risultato della funzione di sistema `USER_NAME` per il numero di identificazione utente `1`.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
name  
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="d-calling-user_name-during-impersonation-with-execute-as"></a>D. Chiamata della funzione USER_NAME durante la rappresentazione tramite EXECUTE AS  
 Nell'esempio seguente viene illustrato il comportamento della funzione `USER_NAME` durante la rappresentazione.  
  
```  
SELECT USER_NAME();  
GO  
EXECUTE AS USER = 'Zelig';  
GO  
SELECT USER_NAME();  
GO  
REVERT;  
GO  
SELECT USER_NAME();  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO  
Zelig  
DBO
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-user_name-without-an-id"></a>E. Utilizzo di USER_NAME senza un ID  
 Nell'esempio seguente viene restituito il nome dell'utente corrente senza specificare un ID.  
  
```  
SELECT USER_NAME();  
```  
  
 Ecco il set di risultati di un utente attualmente connesso.  
  
```  
------------------------------   
User7                              
```  
  
### <a name="f-using-user_name-in-the-where-clause"></a>F. Utilizzo di USER_NAME nella clausola WHERE  
 Nell'esempio seguente viene restituita la riga di `sysusers` contenente un nome che corrisponde al risultato della funzione di sistema `USER_NAME` per il numero di identificazione utente `1`.  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
name                             
------------------------------   
User7                              
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact-SQL&#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact-SQL&#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;Transact-SQL&#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [SYSTEM_USER &#40;Transact-SQL&#41;](../../t-sql/functions/system-user-transact-sql.md)  
  
