---
title: Eliminazione dei file BLOB di backup con lease attivi | Microsoft Docs
description: Se un backup o un ripristino di SQL Server non riesce, un BLOB in archiviazione di Azure può diventare orfano. Informazioni su come eliminare un BLOB orfano.
ms.custom: ''
ms.date: 08/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 95b7165fb16832b8b76e6a9c7a331433d49ff0a9
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809637"
---
# <a name="delete-backup-blob-files-with-active-leases"></a>Eliminare i file BLOB di backup con lease attivi

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Quando si esegue il backup nell'archiviazione di Microsoft Azure o il ripristino dallo stesso, tramite SQL Server viene acquisito un lease infinito per bloccare l'accesso esclusivo al BLOB. Quando il processo di backup o ripristino viene completato correttamente, il lease viene rilasciato. Se il backup o il ripristino non viene completato, il processo di backup tenta di eliminare i BLOB non validi. Tuttavia, se il backup non viene completato a causa di un problema di connettività di rete che persiste nel tempo, è possibile che il processo di backup non sia in grado di accedere al BLOB e che quindi quest'ultimo rimanga orfano. Di conseguenza, il BLOB non può essere scritto o eliminato finché il lease non viene rilasciato. In questo argomento viene descritto come rilasciare (interrompere) il lease ed eliminare il BLOB.
  
Per altre informazioni sui tipi di lease, leggere questo [articolo](/rest/api/storageservices/Lease-Blob).  
  
Il mancato completamento dell'operazione di backup potrebbe generare un file di backup non valido. Anche nel file BLOB di backup potrebbe essere presente un lease attivo, impedendone l'eliminazione o la sovrascrittura. Per eliminare o sovrascrivere questi BLOB, il lease deve innanzitutto essere rilasciato (interrotto). Se sono presenti errori di backup, è consigliabile rimuovere i lease ed eliminare i BLOB. Periodicamente, è anche possibile rimuovere i lease ed eliminare i BLOB come parte dell'attività di gestione della risorsa di archiviazione.  
  
Se si verifica un errore di ripristino, i ripristini successivi non vengono bloccati, quindi il lease attivo potrebbe non essere un problema. L'interruzione del lease è necessaria solo quando si deve sovrascrivere o eliminare il BLOB.  
  
## <a name="manage-orphaned-blobs"></a>Gestire i BLOB orfani

Nei passaggi seguenti viene descritto come effettuare una rimozione dopo un backup non riuscito o un'attività di ripristino. È possibile eseguire tutti i passaggi tramite gli script di PowerShell. La sezione seguente include un esempio di script di PowerShell:  
  
1. **Identificare i BLOB con lease:** se si usa uno script o un processo in cui vengono eseguiti i processi di backup, è possibile rilevare l'errore nello script o nel processo e usarlo per rimuovere i BLOB.  È anche possibile usare le proprietà LeastState e LeaseStats per identificare i BLOB con lease. Dopo aver identificato i BLOB, rivedere l'elenco e verificare la validità del file di backup prima di eliminare il BLOB.  
  
1. **Interrompere il lease:** usando una richiesta autorizzata è possibile interrompere il lease senza specificare un relativo ID. Per altre informazioni, fare clic [qui](/rest/api/storageservices/Lease-Blob) .  
  
    > [!TIP]  
    > Tramite SQL Server viene generato un ID lease per stabilire l'accesso esclusivo durante l'operazione di ripristino. L'ID lease di ripristino è BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
1. **Eliminare il BLOB:** per eliminare un BLOB con un lease attivo, per prima cosa è necessario interrompere il lease.  

###  <a name="powershell-script-example"></a><a name="Code_Example"></a> Esempio di script di PowerShell  
  
> [!IMPORTANT]
> Se si esegue PowerShell 2.0 potrebbero verificarsi dei problemi durante il caricamento dell'assembly Microsoft.WindowsAzure.Storage.dll. È consigliabile eseguire l'aggiornamento di [Powershell](/powershell/) per risolvere il problema. È anche possibile usare la soluzione seguente per creare o modificare il file powershell.exe.config per caricare gli assembly .NET 2.0 e .NET 4.0 in fase di esecuzione come segue:  
>
> ```xml
> <?xml version="1.0"?>
>     <configuration>
>         <startup useLegacyV2RuntimeActivationPolicy="true">
>             <supportedRuntime version="v4.0.30319"/>
>             <supportedRuntime version="v2.0.50727"/>
>         </startup>
>     </configuration>  
> ```  
  
 Lo script di esempio seguente identifica i BLOB con lease attivi e quindi li interrompe. Nell'esempio viene anche descritto come applicare i filtri per gli ID lease di rilascio.  
  
#### <a name="tips-on-running-this-script"></a>Suggerimenti per l'esecuzione di questo script
  
> [!WARNING]  
> Se viene eseguito un backup nel servizio Archiviazione BLOB di Azure contemporaneamente a questo script, è possibile che il backup non venga completato perché il lease che il backup sta tentando di acquisire verrà interrotto dallo script. Eseguire questo script durante un periodo di manutenzione o quando non sono in atto esecuzioni di backup.  
  
- Prima di eseguire questo script, è necessario aggiungere valori per l'account e la chiave di archiviazione, il contenitore, nonché per i parametri del percorso e del nome dell'assembly di archiviazione di Azure. Il percorso dell'assembly di archiviazione è la directory di installazione dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il nome del file per l'assembly di archiviazione è Microsoft.WindowsAzure.Storage.dll.
  
- Se non sono presenti BLOB con lease bloccati, dovrebbe essere visualizzato il messaggio seguente: `There are no blobs with locked lease status`
  
- Se sono presenti BLOB con lease bloccati, dovrebbero essere visualizzati i messaggi seguenti: `Breaking Leases`, `The lease on <URL of the Blob> is a restore lease: You will see this message only if you have a blob with a restore lease that is still active.` e `The lease on <URL of the Blob> is not a restore lease Breaking lease on <URL of the Bob>.`
  
```powershell
$storageAccount = "<myStorageAccount>"
$storageKey = "<myStorageKey>"
$blobContainer = "<myBlobContainer>"
$storageAssemblyPathName = "<myStorageAssemblyPathName>"
  
# well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
# list all the blobs  
$blobs = $container.ListBlobs($null,$true)
  
# filter blobs that are have Lease Status as "locked"
$lockedBlobs = @()  
foreach($blob in $blobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases..."
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease."  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease."  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)."  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
} else { Write-Host " There are no blobs with locked lease status." }
```  
  
## <a name="see-also"></a>Vedere anche

[Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)