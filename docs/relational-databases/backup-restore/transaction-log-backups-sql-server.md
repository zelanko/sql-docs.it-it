---
title: Backup di log delle transazioni [SQL Server] | Microsoft Docs
description: Indipendentemente dai backup di database, è possibile eseguire il backup del log delle transazioni di SQL Server di frequente. La sequenza dei backup del log delle transazioni è una catena di log.
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b4cbba5a13a41d9f24901d348566c4c09234060f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180441"
---
# <a name="transaction-log-backups-sql-server"></a>Backup di log delle transazioni (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le informazioni contenute in questo argomento sono rilevanti solo per i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che utilizzano i modelli di recupero con registrazione completa o con registrazione minima delle operazioni bulk. In questo argomento viene illustrata l'esecuzione del backup del log delle transazioni di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per poter creare backup dei log è necessario aver creato almeno un backup completo. A quel punto, è possibile eseguire il backup del log delle transazioni in qualsiasi momento a meno che non sia già stato eseguito. 
 
È consigliabile eseguire backup del log spesso, sia per ridurre al minimo il rischio di perdita dei dati sia per consentire il troncamento del log. 
 
In genere, un amministratore del database crea un backup completo occasionale del database, ad esempio con cadenza settimanale ed eventualmente crea una serie di backup differenziali a intervalli più brevi, ad esempio giornalmente. Indipendentemente dai backup di database, l'amministratore esegue il backup del log delle transazioni a intervalli frequenti. L'intervallo ottimale per un determinato tipo di backup dipende da fattori quali l'importanza dei dati, le dimensioni del database e il carico di lavoro del server. Per altre informazioni sull'implementazione di una buona strategia, vedere [Indicazioni](#Recommendations) in questo argomento. 
   
##  <a name="how-a-sequence-of-log-backups-works"></a><a name="LogBackupSequence"></a> Modalità di funzionamento di una sequenza di backup del log  
 La sequenza della *catena di log* dei backup del log delle transazioni è indipendente dai backup dei dati. Si consideri ad esempio la sequenza di eventi seguente:  
  
|Tempo|Event|  
|----------|-----------|  
|8\.00|Backup del database|  
|12.00|Backup del log delle transazioni|  
|16.00|Backup del log delle transazioni|  
|18.00|Backup del database|  
|20.00|Backup del log delle transazioni|  
  
 Il backup del log delle transazioni creato alle 20.00 contiene i record del log delle transazioni compresi tra le 16.00 e le 20.00, includendo l'ora di creazione del backup completo del database (18.00). La sequenza di backup del log delle transazioni è continua, dal primo backup completo del database creato alle 8.00 fino all'ultimo backup del log delle transazioni creato alle 20.00. Per informazioni su come applicare i backup del log, vedere l'esempio in [Applicare backup log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   Se un log delle transazioni è danneggiato, il lavoro eseguito dopo il backup valido più recente viene perso. Pertanto è consigliabile inserire i file di log in una risorsa di archiviazione con tolleranza di errore.  
  
-   Se un database è danneggiato oppure deve essere ripristinato, è consigliabile creare un [backup della parte finale del log](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) per consentire il ripristino del database al momento corrente.  
  
-   Per impostazione predefinita, per ogni operazione di backup eseguita in modo corretto viene aggiunta una voce al log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e al registro eventi di sistema. Se il backup del log viene eseguito di frequente, questi messaggi possono aumentare rapidamente, provocando la creazione di log degli errori di dimensioni elevate e rendendo difficile l'individuazione di altri messaggi. In questi casi è possibile eliminare tali voci di log utilizzando il flag di traccia 3226 se nessuno degli script dipende da esse. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  

-   Eseguire backup del log abbastanza frequenti da soddisfare i requisiti aziendali e in particolare il requisito di tolleranza per eventuali perdite di dati, che potrebbero ad esempio verificarsi in seguito al danneggiamento della risorsa di archiviazione dei log. 
   -   La frequenza appropriata per l'esecuzione dei backup del log viene determinata in base al raggiungimento di un compromesso tra la tolleranza per il rischio di perdita dei dati e la quantità di backup del log che è possibile archiviare, gestire e potenzialmente ripristinare. Considerare gli obiettivi [RTO](https://wikipedia.org/wiki/Recovery_time_objective) e [RPO](https://wikipedia.org/wiki/Recovery_point_objective) richiesti quando si implementa la strategia di ripristino, in particolare la frequenza di backup del log.
   -   Potrebbe essere sufficiente eseguire un backup del log ogni 15 - 30 minuti. Se nella propria azienda è necessario limitare al minimo il rischio di perdita dei dati, valutare se eseguire i backup del log con una maggiore frequenza. L'esecuzione di backup del log più frequenti offre il vantaggio aggiuntivo di un aumento della frequenza del troncamento del log, con una conseguente riduzione delle dimensioni dei file di log.  
  
> [!IMPORTANT]
> Per limitare il numero di backup dei log che è necessario ripristinare, è fondamentale eseguire regolarmente il backup dei dati. Ad esempio, è possibile pianificare un backup completo del database una volta la settima e backup differenziali del database una volta al giorno.  
> Anche in questo caso considerare gli obiettivi [RTO](https://wikipedia.org/wiki/Recovery_time_objective) e [RPO](https://wikipedia.org/wiki/Recovery_point_objective) richiesti quando si implementa la strategia di ripristino, in particolare la frequenza del backup completo e differenziale del database.
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per creare un backup del log delle transazioni**  
  
-   [Eseguire il backup di un log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 Per pianificare i processi di backup, vedere [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).  
  

## <a name="see-also"></a>Vedere anche  
 [Log delle transazioni &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Backup del log delle transazioni nella Guida sull'architettura e gestione del log delle transazioni in SQL Server](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [Backup e ripristino di database SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Backup della parte finale del log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [Applicare backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
