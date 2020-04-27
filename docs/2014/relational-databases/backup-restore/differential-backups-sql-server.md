---
title: Backup differenziali (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- differential backups
- differential backups, about
ms.assetid: 123bb7af-1367-4bde-bfcb-76d36799b905
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 179e7aaea331ba565ca5afae7bd51754e23b9718
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62876193"
---
# <a name="differential-backups-sql-server"></a>Backup differenziali [SQL Server]
  Questo argomento relativo a backup e ripristino è applicabile a tutti i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 un backup differenziale si basa sul precedente backup completo dei dati più recente. In un backup differenziale vengono acquisiti solo i dati che hanno subito modifiche dopo il backup completo. Il backup completo su cui si basa un backup differenziale è noto come *base* del backup differenziale. I backup completi, ad eccezione di backup di sola copia, possono servire come base per una serie di backup differenziali, compresi backup di database, backup parziali e backup di file. Il backup di base per un backup differenziale di file può essere contenuto in un backup completo, un backup di file o un backup parziale.  
  
  
##  <a name="benefits"></a><a name="Benefits"></a> Vantaggi  
  
-   La creazione di backup differenziali può risultare molto rapida rispetto alla creazione di un backup completo. Un backup differenziale registra solo i dati modificati dopo l'ultimo backup completo su cui si basa il backup differenziale. Ciò facilita l'esecuzione più frequente di backup dei dati, riducendo il rischio di perdita di dati. Prima di ripristinare un backup differenziale, è tuttavia necessario eseguire il ripristino della relativa base. Pertanto, l'esecuzione di un ripristino da un backup differenziale richiederà necessariamente più passaggi e tempo di un ripristino da un backup completo, poiché sono richiesti due file di backup.  
  
-   I backup differenziali del database risultano particolarmente utili se un subset di un database viene modificato più spesso rispetto al resto del database. In questi casi, i backup differenziali del database consentono di eseguire frequentemente backup evitando l'overhead tipico dei backup completi del database.  
  
-   In base al modello di recupero con registrazione completa, l'utilizzo di backup differenziali può ridurre il numero di backup del log che è necessario ripristinare.  
  
##  <a name="overview-of-differential-backups"></a><a name="Overview"></a> Panoramica dei backup differenziali  
 Un backup differenziale acquisisce lo stato di qualsiasi *extent* (raccolta di otto pagine fisicamente contigue) che ha subito modifiche tra la creazione della base differenziale e la creazione del backup differenziale. Le dimensioni di un determinato backup differenziale dipendono pertanto dalla quantità di dati modificata rispetto alla base. In genere, meno recente è la base, maggiori saranno le dimensioni di un nuovo backup differenziale. In una serie di backup differenziali, è probabile che gli extent aggiornati di frequente contengano dati diversi in ogni backup differenziale.  
  
 Nella figura seguente viene illustrato il funzionamento di un backup differenziale. Nella figura sono illustrati 24 extent di dati, sei dei quali sono stati modificati. Il backup differenziale contiene solo questi sei extent di dati. L'operazione di backup differenziale è basata su una pagina della mappa di bit contenente un bit per ogni extent. Per ogni extent aggiornato rispetto alla base, il bit viene impostato su 1 nella mappa di bit.  
  
 ![La mappa di bit differenziale identifica gli extent modificati](../../database-engine/media/bnr-how-diff-backups-work.gif "La mappa di bit differenziale identifica gli extent modificati")  
  
> [!NOTE]  
>  La mappa di bit differenziale non viene aggiornata da un backup di sola copia. Di conseguenza, un backup di sola copia non influisce sui backup differenziali successivi.  
  
 Un backup differenziale eseguito entro un periodo di tempo relativamente breve dalla base in genere ha dimensioni decisamente più ridotte rispetto alla base differenziale, il che consente di limitare lo spazio di archiviazione e il tempo di esecuzione del backup. Con il passare del tempo, tuttavia, le modifiche apportate a un database comportano un aumento delle differenze tra tale database e una determinata base differenziale. In genere, l'aumento delle dimensioni del backup differenziale è direttamente proporzionale alla lunghezza del periodo che intercorre tra l'esecuzione di un backup differenziale e la creazione della relativa base. Questo significa che, con il passare del tempo, le dimensioni dei backup differenziali possono avvicinarsi a quelle della base differenziale. Un backup differenziale di notevoli dimensioni non offre più i vantaggi correlati alla maggiore rapidità e allo spazio di archiviazione ridotto.  
  
 A causa dell'aumento delle dimensioni dei backup differenziali, il ripristino di un backup di questo tipo può comportare un notevole aumento del tempo necessario per il ripristino di un database. È consigliabile pertanto eseguire un nuovo backup completo a intervalli prestabiliti per creare una nuova base differenziale per i dati. È ad esempio possibile eseguire un backup completo settimanale dell'intero database, ovvero un backup completo del database, seguito da una serie regolare di backup differenziali del database nell'arco della settimana.  
  
 Prima di ripristinare un backup differenziale, è necessario eseguire il ripristino della relativa base. Ripristinare quindi solo il backup differenziale più recente per riportare il database allo stato esistente nel momento in cui è stato creato tale backup differenziale. In genere, si ripristina il backup completo più recente, seguito dal backup differenziale più recente basato su tale backup completo.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>Backup differenziali di database con tabelle con ottimizzazione per la memoria  
 Per informazioni sui backup differenziali e sui database con tabelle ottimizzate per la memoria, vedere [Backup di un database con tabelle ottimizzate per la memoria](../in-memory-oltp/memory-optimized-tables.md).  
  
##  <a name="differential-backups-of-read-only-databases"></a><a name="ReadOnlyDbs"></a> Backup differenziali di database di sola lettura  
 Per i database di sola lettura, i backup completi sono più semplici da gestire quando vengono utilizzati singolarmente anziché in combinazione con i backup differenziali. Quando un database è di sola lettura, il backup e le altre operazioni non sono in grado di modificare i metadati inclusi nel file. I metadati necessari per un backup differenziale, ad esempio il numero di sequenza del file di log in corrispondenza del quale il backup differenziale ha inizio (l'LSN di base del backup differenziale), vengono pertanto archiviati nel database **master** . Se la base differenziale viene creata quando il database è di sola lettura, la mappa di bit differenziale indicherà un numero maggiore di modifiche rispetto a quelle effettivamente apportate dopo il backup di base. I dati aggiuntivi vengono letti dal backup, ma non vengono scritti nel backup, perché tramite il valore **differential_base_lsn** archiviato nella tabella di sistema [backupset](/sql/relational-databases/system-tables/backupset-transact-sql) viene determinato se i dati sono realmente cambiati dopo la creazione della base.  
  
 Quando viene ricompilato, ripristinato oppure scollegato e collegato un database di sola lettura, le informazioni relative alla base differenziale vengono perse perché il database **master** non è sincronizzato con il database utente. Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non è in grado di rilevare né evitare questo problema. Gli eventuali backup differenziali successivi non saranno basati sul backup completo più recente e potrebbero generare risultati imprevisti. Per creare una nuova base differenziale, è consigliabile eseguire un backup completo del database.  
  
### <a name="best-practices-for-using-differential-backups-with-a-read-only-database"></a>Procedure consigliate per l'utilizzo di backup differenziali con un database di sola lettura  
 Se dopo la creazione di un backup completo di un database di sola lettura si ha intenzione di creare un successivo backup differenziale, eseguire il backup del database **master** .  
  
 In caso di perdita del database **master** , ripristinarlo prima dei backup differenziali di un database utente.  
  
 Se si scollega e si collega un database di sola lettura per il quale in seguito si prevede di usare backup differenziali, eseguire non appena possibile un backup completo sia del database di sola lettura che del database **master** .  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Creare un backup differenziale del database &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [Ripristinare un backup differenziale del database &#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica del backup &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Backup completo del database &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [Ripristini di database completi &#40;modello di recupero con registrazione completa&#41;](complete-database-restores-full-recovery-model.md)   
 [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](complete-database-restores-simple-recovery-model.md)   
 [Backup di log delle transazioni &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
