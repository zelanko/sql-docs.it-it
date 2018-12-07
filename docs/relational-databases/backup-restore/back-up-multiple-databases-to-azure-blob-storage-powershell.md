---
title: Backup di più database nel servizio di archiviazione BLOB di Azure - PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3f043a9df2b561fb9fbd7a56c993838137b0601d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512887"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>Backup di più database nel servizio di archiviazione BLOB di Azure - PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento vengono forniti alcuni script di esempio che possono essere utilizzati per automatizzare i backup nel servizio di archiviazione BLOB di Windows Azure mediante i cmdlet di PowerShell.  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>Panoramica dei cmdlet di PowerShell per il backup e il ripristino  
 **Backup-SqlDatabase** e **Restore-SqlDatabase** sono i due principali cmdlet disponibili per eseguire operazioni di backup e ripristino. Inoltre, sono presenti altri cmdlet che possono essere necessari per automatizzare i backup nel servizio di archiviazione BLOB di Windows Azure come il set di cmdlet **SqlCredential** . Di seguito è riportato un elenco di cmdlet di PowerShell disponibili in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzati nelle operazioni di backup e ripristino:  
  
 Backup-SqlDatabase  
 Questo cmdlet viene utilizzato per creare un backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Restore-SqlDatabase  
 Questo cmdlet viene utilizzato per ripristinare un database.  
  
 New-SqlCredential  
 Questo cmdlet viene utilizzato per creare le credenziali SQL da utilizzare per il backup di SQL Server nel servizio di archiviazione di Windows Azure. Per altre informazioni sulle credenziali e sul relativo uso nelle operazioni di backup e ripristino di SQL Server, vedere [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 Get-SqlCredential  
 Questo cmdlet viene utilizzato per recuperare l'oggetto Credential e le relative proprietà.  
  
 Remove-SqlCredential  
 Questo cmdlet viene utilizzato per eliminare un oggetto Credential di SQL.  
  
 Set-SqlCredential  
 Questo cmdlet viene utilizzato per modificare o impostare le proprietà dell'oggetto Credential di SQL.  
  
> [!TIP]  
>  I cmdlet relativi alle credenziali vengono utilizzati nelle operazioni di backup e ripristino negli scenari del servizio di archiviazione BLOB di Windows Azure.  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>PowerShell per le operazioni di backup di più istanze di più database  
 Nelle sezioni seguenti vengono forniti alcuni script per diverse operazioni quali la creazione di credenziali SQL in più istanze di SQL Server, il backup di tutti i database utente in un'istanza di SQL Server e simili. È possibile utilizzare questi script per automatizzare e pianificare le operazioni di backup in base ai requisiti dell'ambiente. Gli script forniti di seguito sono esempi e possono essere modificati o estesi per l'ambiente in uso.  
  
 Di seguito sono riportate alcune considerazioni per gli script di esempio:  
  
1.  **Spostamento all'interno dei percorsi di SQL Server PowerShell:** Windows PowerShell implementa alcuni cmdlet per spostarsi all'interno della struttura del percorso che rappresenta la gerarchia di oggetti supportati da un provider PowerShell. Quando si passa a un nodo nel percorso, è possibile utilizzare altri cmdlet per eseguire operazioni di base sull'oggetto corrente.  
  
2.  Cmdlet**Get-ChildItem** : le informazioni restituite da **Get-ChildItem** dipendono dal percorso di PowerShell per SQL Server. Ad esempio, se il percorso è a livello di computer, questo cmdlet restituisce tutte le istanze del motore di database di SQL Server installate nel computer. Sempre a titolo di esempio, se il percorso è a livello di oggetto come i database, questo cmdlet restituisce un elenco di oggetti di database.  Per impostazione predefinita il cmdlet **Get-ChildItem** non restituisce oggetti di sistema.  Se si usa il parametro -Force, è possibile visualizzare gli oggetti di sistema.  
  
     Per altre informazioni, vedere [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md).  
  
3.  Ogni esempio di codice può essere utilizzato in modo indipendente modificando i valori di variabili, tuttavia la creazione di un account di archiviazione Windows Azure e delle credenziali SQL è un prerequisito necessario per tutte le operazioni di backup e ripristino nel servizio di archiviazione BLOB di Windows Azure.  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>Creare le credenziali SQL in tutte le istanze di SQL Server  
 Sono disponibili due script di esempio, entrambi per la creazione delle credenziali SQL "mybackupToURL" in tutte le istanze di SQL Server in un computer. Il primo esempio è semplice e consente di creare le credenziali senza intercettare eccezioni.  Se ad esempio sono già presenti credenziali esistenti con lo stesso nome in una delle istanze del computer, lo script avrà esito negativo. Nel secondo esempio vengono intercettati gli errori consentendo allo script di continuare.  
  
```  
  
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | new-sqlcredential -Name $credentialName  -Identity $storageAccount -Secret $secureString  
```  
  
```  
  
import-module sqlps  
  
# set the parameter values  
  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#loop through instances and create a SQL credential, output any errors  
foreach ($instance in $instances)  
{  
    Try  
{  
     new-sqlcredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop   
}  
Catch [Exception]  
    {  
  
            write-host "instance - $($instance.name): "$_.Exception.Message  
  
    }  
  
 }  
  
```  
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>Rimuovere le credenziali SQL da tutte le istanze di SQL Server  
 Questo script può essere utilizzato per rimuovere credenziali specifiche da tutte le istanze di SQL Server installate nel computer. Se l'oggetto Credential non esiste in un'istanza specifica, viene visualizzato un messaggio di errore e lo script continua finché non vengono controllate tutte le istanze.  
  
```  
  
import-module sqlps  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-childitem  
  
foreach ($instance in $instances)  
   {   
    try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-sqlCredential -path $path -ea stop   
         }  
         catch [Exception]  
         {  
            write-host $_.Exception.Message  
  
        }  
  
    }  
```  
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>Backup completo del database per tutti i database (compresi i database di sistema)  
 Lo script seguente consente di creare i backup di tutti i database presenti nel computer, sia database utente che database di sistema **msdb** . Nello script vengono esclusi tramite filtro i database di sistema **tempdb** e **model** .  
  
```  
  
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 foreach ($instance in $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = get-childitem -Force -path $path |Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
  
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>Backup completo del database per tutti i database utente  
 Lo script seguente può essere utilizzato per eseguire il backup di tutti i database utente in tutte le istanze di SQL Server presenti nel computer.  
  
```  
  
import-module sqlps   
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the user databases  
 foreach ($instance in $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
   $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On   
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>Backup completo del database per MASTER e MSDB (database di sistema) in tutte le istanze di SQL Server  
 Lo script seguente può essere utilizzato per eseguire il backup dei database **master** e **msdb** in tutte le istanze di SQL Server installate nel computer.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
foreach ($instance in $instances)  
 {  
      foreach ($s in $sysdbs)  
     {  
Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}    
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>Backup completo del database per tutti i database utente di un'istanza di SQL Server  
 Lo script seguente viene utilizzato per eseguire il backup solo dei database utente disponibili in un'istanza denominata di SQL Server. Lo stesso script può essere utilizzato per l'istanza predefinita del computer modificando il valore del parametro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>Backup completo del database solo per i database di sistema (MASTER e MSDB) in un'istanza di SQL Server  
 Lo script seguente può essere utilizzato per eseguire il backup dei database **master** e **msdb** in un'istanza denominata di SQL Server. Lo stesso script può essere utilizzato per l'istanza predefinita del computer modificando il valore del parametro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
foreach ($s in $sysDbs)   
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
