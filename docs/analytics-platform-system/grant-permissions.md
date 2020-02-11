---
title: Concedere autorizzazioni T-SQL
description: Concedere le autorizzazioni T-SQL per le operazioni di database in parallelo data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401156"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Concedere autorizzazioni T-SQL per data warehouse parallele
Concedere le autorizzazioni T-SQL per le operazioni di database in parallelo data warehouse.

## <a name="grant-permissions-to-submit-database-queries"></a>Concedere le autorizzazioni per l'invio di query sul database
Questa sezione descrive come concedere le autorizzazioni ai ruoli del database e agli utenti per eseguire query sui dati nell'appliance SQL Server PDW.  
  
Le istruzioni utilizzate per concedere le autorizzazioni per eseguire query sui dati dipendono dall'ambito di accesso desiderato. Le istruzioni SQL seguenti creano un account di accesso denominato KimAbercrombie che può accedere al dispositivo, creare un utente di database denominato KimAbercrombie nel database **AdventureWorksPDW2012** , creare un ruolo del database denominato PDWQueryData, aggiungere il KimAbercrombie di utilizzo al ruolo PDWQueryData e quindi visualizzare le opzioni per concedere l'accesso alle query, a seconda che l'accesso venga concesso a livello di oggetto o di database.  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Concedere le autorizzazioni per l'uso della console di amministrazione
Questa sezione descrive come concedere autorizzazioni agli account di accesso di per usare la console di amministrazione.  
  
**Usare la console di amministrazione**  
  
Per usare la console di amministrazione, un account di accesso richiede l'autorizzazione di **visualizzazione** a livello di server. L'istruzione SQL seguente concede l'autorizzazione **View Server state** per l'account `KimAbercrombie` di accesso in modo che Kim possa usare la console di amministrazione per monitorare il dispositivo SQL Server PDW.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Elimina sessioni**  
  
Per concedere a un account di accesso l'autorizzazione per terminare le sessioni, concedere l'autorizzazione **ALTER ANY Connection** come indicato di seguito:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Concedere le autorizzazioni per caricare i dati
Questa sezione descrive come concedere le autorizzazioni ai ruoli del database e agli utenti del database per caricare i dati nel SQL Server PDWappliance.  
  
Lo script seguente mostra le autorizzazioni necessarie per ogni opzione di caricamento. È possibile modificarlo in base alle esigenze specifiche.  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Concedere le autorizzazioni per Copia dati dal dispositivo
Questa sezione descrive come concedere le autorizzazioni a un utente o a un ruolo del database per copiare i dati dall'appliance SQL Server PDW.  
  
Per spostare i dati in un altro percorso è necessaria l'autorizzazione **Select** per la tabella contenente i dati da spostare.  
  
Se la destinazione per i dati è un'altra SQL Server PDW, l'utente deve disporre dell'autorizzazione **Create Table** per la destinazione e dell'autorizzazione **ALTER schema** per lo schema che conterrà la tabella.  
  
## <a name="grant-permissions-to-manage-databases"></a>Concedere le autorizzazioni per la gestione dei database
Questa sezione descrive come concedere le autorizzazioni a un utente del database per gestire un database nel dispositivo SQL Server PDW.  
  
In alcune situazioni, un'azienda assegna un responsabile per un database. Il Manager controlla l'accesso al database di altri account di accesso, nonché i dati e gli oggetti del database. Per gestire tutti gli oggetti, i ruoli e gli utenti in un database, concedere all'utente l'autorizzazione **Control** per il database. L'istruzione seguente concede all'utente `KimAbercrombie`l'autorizzazione **Control** per il database **AdventureWorksPDW2012** .  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Per concedere a un utente l'autorizzazione a controllare tutti i database nel dispositivo, concedere l'autorizzazione **ALTER ANY database** nel database master.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Concedere le autorizzazioni per la gestione di account di accesso, utenti e ruoli del database
In questa sezione viene descritto come concedere autorizzazioni per la gestione di account di accesso, utenti di database e ruoli del database.  
  
### <a name="PermsAdminConsole"></a>Concedere le autorizzazioni per gestire gli account di accesso  
**Aggiunta o gestione di account di accesso**  
  
