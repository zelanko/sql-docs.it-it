---
title: Eseguire la migrazione in un database parzialmente indipendente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e535935da5c99668e39ab4f84eb98ccd5bab064
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528683"
---
# <a name="migrate-to-a-partially-contained-database"></a>Migrate to a Partially Contained Database
  In questo argomento viene descritto come prepararsi al passaggio al modello del database parzialmente indipendente, quindi viene illustrata la procedura di migrazione.  
  
 **Contenuto dell'argomento:**  
  
-   [Preparazione della migrazione di un database](#prepare)  
  
-   [Abilitazione di database indipendenti](#enable)  
  
-   [Conversione di un database a parzialmente indipendente](#convert)  
  
-   [Migrazione di utenti a utenti di database indipendenti](#users)  
  
##  <a name="prepare"></a> Preparazione della migrazione di un database  
 Quando si considera la migrazione di un database al modello di database parzialmente indipendente, esaminare gli elementi seguenti.  
  
-   È necessario comprendere il modello del database parzialmente indipendente. Per altre informazioni, vedere [Database indipendenti](contained-databases.md).  
  
-   È necessario comprendere rischi specifici dei database parzialmente indipendenti. Per altre informazioni, vedere [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md).  
  
-   Nei database indipendenti non è supportato l'utilizzo di funzionalità di replica, di rilevamento modifiche o Change Data Capture. Verificare che nel database non vengano utilizzate queste funzionalità.  
  
-   Esaminare l'elenco di funzionalità del database che vengono modificate per i database parzialmente indipendenti. Per altre informazioni, vedere [Funzionalità modificate &#40;database indipendente&#41;](modified-features-contained-database.md).  
  
-   Eseguire una query su [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql) per trovare oggetti o funzionalità indipendenti nel database. Per altre informazioni, vedere  
  
-   Controllare l'XEvent **database_uncontained_usage** per vedere quando vengono usate le funzionalità indipendenti.  
  
##  <a name="enable"></a> Abilitazione di database indipendenti  
 Prima di poter creare database indipendenti, è necessario abilitarli nell'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>Abilitazione di database indipendenti tramite Transact-SQL  
 Nell'esempio seguente vengono abilitati database indipendenti nell'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>Abilitazione di database indipendenti tramite Management Studio  
 Nell'esempio seguente vengono abilitati database indipendenti nell'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse sul nome del server e quindi scegliere **Proprietà**.  
  
2.  Nella sezione **Indipendenza** della pagina **Avanzate** impostare l'opzione **Abilita database indipendenti** su **True**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> Conversione di un database a parzialmente indipendente  
 Un database viene convertito in un database indipendente modificando l'opzione **CONTAINMENT** .  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>Conversione di un database in parzialmente indipendente tramite Transact-SQL  
 Nell'esempio seguente un database denominato `Accounting` viene convertito in un database parzialmente indipendente.  
  
```sql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>Conversione di un database in parzialmente indipendente tramite Management Studio  
 Nell'esempio seguente un database viene convertito in un database parzialmente indipendente.  
  
1.  In Esplora oggetti espandere **Database**, fare clic con il pulsante destro del mouse sul database da convertire, quindi scegliere **Proprietà**.  
  
2.  Nella pagina **Opzioni** impostare l'opzione **Tipo di indipendenza** su **Parziale**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="users"></a> Migrazione di utenti a utenti di database indipendenti  
 Nell'esempio seguente viene eseguita la migrazione di tutti gli utenti basati sugli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a utenti del database indipendente con password. Nell'esempio sono inclusi account di accesso non abilitati. L'esempio deve essere eseguito nel database indipendente.  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Database indipendenti](contained-databases.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql)   
 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql)  
  
  
