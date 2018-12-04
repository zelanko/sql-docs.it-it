---
title: ALTER USER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_USER_TSQL
- ALTER USER
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database users
- ALTER USER statement
- renaming databases
- schemas [SQL Server], default
- database user names [SQL Server]
- names [SQL Server], database users
- default schemas
- modifying default schemas
ms.assetid: 344fc6ce-a008-47c8-a02e-47fae66cc590
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2cd03ba4b9b0363ef1d8ebe9c3ff0721fc08e3f9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542270"
---
# <a name="alter-user-transact-sql"></a>ALTER USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Rinomina un utente del database oppure ne modifica lo schema predefinito.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | DEFAULT_LANGUAGE = { NONE | <lcid> | <language name> | <language alias> }  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]  
```  
  
```  
-- Syntax for Azure SQL Database  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = schemaName  
    | LOGIN = loginName  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
[;]  
  
-- Azure SQL Database Update Syntax  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
[;]  
  
<set_item> ::=   
      NAME = newUserName   
    | DEFAULT_SCHEMA = { schemaName | NULL }  
    | LOGIN = loginName  
    | PASSWORD = 'password' [ OLD_PASSWORD = 'oldpassword' ]  
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ]   
  
-- SQL Database syntax when connected to a federation member  
ALTER USER userName  
     WITH <set_item> [ ,... n ]   
[;]  
  
<set_item> ::=   
     NAME = newUserName  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER USER userName    
     WITH <set_item> [ ,...n ]  
  
<set_item> ::=   
     NAME =newUserName   
     | LOGIN =loginName  
     | DEFAULT_SCHEMA = schema_name  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *userName*  
 Specifica il nome con cui viene identificato l'utente all'interno del database.  
  
 LOGIN **=**_loginName_  
 Modifica il mapping di un utente associandolo a un altro account di accesso, modificando l'ID di sicurezza (SID) dell'utente in modo che corrisponda all'ID di sicurezza dell'account di accesso.  
  
 Se l'istruzione ALTER USER è l'unica istruzione in un batch SQL, il database SQL di Microsoft Azure supporta la clausola WITH LOGIN. Se l'istruzione ALTER USER non è l'unica istruzione in un batch SQL o viene eseguita in SQL dinamico, la clausola WITH LOGIN non è supportata.  
  
 NAME **=**_newUserName_  
 Specifica il nuovo nome dell'utente. *newUserName* non deve essere già presente nel database corrente.  
  
 DEFAULT_SCHEMA **=** { *schemaName* | NULL }  
 Specifica il primo schema nel quale il server eseguirà una ricerca durante la risoluzione dei nomi di oggetti per l'utente. L'impostazione dello schema predefinito su NULL comporta la rimozione di uno schema predefinito da un gruppo di Windows.   Non è possibile usare NULL con un utente di Windows.  
  
 PASSWORD **=** '*password*'  
 **Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Specifica la password per l'utente che viene modificato. Per le password viene fatta distinzione tra maiuscole e minuscole.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo per gli utenti contenuti. Vedere [Database indipendenti](../../relational-databases/databases/contained-databases.md) e [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md) per altre informazioni.  
  
 OLD_PASSWORD **=**_'oldpassword'_  
 **Si applica a**: da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Password dell'utente corrente che verrà sostituita da '*password*'. Per le password viene fatta distinzione tra maiuscole e minuscole. *OLD_PASSWORD* è necessaria per modificare una password, a meno che non si disponga dell'autorizzazione **ALTER ANY USER**. Si richiede *OLD_PASSWORD* per impedire agli utenti con autorizzazione **IMPERSONATION** di modificare la password.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo per gli utenti contenuti.  
  
 DEFAULT_LANGUAGE **=**_{ NONE | \<lcid> | \<language name> | \<language alias> }_  
 **Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Specifica una lingua predefinita da assegnare all'utente. Se questa opzione è impostata su NONE, la lingua predefinita viene impostata sulla lingua predefinita corrente del database. Se la lingua predefinita del database viene modificata in seguito, la lingua predefinita dell'utente rimarrà invariata. *DEFAULT_LANGUAGE* può essere l'ID locale (lcid), il nome della lingua o l'alias della lingua.  
  
> [!NOTE]  
>  È possibile specificare questa opzione solo in un database indipendente e solo per utenti contenuti.  
  
 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | **OFF** ] ]  
 **Si applica a**: da [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] fino a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Elimina i controlli sui metadati di crittografia nel server nelle operazioni di copia bulk. Ciò consente all'utente di eseguire la copia bulk dei dati crittografati fra tabelle o database senza decrittografare i dati. Il valore predefinito è OFF.  
  
> [!WARNING]  
>  L'uso improprio di questa opzione può causare il danneggiamento dei dati. Per altre informazioni, vedere [Migrare dati sensibili protetti da Always Encrypted](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).  
  
