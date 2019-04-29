---
title: Dispositivo di backup (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a4f23fd3d6d8208410c520676ee4e0c8bbe00fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922142"
---
# <a name="backup-device-general-page"></a>Dispositivo di backup (pagina Generale)
  Utilizzare la pagina **Generale** per specificare o visualizzare le proprietà generali di un dispositivo di backup logica.  
  
 **Per utilizzare SQL Server Management Studio per visualizzare il contenuto di un dispositivo di backup**  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opzioni  
 **Nome dispositivo**  
 Consente di visualizzare il nome di un dispositivo di backup logico esistente o di specificare il nome di un nuovo dispositivo di backup logico.  
  
 **Tape**  
 Consente di visualizzare o selezionare il dispositivo nastro di destinazione nell'elenco **Nastro** . L'opzione è disponibile solo se un'unità nastro è collegata al computer in cui è in esecuzione l'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!NOTE]  
>  I dispositivi di backup su nastro collegati a computer remoti non rappresentano destinazioni di backup valide.  
  
 **File**  
 Consente di visualizzare il file di destinazione di un dispositivo di backup logico esistente o di specificare un file di destinazione per un nuovo dispositivo di backup logico.  
  
-   Per un dispositivo di backup logico esistente, viene visualizzato il percorso del file di backup. Il campo **File** non è modificabile e il pulsante (...) non è disponibile.  
  
-   Per un nuovo dispositivo di backup logico, è necessario specificare il percorso del file di backup per il quale si sta definendo il dispositivo di backup logico. Non è necessario che il file sia già esistente.  
  
     Per specificare un file di backup locale, è possibile fare clic sul pulsante (...) a destra della casella di testo **File** . Quindi, nella finestra di dialogo **Individua file di database** è possibile passare a qualsiasi posizione su una delle unità fisse del computer sul quale è in esecuzione l'istanza del server. Se il file di backup non esiste ancora, è necessario immettere il nome del file che si desidera utilizzare nel campo **Nome file** della finestra di dialogo.  
  
     In alternativa, è possibile modificare il campo **File** manualmente per ignorare il percorso, il nome del file e l'estensione predefiniti. Per specificare un file remoto come destinazione di backup, utilizzare il nome completo in formato UNC (Universal Naming Convention). Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Poiché l'esecuzione del backup dei dati in rete può essere soggetta a errori di rete, è consigliabile verificare l'operazione di backup dopo il suo completamento. Per altre informazioni, vedere [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql).  
  
## <a name="remarks"></a>Note  
 I backup disponibili in un set di uno o più dispositivi di backup costituiscono un singolo set di supporti. Un *set di supporti* è una raccolta ordinata di supporti di backup, nastri o file su disco, su cui una o più operazioni di backup hanno eseguito la scrittura utilizzando un tipo e un numero fisso di dispositivi di backup. Per informazioni sui set di supporti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
 Il dispositivo di backup fisico corrisponde a un dispositivo di backup logico che viene inizializzata quando il primo backup nel set di supporti viene scritto sul dispositivo di backup logico. Se il dispositivo di backup fisico è un file non ancora esistente, viene creato in quel momento.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definire un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [Impostare la data di scadenza di un backup &#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare i file di dati e i file di log in un set di backup &#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ripristino di un backup da un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
