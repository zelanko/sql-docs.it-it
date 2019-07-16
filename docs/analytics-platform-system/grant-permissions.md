---
title: Autorizzazioni di T-SQL GRANT - Parallel Data Warehouse | Microsoft Docs
description: Autorizzazioni GRANT T-SQL per le operazioni di database in Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 15798edc4d6a9b1f00c8dd489dfed76a39e5f340
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960941"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Autorizzazioni di T-SQL GRANT per Parallel Data Warehouse
Autorizzazioni GRANT T-SQL per le operazioni di database in Parallel Data Warehouse.

## <a name="grant-permissions-to-submit-database-queries"></a>Concedere le autorizzazioni per inviare le query di Database
Questa sezione descrive come concedere autorizzazioni ai ruoli del database e agli utenti di eseguire query sui dati nell'appliance di SQL Server PDW.  
  
Le istruzioni utilizzate per concedere le autorizzazioni per eseguire query sui dati dipendono dall'ambito di accesso desiderato. Le istruzioni SQL seguenti creano un account di accesso denominato KimAbercrombie in grado di accedere all'appliance, creare un utente del database denominato KimAbercrombie nel **AdventureWorksPDW2012** del database, creare un ruolo del database denominato PDWQueryData aggiunge l'uso KimAbercrombie al ruolo PDWQueryData e quindi Mostra le opzioni per la concessione dell'accesso di query, basato sul fatto che l'accesso viene consentito all'oggetto o a livello di database.  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Concedere le autorizzazioni per usare la Console di amministrazione
Questa sezione descrive come concedere autorizzazioni agli account di accesso per usare la Console di amministrazione.  
  
**Usare la Console di amministrazione**  
  
Usare la Console di amministrazione di un account di accesso richiede il livello di server **VIEW SERVER STATE** l'autorizzazione. L'istruzione SQL seguente concede il **VIEW SERVER STATE** autorizzazione all'accesso `KimAbercrombie` Kim è possibile utilizzare la Console di amministrazione per monitorare l'appliance di SQL Server PDW.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Terminare le sessioni**  
  
Per concedere l'autorizzazione per terminare le sessioni di un account di accesso, concedere le **ALTER ANY CONNECTION** autorizzazione come indicato di seguito:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Concedere le autorizzazioni per caricare i dati
Questa sezione descrive come concedere autorizzazioni ai ruoli predefiniti del database e agli utenti di database per caricare i dati in PDWappliance il Server SQL.  
  
Lo script seguente con esattezza quali autorizzazioni sono necessarie per ogni opzione di caricamento. È possibile modificare questa opzione per soddisfare esigenze specifiche.  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Concedere le autorizzazioni per copiare i dati all'esterno dell'Appliance
In questa sezione viene descritto come concedere autorizzazioni a un utente o ruolo del database per copiare i dati fuori dal dispositivo di SQL Server PDW.  
  
Per spostare i dati in un'altra posizione, è necessario **seleziona** autorizzazione per la tabella che contiene i dati da spostare.  
  
Se la destinazione per i dati è un altro SQL Server PDW, l'utente deve disporre **CREATE TABLE** autorizzazione a livello di destinazione e **ALTER SCHEMA** autorizzazione per lo schema che conterrà la tabella.  
  
## <a name="grant-permissions-to-manage-databases"></a>Concedere le autorizzazioni per gestire i database
In questa sezione viene descritto come concedere autorizzazioni a un utente del database per gestire un database nell'appliance di SQL Server PDW.  
  
In alcune situazioni, una società assegna un gestore per un database. La gestione controlla l'accesso di altri account di accesso per il database, nonché i dati e oggetti nel database. Per gestire tutti gli oggetti, ruoli, e gli utenti in un database di concedono all'utente il **controllo** autorizzazione per il database. L'istruzione seguente concede il **controllo** l'autorizzazione per il **AdventureWorksPDW2012** database all'utente `KimAbercrombie`.  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Per concedere a un utente l'autorizzazione per controllare tutti i database nell'appliance, concedere le **ALTER ANY DATABASE** autorizzazione nel database master.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Concedere le autorizzazioni per gestire gli account di accesso, utenti e ruoli del Database
In questa sezione viene descritto come concedere le autorizzazioni per gestire gli account di accesso, gli utenti del database e i ruoli del database.  
  
