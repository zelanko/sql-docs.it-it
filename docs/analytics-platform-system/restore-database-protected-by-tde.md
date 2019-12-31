---
title: Ripristinare un database protetto da TDE
description: Usare la procedura seguente per ripristinare un database crittografato con Transparent Data Encryption in Analytics Platform System Parallel data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 53707c62e018b9923f2bb923a4df46f6917d2902
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400443"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Ripristinare un database protetto da Transparent Data Encryption in parallelo data warehouse
Utilizzare la procedura seguente per ripristinare un database crittografato tramite Transparent Data Encryption.  
  
Nell'esempio [Using Transparent Data Encryption](transparent-data-encryption.md#using-tde) è presente codice per abilitare Transparent Data Encryption nel `AdventureWorksPDW2012` database. Il codice seguente continua l'esempio creando un backup del database nell'appliance del sistema di piattaforma analitico originale (APS), quindi ripristinando il certificato e il database in un altro dispositivo.  
  
Il primo passaggio consiste nel creare un backup del database di origine.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Preparare la nuova SQL Server PDW per Transparent Data Encryption creando una chiave master, abilitando la crittografia e creando una credenziale di rete.  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
Gli ultimi due passaggi ricreano il certificato usando i backup del SQL Server PDW originale. Utilizzare la password utilizzata durante la creazione del backup del certificato.  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>Vedere anche  
[BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[Creazione della chiave](../t-sql/statements/create-master-key-transact-sql.md) 
master[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREA CERTIFICATO](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
