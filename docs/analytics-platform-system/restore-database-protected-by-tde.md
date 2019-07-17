---
title: Ripristinare un database protetto con TDE - Parallel Data Warehouse | Microsoft Docs
description: Usare la procedura seguente per ripristinare un database che viene crittografato con TDE in Analitica Platform System Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7c2f676f75c5a8c79bfc2f2417ff30c9806e3c80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960160"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Ripristinare un database protetto con TDE in Parallel Data Warehouse
Usare la procedura seguente per ripristinare un database che verrà crittografato usando crittografia trasparente dei dati.  
  
Il [tramite Transparent Data Encryption](transparent-data-encryption.md#using-tde) esempio include il codice per abilitare TDE nel `AdventureWorksPDW2012` database. Il codice seguente continua tale esempio, creando un backup del database nell'appliance Analitica piattaforma di strumenti analitici originale e quindi ripristinare il certificato e il database in un dispositivo diverso.  
  
Il primo passaggio consiste nel creare un backup del database di origine.  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
Preparare il nuovo SQL Server PDW per TDE creando una chiave master, abilitazione della crittografia e creazione di una credenziale di rete.  
  
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
  
Gli ultimi due passaggi ricreare il certificato usando i backup dalla versione originale di SQL Server PDW. Usare la password usati durante la creazione del backup del certificato.  
  
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
[BACKUP DEL DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)  
[CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md) 
[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREARE CERTIFICATI](../t-sql/statements/create-certificate-transact-sql.md)  
[RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)
  
