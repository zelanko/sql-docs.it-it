---
title: Configurazione dell'archiviazione - Cache write-back NVDIMM-N
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 861862fa-9900-4ec0-9494-9874ef52ce65
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b2f0434041b7573bc8c32e2618a64a0f900561fb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85655751"
---
# <a name="configuring-storage-spaces-with-a-nvdimm-n-write-back-cache"></a>Configurazione di spazi di archiviazione con una cache write-back NVDIMM-N
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Windows Server 2016 supporta i dispositivi NVDIMM N che consentono operazioni di input/output (I/O) estremamente veloci. Un uso interessante di tali dispositivi è come cache write-back per ottenere latenze di scrittura ridotte. Questo argomento illustra come configurare uno spazio di archiviazione con mirroring con una cache write-back NVDIMM-N con mirroring come unità virtuale per archiviare il log delle transazioni di SQL Server. Se si vuole usare lo spazio anche per archiviare tabelle di dati o altri dati, è possibile includere più dischi nel pool di archiviazione o creare più pool, se l'isolamento è importante.  
  
 Per un video di Channel 9 sull'uso di questa tecnica, vedere [Using Non-volatile Memory (NVDIMM-N) as Block Storage in Windows Server 2016](https://channel9.msdn.com/Events/Build/2016/P466)(Uso di memoria non volatile (NVDIMM-N) come archiviazione a blocchi in Windows Server 2016).  
  
## <a name="identifying-the-right-disks"></a>Identificazione dei dischi  
 Il modo più semplice per configurare gli spazi di archiviazione in Windows Server 2016, soprattutto con funzionalità avanzate come le cache write-back, consiste nell'usare PowerShell. Il primo passaggio consiste nell'identificare i dischi che dovranno far parte del pool di spazi di archiviazione dal quale verrà creato il disco virtuale. I dispositivi NVDIMM-N hanno un tipo di supporto e un tipo di bus SCM (Storage Class Memory) per i quali è possibile eseguire query tramite il cmdlet Get-PhysicalDisk di PowerShell.  
  
```  
Get-PhysicalDisk | Select FriendlyName, MediaType, BusType  
```  
  
 ![Get-PhysicalDisk](../../relational-databases/performance/media/get-physicaldisk.png "Get-PhysicalDisk")  
  
> [!NOTE]  
>  Con i dispositivi NVDIMM-N non è più necessario selezionare appositamente i dispositivi che possono essere destinazioni di cache write-back.  
  
 Per creare un disco virtuale con mirroring con cache write-back con mirroring sono necessari almeno 2 dispositivi NVDIMM-N e 2 altri dischi. L'assegnazione dei dischi fisici a una variabile prima di creare il pool semplifica il processo.  
  
```  
$pd =  Get-PhysicalDisk | Select FriendlyName, MediaType, BusType | WHere-Object {$_.FriendlyName -like 'MK0*' -or $_.FriendlyName -like '2c80*'}  
```  
  
 Lo screenshot mostra la variabile $pd e le 2 unità SSD e i 2 dispositivi NVDIMM-N cui è assegnata restituiti dal cmdlet PowerShell seguente.  
  
```  
$pd | Select FriendlyName, MediaType, BusType  
```  
  
 ![Select FriendlyName](../../relational-databases/performance/media/select-friendlyname.png "Select FriendlyName")  
  
## <a name="creating-the-storage-pool"></a>Creazione del pool di archiviazione  
 Con la variabile $pd contenente i dischi fisici è facile creare il pool di archiviazione usando il cmdlet New-StoragePool di PowerShell.  
  
```  
New-StoragePool -StorageSubSystemFriendlyName "Windows Storage*" -FriendlyName NVDIMM_Pool -PhysicalDisks $pd  
```  
  
 ![New-StoragePool](../../relational-databases/performance/media/new-storagepool.png "New-StoragePool")  
  
## <a name="creating-the-virtual-disk-and-volume"></a>Creazione del disco virtuale e del volume  
 Dopo aver creato un pool, il passaggio successivo consiste nel creare e formattare un disco virtuale. In questo caso verrà creato 1 solo disco virtuale ed è possibile usare il cmdlet New-Volume di PowerShell per semplificare questo processo:  
  
```  
New-Volume -StoragePool (Get-StoragePool -FriendlyName NVDIMM_Pool) -FriendlyName Log_Space -Size 300GB -FileSystem NTFS -AccessPath S: -ResiliencySettingName Mirror  
```  
  
 ![New-Volume](../../relational-databases/performance/media/new-volume.png "New-Volume")  
  
 Il disco virtuale è stato creato, inizializzato e formattato con NTFS. La schermata seguente indica che il disco ha una dimensione di 300 GB e una cache di scrittura di 1 GB che verrà ospitata nei dispositivi NVDIMM-N.  
  
 ![Get-VirtualDisk](../../relational-databases/performance/media/get-virtualdisk.png "Get-VirtualDisk")  
  
 È ora possibile visualizzare il nuovo volume nel server. È possibile usare questa unità per il log delle transazioni di SQL Server.  
  
 ![Log_Space Drive](../../relational-databases/performance/media/log-space-drive.png "Log_Space Drive")  
  
## <a name="see-also"></a>Vedere anche  
 [Spazi di archiviazione di Windows in Windows 10](https://windows.microsoft.com/windows-10/storage-spaces-windows-10)   
 [Spazi di archiviazione di Windows in Windows 2012 R2](https://technet.microsoft.com/library/hh831739.aspx)   
 [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Visualizzare o modificare i percorsi predefiniti per i file di dati e di log &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)  
  
  
