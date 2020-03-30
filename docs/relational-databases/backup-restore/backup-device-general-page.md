---
title: Dispositivo di backup (pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdevice.general.f1
ms.assetid: c557e37d-319e-4adb-a0c1-94189b15d2ac
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0d37918c0ca2be62c2e620faa8034548df2b4592
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67940822"
---
# <a name="backup-device-general-page"></a>Dispositivo di backup (pagina Generale)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare la pagina **Generale** per specificare o visualizzare le proprietà generali di un dispositivo di backup logica.  
  
 **Per utilizzare SQL Server Management Studio per visualizzare il contenuto di un dispositivo di backup**  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opzioni  
 **Nome dispositivo**  
 Consente di visualizzare il nome di un dispositivo di backup logico esistente o di specificare il nome di un nuovo dispositivo di backup logico.  
  
 **Nastro**  
 Consente di visualizzare o selezionare il dispositivo nastro di destinazione nell'elenco **Nastro** . L'opzione è disponibile solo se un'unità nastro è collegata al computer su cui è in esecuzione l'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!NOTE]  
>  I dispositivi di backup su nastro collegati a computer remoti non rappresentano destinazioni di backup valide.  
  
 **File**  
 Consente di visualizzare il file di destinazione di un dispositivo di backup logico esistente o di specificare un file di destinazione per un nuovo dispositivo di backup logico.  
  
-   Per un dispositivo di backup logico esistente, viene visualizzato il percorso del file di backup. Il campo **File** non è modificabile e il pulsante (...) non è disponibile.  
  
-   Per un nuovo dispositivo di backup logico, è necessario specificare il percorso del file di backup per il quale si sta definendo il dispositivo di backup logico. Non è necessario che il file sia già esistente.  
  
     Per specificare un file di backup locale, è possibile fare clic sul pulsante (...) a destra della casella di testo **File** . Quindi, nella finestra di dialogo **Individua file di database** è possibile passare a qualsiasi posizione su una delle unità fisse del computer sul quale è in esecuzione l'istanza del server. Se il file di backup non esiste ancora, è necessario immettere il nome del file che si desidera utilizzare nel campo **Nome file** della finestra di dialogo.  
  
     In alternativa, è possibile modificare il campo **File** manualmente per ignorare il percorso, il nome del file e l'estensione predefiniti. Per specificare un file remoto come destinazione di backup, utilizzare il nome completo in formato UNC (Universal Naming Convention). Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
    > [!IMPORTANT]  
    >  Poiché l'esecuzione del backup dei dati in rete può essere soggetta a errori di rete, è consigliabile verificare l'operazione di backup dopo il suo completamento. Per altre informazioni, vedere [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
## <a name="remarks"></a>Osservazioni  
 I backup disponibili in un set di uno o più dispositivi di backup costituiscono un singolo set di supporti. Un *set di supporti* è una raccolta ordinata di supporti di backup, nastri o file su disco, su cui una o più operazioni di backup hanno eseguito la scrittura utilizzando un tipo e un numero fisso di dispositivi di backup. Per informazioni sui set di supporti, vedere [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 Il dispositivo di backup fisico corrisponde a un dispositivo di backup logico che viene inizializzata quando il primo backup nel set di supporti viene scritto sul dispositivo di backup logico. Se il dispositivo di backup fisico è un file non ancora esistente, viene creato in quel momento.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definizione di un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Impostazione della data di scadenza di un backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare i file di dati e i file di log in un set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ripristinare un backup da un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
