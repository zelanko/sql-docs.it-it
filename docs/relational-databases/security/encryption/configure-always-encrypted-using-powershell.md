---
title: Configurare Always Encrypted tramite PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6ad4a50d8aeca225ae0d00574a62cc428593ebb2
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903010"
---
# <a name="configure-always-encrypted-using-powershell"></a>Configure Always Encrypted using PowerShell (Configurare Always Encrypted usando PowerShell)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Il modulo PowerShell SqlServer include i cmdlet per la configurazione di [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) nel database SQL di Azure e in SQL Server 2016.

I cmdlet di Always Encrypted nel modulo SqlServer usano chiavi o dati sensibili. È quindi importante eseguire i cmdlet in un computer protetto. Durante la gestione di Always Encrypted eseguire i cmdlet da un computer diverso da quello che ospita l'istanza di SQL Server.

Poiché l'obiettivo principale di Always Encrypted è garantire la sicurezza dei dati sensibili crittografati anche se il sistema di database viene compromesso, l'esecuzione di uno script di PowerShell che elabora chiavi o dati sensibili nel computer SQL Server può ridurre o annullare i vantaggi della funzionalità. Per altre indicazioni relative alla sicurezza, vedere [Considerazioni sulla sicurezza per la gestione delle chiavi](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management).

I collegamenti ai singoli articoli dei cmdlet sono presenti alla [fine di questa pagina](#aecmdletreference).

## <a name="prerequisites"></a>Prerequisites

Installare il [modulo SqlServer](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/sqlserver) in un computer protetto che NON sia il computer che ospita l'istanza di SQL Server. Il modulo può essere installato direttamente da PowerShell Gallery.  Per altri dettagli, vedere le istruzioni di [download](../../../ssms/download-sql-server-ps-module.md).


## <a name="importsqlservermodule"></a> Importazione del modulo SqlServer 

Per caricare il modulo SqlServer:

1.  Usare il cmdlet **Set-ExecutionPolicy** per impostare i criteri di esecuzione degli script appropriati.
2.  Usare il cmdlet **Import-Module** per importare il modulo SqlServer.

Questo esempio carica il modulo SqlServer.

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> Connessione a un database

Alcuni dei cmdlet Always Encrypted possono essere usati con dati o metadati del database e richiedono la connessione al database. Quando si configura Always Encrypted con il modulo SqlServer è consigliabile connettersi al database con i due metodi seguenti: 
1. Connettersi usando SQL Server PowerShell.
2. Connettersi usando SQL Server Management Objects (SMO).

### <a name="using-sql-server-powershell"></a>Utilizzo di SQL Server PowerShell

Questo metodo si applica solo a SQL Server e non è supportato nel database SQL di Azure.

Con SQL Server PowerShell è possibile spostarsi tra i percorsi usando alias di Windows PowerShell simili ai comandi normalmente usati per spostarsi tra i percorsi del file system. Dopo essere passati all'istanza di destinazione e al database, i cmdlet successivi vengono eseguiti nel database come illustrato nell'esempio seguente:

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
In alternativa, è possibile specificare un percorso di database usando il parametro generico **Path** anziché passare al database.


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
### <a name="using-smo"></a>Utilizzo di SMO

Questo metodo si applica al database SQL di Azure e a SQL Server.
Con SMO, è possibile creare un oggetto di [classe Database](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.database.aspx)e quindi passare l'oggetto usando il parametro **InputObject** di un cmdlet che si connette al database.


```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```


In alternativa, è possibile usare il reindirizzamento:


```
$database | Get-SqlColumnMasterKey
```

## <a name="always-encrypted-tasks-using-powershell"></a>Attività Always Encrypted tramite PowerShell

- [Configure Always Encrypted Keys using PowerShell (Configurare le chiavi Always Encrypted tramite PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md) 
- [Ruotare le chiavi Always Encrypted tramite PowerShell](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Configurare la crittografia della colonna tramite PowerShell](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> Riferimento dei cmdlet di Always Encrypted

Per Always Encrypted sono disponibili i cmdlet di PowerShell seguenti:

|CMDLET |Descrizione
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)**   |Esegue l'autenticazione in Azure e acquisisce un token di autenticazione.
|**[Add-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlcolumnencryptionkeyvalue)**   |Aggiunge un nuovo valore crittografato per un oggetto chiave di crittografia della colonna esistente nel database.
|**[Complete-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/complete-sqlcolumnmasterkeyrotation)**   |Completa la rotazione di una chiave master della colonna.
|**[Get-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnencryptionkey)** |Restituisce tutti gli oggetti chiave di crittografia della colonna definiti nel database oppure un solo oggetto chiave di crittografia della colonna con il nome specificato.
|**[Get-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/get-sqlcolumnmasterkey)** |Restituisce tutti gli oggetti chiave master della colonna definiti nel database oppure un solo oggetto chiave master della colonna con il nome specificato.
|**[Invoke-SqlColumnMasterKeyRotation](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/invoke-sqlcolumnmasterkeyrotation)**   |Avvia la rotazione di una chiave master della colonna.
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)**   |Crea un oggetto SqlColumnMasterKeySettings che descrive una chiave asimmetrica archiviata nell'insieme di credenziali delle chiavi di Azure.
|**[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)**   |Crea un oggetto SqlColumnMasterKeySettings che descrive una chiave asimmetrica archiviata in un archivio chiavi che supporta l'API CNG (Cryptography Next Generation).
|**[New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)** |Crea un oggetto chiave di crittografia della colonna nel database.
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)** |Produce un valore crittografato di una chiave di crittografia della colonna.
|**[New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings)**   |Crea un oggetto SqlColumnEncryptionSettings che incapsula le informazioni sulla crittografia di una singola colonna, tra cui la chiave di crittografia della colonna e il tipo di crittografia.
|**[New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)** |Crea un oggetto chiave master della colonna nel database.
|**[New-SqlColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkeysettings)**|Crea un oggetto SqlColumnMasterKeySettings per una chiave master della colonna con il provider specificato e il percorso della chiave.
|**[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)**   |Crea un oggetto SqlColumnMasterKeySettings che descrive una chiave asimmetrica archiviata in un archivio chiavi con un CSP (Cryptography Service Provider) che supporta l'API Cryptography (CAPI).
|**[Remove-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkey)**   |Rimuove l'oggetto chiave di crittografia della colonna dal database.
|**[Remove-SqlColumnEncryptionKeyValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnencryptionkeyvalue)** |Rimuove un valore crittografato da un oggetto chiave di crittografia della colonna esistente nel database.
|**[Remove-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/remove-sqlcolumnmasterkey)**   |Rimuove l'oggetto chiave master della colonna dal database.
|**[Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)**   |Crittografa, decrittografa o ricrittografa le colonne specificate nel database.



## <a name="additional-resources"></a>Risorse aggiuntive

- [Always Encrypted (Motore di database)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Panoramica della gestione delle chiavi per Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Using Always Encrypted with .NET Framework Data Provider for SQL Server (Uso di Always Encrypted con il provider di dati .NET Framework per SQL Server)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Configurare Always Encrypted usando SQL Server Management Studio](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)