### <a name="PermsAdminConsole"></a>Concedere le autorizzazioni per gestire gli account di accesso  
**Aggiungere o gestire gli account di accesso**  
  
Le istruzioni SQL seguenti creano un account di accesso denominato KimAbercrombie che è possibile creare nuovi account di accesso usando il [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) istruzione e modificare l'account di accesso esistenti tramite il [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) istruzione.  
  
Il **ALTER ANY LOGIN** autorizzazione concede la possibilità di creare nuovi account di accesso ed eliminare esistente. Una volta creato un account di accesso, l'account di accesso possono essere gestiti dagli account di accesso con il **ALTER ANY LOGIN** autorizzazione o il **ALTER** l'autorizzazione per tale account di accesso. Un account di accesso è possibile modificare il database predefinito e password per il proprio account di accesso.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Concedere le autorizzazioni per gestire sessioni di accesso  
Per avere la possibilità di visualizzare tutte le sessioni nel server, è necessario il **VIEW SERVER STATE** l'autorizzazione. Richiede la possibilità di terminare le sessioni di altri account di accesso di **ALTER ANY CONNECTION** l'autorizzazione. L'esempio seguente usa il `KimAbercrombie` account di accesso creato in precedenza.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Concedere l'autorizzazione per gestire gli utenti del Database  
Creazione ed eliminazione di utenti del database richiede la **ALTER ANY USER** l'autorizzazione. Richiede la gestione degli utenti esistenti di **ALTER ANY USER** autorizzazione o il **ALTER** dell'autorizzazione per tale utente. L'esempio seguente usa il `KimAbercrombie` account di accesso creato in precedenza.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Concessione dell'autorizzazione per accedere a gestire i ruoli di Database  
Creare ed eliminare i ruoli del database definito dall'utente richiede la **ALTER ANY ROLE** l'autorizzazione. L'esempio seguente usa il `KimAbercrombie` account di accesso e utilizzo creato in precedenza.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Account di accesso, utenti e i grafici di autorizzazione di ruolo  
I grafici seguenti possono generare confusione, ma devono essere visualizzate autorizzazioni levetta come superiori, ad esempio, includono le autorizzazioni più granulari che possono essere concesse separatamente (ad esempio ALTER). È consigliabile concedere sempre la quantità minima di autorizzazioni per un utente di completare le attività necessarie. A tale scopo, concedere le autorizzazioni più specifiche, anziché le autorizzazioni di livello superiore.  
  
**Autorizzazioni di accesso:**  
  
![Le autorizzazioni di accesso di sicurezza APS](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Autorizzazioni utente:**  
  
![Autorizzazioni utente di sicurezza APS](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Autorizzazioni del ruolo:**  
  
![Autorizzazioni ruolo di sicurezza APS](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Concedere le autorizzazioni per monitorare l'Appliance
L'appliance di SQL Server PDW può essere monitorato mediante la Console di amministrazione o SQL Server PDW viste di sistema. Gli account di accesso richiedono il livello di server **VIEW SERVER STATE** dell'autorizzazione per monitorare l'appliance. Gli account di accesso richiedono il **ALTER ANY CONNECTION** l'autorizzazione per terminare le connessioni utilizzando la Console di amministrazione o il **KILL** comando. Per informazioni sulle autorizzazioni necessarie per usare la Console di amministrazione, vedere [concedere autorizzazioni per usare la Console di amministrazione &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="PermsAdminConsole"></a>Concedere l'autorizzazione per monitorare l'Appliance usando le viste di sistema  
Le istruzioni SQL seguenti creano un account di accesso denominato `monitor_login` e concede il **VIEW SERVER STATE** l'autorizzazione per il `monitor_login` account di accesso.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Concedere l'autorizzazione per monitorare l'Appliance usando le viste di sistema e per terminare le connessioni  
Le istruzioni SQL seguenti creano un account di accesso denominato `monitor_and_terminate_login` e concede il **VIEW SERVER STATE** e **ALTER ANY CONNECTION** delle autorizzazioni per il `monitor_and_terminate_login` account di accesso.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Per creare gli account di accesso di amministratore, vedere [ruoli Server fissi](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Vedere anche
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[CREA UTENTE](../t-sql/statements/create-user-transact-sql.md)  
[CREA RUOLO](../t-sql/statements/create-role-transact-sql.md)  
[Load](load-overview.md)  
