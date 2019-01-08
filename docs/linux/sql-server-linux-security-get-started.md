---
title: Introduzione alla sicurezza di SQL Server in Linux | Microsoft Docs
description: Questo articolo descrive le azioni di sicurezza standard.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: sql-linux
ms.openlocfilehash: c3d3c4a6ac5d5d49e880fc2af1546bdcf9a73779
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211740"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Procedura dettagliata per la funzionalità di sicurezza di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Se sei un utente di Linux che è una novità di SQL Server, le attività seguenti illustrano alcune delle attività di sicurezza. Questi non sono specifiche di Linux o univoco, ma è utile per dare un'idea delle aree per analizzare ulteriormente il problema. In ogni esempio viene fornito un collegamento alla documentazione approfondita per quell'area.

> [!NOTE]
>  Gli esempi seguenti usano il **AdventureWorks2014** database di esempio. Per istruzioni su come ottenere e installare il database di esempio, vedere [ripristinare un database di SQL Server da Windows a Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Creare un account di accesso e un utente del database 

Concedere ad altri utenti l'accesso a SQL Server mediante la creazione di un account di accesso nel database master usando il [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) istruzione. Ad esempio:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  Usare sempre una password complessa al posto di un asterisco nel comando precedente.

Gli account di accesso possono connettersi a SQL Server e dispongono di accesso (con autorizzazioni limitate) al database master. Per connettersi a un database utente, un account di accesso richiede un'identità a livello di database, denominato un utente del database corrispondente. Gli utenti sono specifici per ogni database e devono essere creati separatamente in ogni database per concedere loro l'accesso. Nell'esempio seguente consente di passare al database AdventureWorks2014 e quindi Usa il [CREATE USER](../t-sql/statements/create-user-transact-sql.md) istruzione per creare un utente denominato Larry associato con l'account di accesso denominato Larry. Se l'account di accesso e l'utente sono correlate (mapping reciproco), sono oggetti diversi. L'account di accesso è un'entità a livello di server. L'utente è un'entità a livello di database.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Un account di amministratore di SQL Server può connettersi a qualsiasi database e possa creare più account di accesso e utenti in qualsiasi database.  
- Quando un utente crea un database diventano il proprietario del database, in grado di connettersi a tale database. I proprietari di database possono creare altri utenti.

In un secondo momento è possibile autorizzare altri account di accesso per creare un altro account di accesso da concedere loro il `ALTER ANY LOGIN` l'autorizzazione. All'interno di un database, è possibile autorizzare altri utenti per creare altre utenti concedendo il `ALTER ANY USER` l'autorizzazione. Ad esempio:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

L'account di accesso Larry possono ora creare ulteriori account di accesso e l'utente Jerry possono creare altri utenti.


## <a name="granting-access-with-least-privileges"></a>Concessione dell'accesso con privilegi minimi

I primi utenti di connettersi a un database utente sarà l'amministratore e gli account proprietario del database. Tuttavia questi utenti hanno tutte le autorizzazioni disponibili per il database. Si tratta di autorizzazioni maggiori rispetto a quasi tutti gli utenti devono avere. 

Quando sta iniziando, è possibile assegnare alcune categorie generali di autorizzazioni tramite l'oggetto incorporato *ruoli predefiniti del database*. Ad esempio, il `db_datareader` può leggere tutte le tabelle nel database del ruolo predefinito del database, ma senza apportare alcuna modifica. Concedere l'appartenenza a un ruolo predefinito del database usando il [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) istruzione. Nell'esempio seguente l'utente di aggiungere `Jerry` per il `db_datareader` ruolo predefinito del database.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Per un elenco dei ruoli predefiniti del database, vedere [ruoli a livello di Database](../relational-databases/security/authentication-access/database-level-roles.md).

In un secondo momento, quando si è pronti per configurare l'accesso più preciso ai dati (altamente consigliati), creare ruoli database definiti dall'utente usando [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) istruzione. Quindi assegnare specifiche autorizzazioni granulari all'utente i ruoli personalizzati.

Ad esempio, le istruzioni che seguono creano un ruolo del database denominato `Sales`, concede il `Sales` raggruppare la possibilità di visualizzare, aggiornare ed eliminare righe dal `Orders` tabella e quindi aggiunge l'utente `Jerry` per il `Sales` ruolo.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
CREARE SalesFilter dei criteri di sicurezza   
Aggiungi filtro PREDICATO Security.fn_securitypredicate(SalesPersonID)    
  IN Sales. SalesOrderHeader,   
AGGIUNGERE Security.fn_securitypredicate(SalesPersonID) PREDICATO di blocco    
  IN Sales. SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
Selezionare * da Sales. SalesOrderHeader;    
RIPRISTINARE; 
 
EXECUTE AS USER = 'Manager';   
Selezionare * da Sales. SalesOrderHeader;   
RIPRISTINARE;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SECURITY POLICY SalesFilter   
CON (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USARE AdventureWorks2014; ALTER passare tabella Person.EmailAddress     EmailAddress colonna ALTER    
Aggiungere MASKED WITH (funzione = ' email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
CREARE TestUser utente senza account di accesso;   
GRANT selezionare ON Person.EmailAddress a TestUser;    
 
EXECUTE AS USER = "TestUser";   
Selezionare EmailAddressID, indirizzo di posta elettronica da Person.EmailAddress;       
RIPRISTINARE;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = ' * * * ';  
GO  

CREARE MyServerCert certificato con soggetto = 'My Database certificato della chiave DEK';  
GO  

USARE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
CON L'ALGORITMO = AES_256  
ENCRYPTION BY SERVER certificato MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON.   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
Utilizzare master;   ANDARE   Crea certificato BackupEncryptCert   con l'oggetto = 'Backup del Database';   Passare il DATABASE di BACKUP [AdventureWorks2014]   sul disco = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
con  
  COMPRESSIONE,  
  ENCRYPTION   
   (  
   ALGORITMO = AES_256,  
   CERTIFICATO SERVER = BackupEncryptCert  
   ),  
  STATISTICHE = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
