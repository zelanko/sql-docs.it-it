---
title: Seleziona destinazione di backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d9b4a0e07f32e074ff7e8875c263615bcebc12d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874875"
---
# <a name="select-backup-destination"></a>Seleziona destinazione di backup
  Usare la finestra di dialogo **Seleziona destinazione di backup** per selezionare un dispositivo come destinazione di backup. La destinazione di backup può essere un disco o un dispositivo di backup logico.  
  
 **Per utilizzare SQL Server Management Studio per l'esecuzione del backup di un database**  
  
-   [Creazione di un backup completo del database &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Eseguire il backup di file e filegroup &#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>Opzioni  
 Le opzioni disponibili in questa finestra di dialogo variano a seconda che si selezioni una destinazione su disco o su nastro.  
  
 **Destinazioni su disco**  
 Per specificare una destinazione di backup, scegliere una delle opzioni seguenti.  
  
|||  
|-|-|  
|**Nome file**|Scegliere questa opzione per immettere il nome di un file locale o remoto da utilizzare come destinazione di backup nella casella di testo.<br /><br /> Per specificare un file locale, fare clic sul pulsante Sfoglia a destra della casella di testo e individuare il file nei dischi rigidi del computer che esegue il server oppure digitare direttamente il nome e il percorso completo del file, ad esempio `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`.<br /><br /> Per specificare un file remoto come destinazione di backup, utilizzare il nome completo in formato UNC (Universal Naming Convention). Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md).<br /><br /> **\*\* Importante \*\*** L'esecuzione del backup dei dati in rete può essere soggetta a errori di rete, quindi è consigliabile verificare l'operazione di backup dopo il suo completamento. Per altre informazioni, vedere [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).|  
|**Dispositivo di backup**|Scegliere questa opzione per selezionare un dispositivo di backup logico.<br /><br /> Nota: Per informazioni su come creare un dispositivo di backup su disco, vedere [definire un dispositivo di Backup logico per un File di disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md).|  
  
 **Destinazioni su nastro**  
 Consente di specificare una destinazione di backup su un'unità nastro fisicamente collegata al computer che esegue il server, ovvero l'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Scegliere una delle opzioni seguenti:  
  
|||  
|-|-|  
|**Unità nastro**|Scegliere questa opzione per selezionare un'unità nastro come destinazione del backup dall'elenco delle unità nastro fisicamente collegate al computer che esegue l'istanza del server.<br /><br /> Nota: I dispositivi di backup su nastro collegati a computer remoti non rappresentano destinazioni di backup valide.|  
|**Dispositivo di backup**|Scegliere questa opzione per selezionare un dispositivo di backup logico esistente. Questi dispositivi di backup logici corrispondono a unità nastro fisicamente collegate al computer che esegue l'istanza del server.<br /><br /> Nota: Per informazioni su come creare un dispositivo di backup su nastro, vedere [definire un dispositivo di Backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
