---
title: ALTER MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER MASTER KEY
- ALTER_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REGENERATE phrase
- ALTER MASTER KEY statement
- decryption [SQL Server], Database Master Key
- FORCE option
- encryption [SQL Server], Database Master Key
- database master key [SQL Server], modifying
- cryptography [SQL Server], Database Master Key
- modifying Database Master Key
- service master key [SQL Server], modifying
- DROP ENCRYPTION BY SERVICE MASTER KEY phrase
ms.assetid: 8ac501c3-4280-4d5b-b58a-1524fa715b50
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7190892a06eb7684b549e38d6cb417b8bddb6ff0
ms.sourcegitcommit: 9c99f992abd5f1c174b3d1e978774dffb99ff218
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/17/2019
ms.locfileid: "54361481"
---
# <a name="alter-master-key-transact-sql"></a>ALTER MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Modifica le proprietà di una chiave master del database.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
-- Syntax for SQL Server  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Database
-- Note: DROP ENCRYPTION BY SERVICE MASTER KEY is not supported on Azure SQL Database.
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD = 'password'  
  
<encryption_option> ::=  
    ADD ENCRYPTION BY { SERVICE MASTER KEY | PASSWORD = 'password' }  
    |   
    DROP ENCRYPTION BY { PASSWORD = 'password' }  
```  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
ALTER MASTER KEY <alter_option>  
  
<alter_option> ::=  
    <regenerate_option> | <encryption_option>  
  
<regenerate_option> ::=  
    [ FORCE ] REGENERATE WITH ENCRYPTION BY PASSWORD ='password'<encryption_option> ::=  
    ADD ENCRYPTION BY SERVICE MASTER KEY   
    |   
    DROP ENCRYPTION BY SERVICE MASTER KEY  
```  
  
## <a name="arguments"></a>Argomenti  
 PASSWORD ='*password*'  
 Specifica una password con la quale crittografare o decrittografare la chiave master del database. *password* deve soddisfare i requisiti per i criteri password di Windows del computer che sta eseguendo l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Remarks  
 L'opzione REGENERATE rigenera la chiave master del database e tutte le chiavi protette dalla chiave master. Le chiavi vengono prima decrittografate con la chiave master precedente e quindi crittografate con la nuova chiave master. Si tratta di un'operazione che utilizza molte risorse e pertanto dovrebbe essere pianificata in periodi di carico ridotto, a meno che la chiave master non sia stata compromessa.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] usa l'algoritmo di crittografia AES per proteggere la chiave master del servizio (SMK) e la chiave master del database (DMK). AES è un algoritmo di crittografia più recente rispetto a 3DES utilizzato nelle versioni precedenti. Dopo aver aggiornato un'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] le chiavi SMK e DMK devono essere rigenerate per aggiornare le chiavi master ad AES. Per altre informazioni sulla rigenerazione della SMK, vedere [ALTER SERVICE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-master-key-transact-sql.md).  
  
 Quando si utilizza l'opzione FORCE, la rigenerazione delle chiavi continuerà anche se la chiave master non è disponibile o il server non è in grado di decrittografare tutte le chiavi private crittografate. Se non è possibile aprire la chiave master, usare l'istruzione [RESTORE MASTER KEY](../../t-sql/statements/restore-master-key-transact-sql.md) per ripristinare la chiave master da un backup. Utilizzare l'opzione FORCE solo se la chiave master è irrecuperabile o se la decrittografia ha esito negativo. Le informazioni crittografate esclusivamente da una chiave irrecuperabile andranno perdute.  
  
 L'opzione DROP ENCRYPTION BY SERVICE MASTER KEY rimuove l'impostazione per la crittografia della chiave master del database tramite la chiave master del servizio.  
  
 Con ADD ENCRYPTION BY SERVICE MASTER KEY una copia della chiave master viene crittografata utilizzando la chiave master del servizio e archiviata sia nel database corrente che nel database master.  
  
## <a name="permissions"></a>Permissions  
 È richiesta l'autorizzazione CONTROL per il database. Se la chiave master del database è stata crittografata con una password è inoltre necessario conoscere tale password.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene creta una nuova chiave master del database per `AdventureWorks` e vengono di nuovo crittografate le chiavi figlio corrispondenti nella gerarchia di crittografia.  
  
```  
USE AdventureWorks2012;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Nell'esempio seguente viene creta una nuova chiave master del database per `AdventureWorksPDW2012` e vengono di nuovo crittografate le chiavi figlio corrispondenti nella gerarchia di crittografia.  
  
```  
USE master;  
ALTER MASTER KEY REGENERATE WITH ENCRYPTION BY PASSWORD = 'dsjdkflJ435907NnmM#sX003';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [DROP MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-master-key-transact-sql.md)   
 [Gerarchia di crittografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