Nelle istruzioni SQL seguenti viene creato un account di accesso denominato KimAbercrombie in grado di creare nuovi account di accesso utilizzando l'istruzione [Create Login](../t-sql/statements/create-login-transact-sql.md) e modificare gli account di accesso esistenti utilizzando l'istruzione [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) .  
  
L'autorizzazione **ALTER ANY LOGIN** concede la possibilità di creare nuovi account di accesso ed eliminare esistente. Una volta creato un account di accesso, è possibile gestire l'account di accesso con l'autorizzazione **ALTER ANY LOGIN** o l'autorizzazione **ALTER** per tale account di accesso. Un account di accesso può modificare la password e il database predefinito per il proprio account di accesso.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Concedere le autorizzazioni per gestire le sessioni di accesso  
Per avere la possibilità di visualizzare tutte le sessioni sul server, è necessaria l'autorizzazione **View Server state** . La possibilità di terminare le sessioni di altri account di accesso richiede l'autorizzazione **ALTER ANY Connection** . Nell'esempio seguente viene usato `KimAbercrombie` l'account di accesso creato in precedenza.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Concedere l'autorizzazione per gestire gli utenti del database  
Per la creazione e l'eliminazione di utenti di database è necessaria l'autorizzazione **ALTER ANY USER** . Per la gestione degli utenti esistenti è necessaria l'autorizzazione **ALTER ANY USER** o l'autorizzazione **ALTER** per tale utente. Nell'esempio seguente viene usato `KimAbercrombie` l'account di accesso creato in precedenza.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Concedere a autorizzazione per gestire i ruoli del database  
Per creare ed eliminare ruoli del database definiti dall'utente è necessaria l'autorizzazione **ALTER ANY ROLE** . Nell'esempio seguente viene usato `KimAbercrombie` l'account di accesso di e viene creato in precedenza.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Grafici delle autorizzazioni di accesso, utente e ruolo  
I grafici seguenti possono generare confusione, ma mostrano come le autorizzazioni per le leve più elevate, ad esempio il controllo, includano autorizzazioni più granulari che possono essere concesse separatamente, ad esempio ALTER. È consigliabile concedere sempre il minor numero di autorizzazioni per consentire a un utente di completare le attività necessarie. A tale scopo, concedere autorizzazioni più specifiche, anziché le autorizzazioni di primo livello.  
  
**Autorizzazioni di accesso:**  
  
![Autorizzazioni di accesso per la sicurezza APS](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Autorizzazioni utente:**  
  
![Autorizzazioni utente per la sicurezza APS](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Autorizzazioni per i ruoli:**  
  
![Autorizzazioni dei ruoli di sicurezza APS](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Concedere le autorizzazioni per il monitoraggio dell'appliance
Il dispositivo SQL Server PDW può essere monitorato tramite la console di amministrazione o SQL Server PDW viste di sistema. Gli account di accesso richiedono l'autorizzazione di **visualizzazione** a livello di server per il monitoraggio dell'appliance. Per gli account di accesso è necessaria l'autorizzazione **ALTER ANY Connection** per terminare le connessioni tramite la console di amministrazione o il comando **Kill** . Per informazioni sulle autorizzazioni necessarie per usare la console di amministrazione, vedere [concedere le autorizzazioni per usare la console di amministrazione &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="PermsAdminConsole"></a>Concedere l'autorizzazione per monitorare l'appliance usando le viste di sistema  
Nelle istruzioni SQL seguenti viene creato un account `monitor_login` di accesso denominato e viene concessa l'autorizzazione `monitor_login` **View Server state** per l'account di accesso.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Concedere l'autorizzazione per il monitoraggio dell'appliance usando le viste di sistema e per terminare le connessioni  
Nelle istruzioni SQL seguenti viene creato un account `monitor_and_terminate_login` di accesso denominato e vengono concesse le autorizzazioni **View Server state** e **ALTER ANY Connection** all' `monitor_and_terminate_login` account di accesso.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Per creare account di accesso amministratore, vedere ruoli predefiniti del [Server](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Vedere anche
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[CREA UTENTE](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[Caricamento](load-overview.md)  