## <a name="remarks"></a>Remarks  
 Lo schema predefinito sarà il primo schema in cui verrà eseguita la ricerca nel server durante la risoluzione dei nomi di oggetti per l'utente del database. Se non specificato diversamente, lo schema predefinito sarà il proprietario degli oggetti creati dall'utente del database.  
  
 Se l'utente dispone di uno schema predefinito, verrà utilizzato tale schema. Se l'utente non dispone di uno schema predefinito, ma è un membro di un gruppo che dispone di uno schema predefinito, verrà utilizzato lo schema predefinito del gruppo. Se l'utente non dispone di uno schema predefinito ed è un membro di più gruppi, lo schema predefinito per l'utente sarà quello del gruppo di Windows con principal_id inferiore e uno schema predefinito impostato in modo esplicito. Se non possono essere determinati schemi predefiniti per un utente, viene usato lo schema **dbo**.  
  
 È possibile impostare DEFAULT_SCHEMA su uno schema non attualmente presente nel database. È pertanto possibile assegnare uno schema predefinito tramite DEFAULT_SCHEMA a un utente prima della creazione dello schema.  
  
 Non è possibile specificare DEFAULT_SCHEMA per un utente di cui è stato eseguito il mapping a un certificato o a una chiave asimmetrica.  
  
> [!IMPORTANT]  
>  Il valore di DEFAULT_SCHEMA viene ignorato se l'utente è un membro del ruolo predefinito del server **sysadmin**. Tutti i membri del ruolo predefinito del server **sysadmin** dispongono di uno schema predefinito di `dbo`.  
  
 È possibile modificare il nome di un utente sul quale viene eseguito il mapping a un account di accesso o a un gruppo di Windows solo se il SID del nuovo nome utente corrisponde al SID registrato nel database. Questa verifica consente di impedire lo spoofing degli account di accesso di Windows nel database.  
  
 La clausola WITH LOGIN consente di modificare il mapping di un utente associandolo a un account di accesso diverso. Tramite questa clausola non è possibile modificare il mapping di utenti senza un account accesso, utenti sui quali viene eseguito il mapping a un certificato o utenti sui quali viene eseguito il mapping a una chiave asimmetrica. È possibile modificare il mapping solo di utenti di SQL e di utenti (o gruppi) di Windows. Non è possibile usare la clausola WITH LOGIN per modificare il tipo di utente, ad esempio modificando un account di Windows in un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se vengono soddisfatte le seguenti condizioni, il nome dell'utente viene automaticamente modificando nel nome dell'account di accesso.  
  
-   L'utente è un utente di Windows.  
  
-   Il nome è un nome di Windows (contiene una barra rovesciata).  
  
-   Non è stato specificato alcun nome.  
  
-   Il nome corrente è diverso dal nome dell'account di accesso.  
  
 In caso contrario, l'utente non verrà rinominato, a meno che il chiamante non richiami anche la clausola NAME.  
  
Il nome di un utente di cui è stato eseguito il mapping a un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un certificato o una chiave asimmetrica non può contenere il carattere barra rovesciata (\\).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="security"></a>Security  
  
> [!NOTE]  
>  Un utente con autorizzazione **ALTER ANY USER** può modificare lo schema predefinito di qualsiasi utente. È possibile che un utente con uno schema modificato selezioni involontariamente i dati dalla tabella errata o esegua codice dallo schema errato.  
  
### <a name="permissions"></a>Permissions  
 Per modificare il nome di un utente, è necessaria l'autorizzazione **ALTER ANY USER**.  
  
 Per modificare l'account di accesso di destinazione di un utente, è necessaria l'autorizzazione **CONTROL** per il database.  
  
 Per modificare il nome di un utente con autorizzazione **CONTROL** per il database, è necessaria l'autorizzazione **CONTROL** per il database.  
  
 Per modificare la lingua o lo schema predefinito, è necessaria l'autorizzazione **ALTER** per l'utente. Gli utenti possono modificare il proprio schema predefinito o la lingua.  
  
## <a name="examples"></a>Esempi  

Tutti gli esempi vengono eseguiti in un database utente.  

### <a name="a-changing-the-name-of-a-database-user"></a>A. Modifica del nome di un utente del database  
 Nell'esempio seguente il nome dell'utente del database `Mary5` viene modificato in `Mary51`.  
  
```  
ALTER USER Mary5 WITH NAME = Mary51;  
GO  
```  
  
### <a name="b-changing-the-default-schema-of-a-user"></a>B. Modifica dello schema predefinito di un utente  
 Nell'esempio seguente lo schema predefinito dell'utente `Mary51` viene modificato in `Purchasing`.  
  
```  
ALTER USER Mary51 WITH DEFAULT_SCHEMA = Purchasing;  
GO  
```  
  
### <a name="c-changing-several-options-at-once"></a>C. Modifica contemporanea di diverse opzioni  
 Nell'esempio seguente vengono modificate diverse opzioni per un utente del database indipendente in un'istruzione.  
  
**Si applica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] tramite [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER USER Philip   
WITH  NAME = Philipe   
    , DEFAULT_SCHEMA = Development   
    , PASSWORD = 'W1r77TT98%ab@#' OLD_PASSWORD = 'New Devel0per'   
    , DEFAULT_LANGUAGE  = French ;  
GO  
```  
  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Database indipendenti](../../relational-databases/databases/contained-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)  
  
  


