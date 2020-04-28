---
title: SQL Server backup e ripristino con il servizio di archiviazione BLOB di Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38c92e397c971f6e9976bb857c63410fa60b7e85
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75232426"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>Backup e ripristino di SQL Server con il servizio Archiviazione BLOB di Azure
  Questo argomento introduce [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i backup e il ripristino dal [servizio di archiviazione BLOB di Azure](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/). Fornisce inoltre un riepilogo dei vantaggi derivanti dall'uso del servizio BLOB di Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per archiviare i backup.  
  
 SQL Server supporta l'archiviazione dei backup nel servizio di archiviazione BLOB di Azure nei modi seguenti:  
  
-   **Gestire i backup in Azure:** Usando gli stessi metodi usati per eseguire il backup su disco e nastro, è ora possibile eseguire il backup in archiviazione di Azure specificando l'URL come destinazione di backup.  È possibile utilizzare questa funzionalità per eseguire il backup manualmente o per configurare la propria strategia di backup allo stesso modo di una risorsa di archiviazione locale o di altre soluzioni esterne. Questa funzionalità viene definita anche **Backup di SQL Server nell'URL**. Per altre informazioni, vedere [SQL Server Backup to URL](sql-server-backup-to-url.md). Questa funzionalità è disponibile in SQL Server 2012 SP1 CU2 o versione successiva.  
  
    > [!NOTE]  
    >  Per SQL Server versioni precedenti a SQL Server 2014, è possibile usare il componente aggiuntivo SQL Server il backup in Azure per creare rapidamente e facilmente i backup in archiviazione di Azure. Per ulteriori informazioni, vedere l' [Area download](https://go.microsoft.com/fwlink/?LinkID=324399).  
  
-   **Consente di SQL Server gestire i backup in Azure:** Configurare SQL Server per gestire la strategia di backup e pianificare i backup per un singolo database o più database oppure impostare i valori predefiniti a livello di istanza. Questa funzionalità viene definita **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]**. Per altre informazioni, vedere [SQL Server backup gestito in Azure](sql-server-managed-backup-to-microsoft-azure.md). Questa funzionalità è disponibile in SQL Server 2014 o versione successiva.  
  
## <a name="benefits-of-using-the-azure-blob-service-for-ssnoversion-backups"></a>Vantaggi dell'uso del servizio BLOB di Azure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i backup  
  
-   Archiviazione fuori sede flessibile, affidabile e illimitata: l'archiviazione dei backup nel servizio BLOB di Azure può essere un'opzione esterna pratica, flessibile e di facile accesso. La creazione dell'archiviazione in una posizione esterna per i backup di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere semplice quanto la modifica degli script o dei processi esistenti. Generalmente, l'archiviazione in una posizione esterna deve essere sufficientemente lontana dalla posizione del database di produzione per impedire che una singola situazione di emergenza possa influire sia sulla posizione esterna sia su quella del database di produzione. Scegliendo la replica a livello geografico dell'archiviazione BLOB si dispone di un ulteriore livello di protezione in caso di evento di emergenza che potrebbe influire sull'intera area. Inoltre, i backup sono disponibili sempre e in qualsiasi punto e possono essere facilmente utilizzati per i ripristini.  
  
-   Archivio di backup: il servizio di archiviazione BLOB di Azure offre un'alternativa migliore rispetto all'opzione Tape spesso usata per archiviare i backup. L'archiviazione su nastro può richiedere il trasporto fisico alla struttura fuori sede e l'adozione di determinate misure per la protezione dei supporti. L'archiviazione dei backup nell'archiviazione BLOB di Azure rappresenta un'opzione di archiviazione istantanea, estremamente disponibile e durevole.  
  
-   Nessun overhead di gestione dell'hardware: non è previsto alcun sovraccarico di gestione hardware con i servizi di Azure. I servizi di Azure consentono di gestire l'hardware con l'aggiunta della replica geografica per la ridondanza e la protezione dagli errori hardware.  
  
-   Attualmente, per le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanze di in esecuzione in una macchina virtuale di Azure, il backup nei servizi di archiviazione BLOB di Azure può essere eseguito creando dischi collegati. Tuttavia, esiste un limite al numero di dischi che è possibile connettersi a una macchina virtuale di Azure. vale a dire 16 per un'istanza di dimensioni elevate e un po' di meno per istanze di dimensioni inferiori. Abilitando un backup diretto nell'archiviazione BLOB di Azure, è possibile ignorare il limite di 16 dischi.  
  
     Inoltre, il file di backup che ora è archiviato nel servizio di archiviazione BLOB di Azure è direttamente disponibile in un'istanza locale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o in un' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] altra in esecuzione in una macchina virtuale di Azure, senza la necessità di collegamento/scollegamento del database o di scaricare e connettere il disco rigido virtuale.  
  
-   Vantaggi economici: si paga solo il servizio utilizzato. Può rivelarsi una soluzione economica per il backup e l'archiviazione fuori sede. Per ulteriori informazioni e collegamenti, vedere la sezione [considerazioni sulla fatturazione di Azure](#Billing) .  
  
##  <a name="azure-billing-considerations"></a><a name="Billing"></a>Considerazioni sulla fatturazione di Azure:  
 Conoscere i costi di archiviazione di Azure consente di prevedere il costo della creazione e dell'archiviazione dei backup in Azure.  
  
 Il [calcolatore dei prezzi di Azure](https://go.microsoft.com/fwlink/?LinkId=277060) può aiutare a stimare i costi.  
  
 **Archiviazione:** i costi dipendono dallo spazio utilizzato e vengono calcolati in base a una scala graduata e al livello di ridondanza. Per altri dettagli e informazioni aggiornate, vedere la sezione sulla **gestione dei dati** nell'articolo [Dettagli prezzi](https://go.microsoft.com/fwlink/?LinkId=277059) .  
  
 **Trasferimenti di dati:** I trasferimenti di dati in ingresso in Azure sono gratuiti. Per i trasferimenti in uscita viene addebitato il costo relativo all'utilizzo della larghezza di banda e il calcolo viene effettuato in base a una scala graduata specifica per l'area. Per ulteriori informazioni, vedere la sezione [Trasferimenti di dati](https://go.microsoft.com/fwlink/?LinkId=277061) nell'articolo Dettagli prezzi.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure consigliate e risoluzione dei problemi per il backup di SQL Server nell'URL](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Backup e ripristino di database di sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Esercitazione: SQL Server backup e ripristino nel servizio di archiviazione BLOB di Azure](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [Backup di SQL Server nell'URL](sql-server-backup-to-url.md)  
  
