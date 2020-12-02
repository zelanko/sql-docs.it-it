---
title: Sequenze di ripristino (modello di recupero con registrazione completa) | Microsoft Docs
description: Informazioni su come pianificare ed eseguire una sequenza di ripristino, costituita da istruzioni RESTORE, per un database di SQL Server che usa solitamente il modello di recupero con registrazione completa.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
author: cawrites
ms.author: chadam
ms.openlocfilehash: 8ac088e916736ee852cd828735c988f134ec4978
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129189"
---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>Pianificare ed eseguire sequenze di ripristino (Modello di recupero con registrazione completa)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  In questo argomento si spiega come pianificare ed eseguire una sequenza di ripristino per un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui viene utilizzato in genere il modello di recupero con registrazione completa. Una *sequenza di ripristino* è una sequenza contenente una o più istruzioni [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) . In genere, consente di inizializzare il contenuto del database, dei file e/o delle pagine in fase di ripristino (fase di copia dei dati), di eseguire il roll forward delle transazioni registrate (fase di rollforward) e quindi di eseguire il rollback delle transazioni di cui non è stato eseguito il commit (fase di rollback).  
  
 In scenari semplici, per una sequenza di ripristino sono necessari solo un backup completo del database, un backup differenziale del database e i successivi backup del log. In questi casi, la formulazione di una corretta sequenza di ripristino è un'operazione semplice. Per ripristinare ad esempio un intero database fino al punto in cui si è verificato un errore, eseguire innanzitutto il backup del log delle transazioni attivo (la *parte finale* del log). Ripristinare quindi il backup completo del database più recente, l'eventuale backup differenziale più recente e tutti i successivi backup del log nell'ordine in cui sono stati eseguiti.  
  
 In scenari più complessi, la formulazione di una corretta sequenza di ripristino può risultare difficile. Una sequenza di ripristino potrebbe ad esempio richiedere più backup di file oppure il ripristino dei dati fino a un punto nel tempo specifico. In scenari estremamente complessi, potrebbe persino essere necessario attraversare un percorso di recupero che si estende su uno o più fork di recupero.  
  
> [!NOTE]  
>  Un *percorso di recupero* è la sequenza di dati e di backup del log che hanno portato un database a un determinato momento, noto come punto di recupero. Un percorso di recupero è costituito da un set specifico di trasformazioni che hanno determinato la modifica del database nel corso del tempo, mantenendone tuttavia la coerenza. Un percorso di recupero descrive un intervallo di LSN da un punto di inizio (LSN,GUID) a un punto di fine (LSN,GUID). È possibile che l'intervallo di LSN in un percorso di recupero attraversi uno o più rami di recupero dall'inizio alla fine.  
  
## <a name="to-plan-a-restore-sequence"></a>Per pianificare una sequenza di ripristino  
 Prima di avviare una sequenza di ripristino, effettuare le operazioni seguenti:  
  
1.  Se possibile, creare un backup della parte finale del log per il database. Per altre informazioni, vedere [Backup della parte finale del log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
2.  Determinare il punto di recupero previsto.  
  
     Il punto di recupero previsto può corrispondere a un qualsiasi punto nel tempo o un qualsiasi contrassegno all'interno di un backup del log delle transazioni. Per altre informazioni, vedere [Ripristinare un database di SQL Server fino a un punto specifico &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md) o [Usare transazioni contrassegnate per recuperare coerentemente i database correlati &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
3.  Determinare il tipo di ripristino che si desidera eseguire. Per altre informazioni, vedere [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
4.  Individuare i backup necessari e verificare che siano disponibili i set di supporti e i dispositivi di backup appropriati. Per altre informazioni, vedere [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md) e [Set di supporti, gruppi di supporti e set di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
## <a name="to-perform-a-restore-sequence"></a>Per eseguire una sequenza di ripristino  
 Per eseguire una sequenza di ripristino, effettuare le operazioni seguenti:  
  
1.  Per avviare la sequenza, ripristinare uno o più backup dei dati, ad esempio un backup del database, un backup parziale, uno o più backup di file.  
  
2.  Ripristinare facoltativamente gli ultimi backup differenziali basati su questi backup completi.  
  
     Per ogni backup completo che si prevede di ripristinare, determinare se viene utilizzato come base per qualsiasi backup differenziale. In tal caso, ripristinare se possibile il backup differenziale più recente. Per altre informazioni, vedere [Backup differenziali &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
3.  Eseguire il rollforward del database ripristinando in sequenza i backup del log e terminando con il backup che include il punto di recupero. L'applicazione o meno di tutti i backup del log dipende dal backup del log che contiene il punto di recupero previsto, come descritto di seguito:  
  
    -   Se il punto di recupero corrisponde al punto in cui si è verificato un errore, è necessario ripristinare tutti i backup del log creati dopo l'ultimo backup dei dati completo o differenziale ripristinato. Per altre informazioni, vedere [Applicazione dei backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
    -   Nel caso di un ripristino temporizzato, i backup del log più recenti potrebbero non essere necessari. Se si utilizza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], tramite Database Recovery Advisor viene assicurato che vengano selezionati solo i backup necessari per eseguire il ripristino alla temporizzazione specificata. Questi backup costituiscono il piano di ripristino consigliato per il ripristino temporizzato. Per altre informazioni, vedere [Ripristino di un database di SQL Server fino a un punto specifico all'interno di un backup &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
## <a name="restarting-a-restore-sequence"></a>Riavvio di una sequenza di ripristino  
 Se l'esito di una sequenza di ripristino viene compromesso da un problema, è possibile interrompere la sequenza e riavviarla dall'inizio. Se, ad esempio, si ripristina per errore un numero eccessivo di backup del log e si supera il punto di recupero desiderato, è necessario riavviare la sequenza di ripristino fino al backup del log che contiene il punto di recupero previsto.  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Panoramica del ripristino e del recupero &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Ripristino online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Ripristini di file &#40;modello di recupero con registrazione completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Ripristino di pagine &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Ripristini a fasi &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
