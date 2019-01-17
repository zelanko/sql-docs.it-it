---
title: SUSER_SID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d4a3d885eb4f0d40d95f937ba252625e9e07de5
ms.sourcegitcommit: 467b2c708651a3a2be2c45e36d0006a5bbe87b79
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/02/2019
ms.locfileid: "53979887"
---
# <a name="susersid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce l'ID di sicurezza (SID) per il nome dell'account di accesso specificato.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>Argomenti  
 **'** *login* **'**  
**Si applica a**: da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Nome dell'account di accesso dell'utente. *login* è di tipo **sysname**. Il parametro facoltativo *login* può essere un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure un utente o un gruppo di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Se *login* viene omesso, vengono restituite informazioni sul contesto di sicurezza corrente. Se nel parametro è inclusa la parola NULL, verrà restituito NULL.  
  
 *Param2*  
**Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Specifica se il nome di accesso viene convalidato. *Param2* è di tipo **int** ed è facoltativo. Se *Param2* è 0, il nome di account di accesso non è convalidato. Se per *Param2* non è specificato 0, il nome di accesso di Windows viene considerato come identico al nome di account di accesso archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="return-types"></a>Tipi restituiti  
 **varbinary(85)**  
  
## <a name="remarks"></a>Remarks  
 La funzione SUSER_SID può essere utilizzata come vincolo DEFAULT nell'istruzione ALTER TABLE o CREATE TABLE. È possibile utilizzare SUSER_SID in un elenco di selezione, in una clausola WHERE e in tutti i casi in cui è consentita un'espressione. SUSER_SID deve essere sempre seguita dalle parentesi, anche in assenza di parametri.  
  
 Se viene richiamata senza alcun argomento, la funzione SUSER_SID restituisce il SID del contesto di sicurezza corrente. Se richiamata senza alcun argomento all'interno di un batch per il quale il contesto è stato cambiato tramite EXECUTE AS, la funzione SUSER_SID restituisce il SID del contesto rappresentato. Se chiamata da un contesto rappresentato, SUSER_SID(ORIGINAL_LOGIN()) restituisce il SID del contesto originale.  
  
 Se le regole di confronto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quelle di Windows sono diverse, è possibile che SUSER_SID abbia esito negativo, qualora in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows l'account di accesso venga archiviato in un diverso formato. Se ad esempio l'account di accesso del computer Windows TestComputer è User e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'account di accesso è archiviato come TESTCOMPUTER\User, è possibile che il nome di account di accesso non venga risolto correttamente durante la ricerca dell'account di accesso TestComputer\User. Per ignorare questa convalida del nome account di accesso, usare *Param2*. L'assegnazione di regole di confronto diverse spesso determina l'errore 15401 di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-susersid"></a>A. Utilizzo della funzione SUSER_SID  
 Nell'esempio seguente viene restituito l'ID di sicurezza (SID) per il contesto di sicurezza corrente.  
  
```  
SELECT SUSER_SID();  
```  
  
### <a name="b-using-susersid-with-a-specific-login"></a>b. Utilizzo di SUSER_SID con un account di accesso specifico  
 Nell'esempio seguente viene restituito l'ID di sicurezza (SID) per l'account di accesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `sa`.  
  
**Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-susersid-with-a-windows-user-name"></a>C. Utilizzo della funzione SUSER_SID con un nome utente di Windows  
 Nell'esempio seguente viene restituito l'ID di sicurezza (SID) per l'utente di Windows `London\Workstation1`.  
  
**Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-susersid-as-a-default-constraint"></a>D. Utilizzo della funzione SUSER_SID come vincolo DEFAULT  
 Nell'esempio seguente la funzione `SUSER_SID` viene utilizzata come vincolo `DEFAULT` in un'istruzione `CREATE TABLE`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. Confronto tra il nome di account di accesso di Windows e il nome di account di accesso archiviato in SQL Server  
 Nell'esempio seguente viene illustrato come usare *Param2* per ottenere il SID da Windows e usarlo come input per la funzione `SUSER_SNAME`. In questo esempio viene fornito l'account di accesso nel formato archiviato in Windows (`TestComputer\User`) e viene restituito l'account di accesso nel formato nel quale è archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (`TESTCOMPUTER\User`).  
  
**Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ORIGINAL_LOGIN &#40;Transact-SQL&#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [Funzioni di sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
