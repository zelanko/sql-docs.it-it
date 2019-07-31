---
title: Dispositivo di backup (pagina Contenuto supporti)| Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdevice.contents.f1
ms.assetid: 5fc7bd22-b6d8-4af1-8a58-2e7d0b994d08
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c877ffb5bb15836f21a6a37c7cd8ccb22b27cc10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987768"
---
# <a name="backup-device-media-contents-page"></a>Dispositivo di backup (pagina Contenuto supporti)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare la finestra di dialogo **Dispositivo di backup** per visualizzare le informazioni di backup. Vengono riportate informazioni sul dispositivo, sui supporti, sul set di supporti e sul set o i set di backup.  
  
 **Per utilizzare SQL Server Management Studio per visualizzare il contenuto di un dispositivo di backup**  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opzioni  
 Visualizzare informazioni relative al supporto specifico, al set di supporti e ai set di backup.  
  
 **Supporti**  
 Disco o set di nastri in cui sono archiviate le informazioni di backup.  
  
 **Sequenza supporti**  
 Consente di visualizzare il numero di sequenza dei supporti, il numero di sequenza del gruppo e l'identificatore del mirror, se disponibili. Ogni supporto di backup fisico è contrassegnato con un numero di sequenza dei supporti che indica l'ordine in cui i supporti sono stati utilizzati. Il supporto di backup iniziale è contrassegnato con 1, il secondo supporto, ovvero il primo nastro di continuità, con 2 e così via. Quando viene ripristinato il set di backup, i numeri di sequenza dei supporti consentono all'operatore che esegue il ripristino del backup di caricare i supporti in base all'ordine corretto.  
  
 **Data creazione**  
 Consente di visualizzare la data e l'ora di creazione del set di supporti.  
  
 **Set di supporti**  
 Un set di supporti consiste in una raccolta ordinata di supporti di backup su cui è stata eseguita la scrittura di una o più operazioni di backup utilizzando un numero costante di dispositivi di backup.  
  
 **Nome**  
 Consente di visualizzare il nome del set di supporti, se disponibile.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione del set di supporti, se disponibile.  
  
 **Conteggio gruppo di supporti**  
 Consente di visualizzare il numero di gruppi contenuti nel set di supporti. Ogni set di supporti è un insieme formato da uno o più gruppi di supporti. L'output per un determinato dispositivo di backup individuale o per un gruppo di dispositivi di backup con mirroring forma un gruppo di supporti distinto. Ogni set di supporti contiene un gruppo di supporti per ciascun dispositivo distinto o per un gruppo di dispositivi con mirroring. Ad esempio, se un set di supporti utilizza due dispositivi di backup senza mirroring, il set di supporti conterrà due gruppi di supporti.  
  
 **Set di backup**  
 Visualizza informazioni sul set o i set di backup contenuti nel supporto. Un set di backup è il risultato di un'operazione di backup riuscita il cui contenuto viene distribuito tra i supporti del set di dispositivi di backup.  
  
|Intestazione|Valori|  
|------------|------------|  
|**Nome**|Nome del set di backup.|  
|**Tipo**|Oggetto di cui è stato eseguito il backup: database, file o *\<vuoto>* , nel caso dei log delle transazioni.|  
|**Componente**|Tipo di operazione di backup eseguita: Completo, Differenziale o Log delle transazioni.|  
|**Server**|Nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ha eseguito l'operazione di backup.|  
|**Database**|Nome del database di cui è stato eseguito il backup.|  
|**Posizione**|Posizione del set di backup nel volume.|  
|**Data**|Data e ora di fine dell'operazione di backup, visualizzate in base alle impostazioni internazionali del client.|  
|**Dimensione**|Dimensioni in byte del set di backup.|  
|**Nome utente**|Nome dell'utente che ha eseguito l'operazione di backup.|  
|**Scadenza**|Data e ora di scadenza del set di backup.|  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Definire un dispositivo di backup logico per un file su disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definire un dispositivo di backup logico per un'unità nastro &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Specificare un disco o un nastro come destinazione di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminare un dispositivo di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Impostare la data di scadenza di un backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Visualizzare il contenuto di un nastro o di un file di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Visualizzare i file di dati e i file di log in un set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Visualizzare le proprietà e il contenuto di un dispositivo di backup logico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ripristinare un backup da un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
