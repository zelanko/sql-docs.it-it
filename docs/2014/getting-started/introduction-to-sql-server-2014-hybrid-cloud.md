---
title: Introduzione al Cloud ibrido SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6dc42752-1fcd-4ab9-8194-c3001ea342e7
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fccd4169245421dd33cb5f41bac85861679de823
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66088614"
---
# <a name="introduction-to-sql-server-2014-hybrid-cloud"></a>Introduzione al cloud ibrido di SQL Server 2014
 L'obiettivo della maggior parte delle applicazioni è affrontare alcuni problemi chiave, quali efficienza elevata, valore aziendale, configurazioni hardware complesse, picchi notevoli su richiesta, nonché conformità a norme aziendali e del settore. Le operazioni necessarie per prendere in considerazione tutti questi fattori e sviluppare una tecnologia aziendale possono risultare molto complesse. La strategia Microsoft di un cloud ibrido intende risolvere questi problemi offrendo il supporto per cloud tradizionali e privati, cloud pubblici e ambienti cloud ibridi. 
 
 Quando l'azienda richiede un'infrastruttura IT flessibile scalabile su richiesta, è possibile creare un cloud privato nel data center o un cloud pubblico in Azure data center globali. Quando si estende il data center per soddisfare le esigenze del cloud pubblico, si compila un modello di cloud ibrido. 
 
 In questo argomento vengono presentate le funzionalità di SQL Server 2014 che supportano scenari di cloud ibrido. Per informazioni dettagliate sulla strategia Microsoft di cloud ibrido e su SQL Server, visitare il sito Web relativo a [soluzioni IT ibride di SQL Server](https://www.microsoft.com/sqlserver/solutions-technologies/hybrid-It.aspx) . 
 
## <a name="sql-server-azure-and-hybrid-cloud"></a>SQL Server, Azure e Cloud ibrido 
 Con le tecnologie Microsoft è possibile eseguire il codice sia in locale sia nel cloud, effettuare esecuzioni nel cloud utilizzando i dati locali oppure esecuzioni interamente nel cloud utilizzando più data center. Di conseguenza, è possibile spostare le applicazioni in uso nel cloud quando lo si ritiene opportuno, preservando, nel contempo, il valore degli investimenti in soluzioni IT legacy esistenti. 
 
 In questo articolo ci concentreremo sugli scenari di cloud ibrido che spaziano da on-premises SQL Server per le offerte di cloud pubblico di Azure: [SQL Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/azure/jj823132.aspx) e [risorsa di archiviazione Azure](http://www.azure.com/documentation/services/storage/). In particolare, si parlerà gli scenari seguenti: 
 
-  [Backup e ripristino di database da e verso archiviazione di Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#backup) 
 
-  [Gestire repliche di Database in macchine virtuali di Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#replica) 
 
-  [Store il file di dati SQL Server in archiviazione di Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#store) 
 
-  [Eseguire la migrazione di database di SQL Server esistenti a macchine virtuali di Azure](../../2014/getting-started/introduction-to-sql-server-2014-hybrid-cloud.md#migrate) 
 
### <a name="hybrid-cloud-scenarios-for-sql-server-and-microsoft-azure"></a>Scenari Cloud ibridi per SQL Server e Microsoft Azure 
 
#### <a name="backup"></a> Backup e ripristino di database da e verso archiviazione di Azure 
 Una delle attività amministrative più importanti è rappresentata dal backup e ripristino dei database. Con SQL Server e Azure, puoi eseguire il backup in modo sicuro i database nel cloud. 
 
 I principali vantaggi dell'uso di funzionalità di backup e ripristino di SQL Server con archiviazione di Azure come destinazione di backup includono: 
 
-  Archiviazione senza limiti a costo contenuto 
 
-  Archiviazione a disponibilità elevata (con replica in località geografiche per evitare perdite di dati) 
 
-  Archiviazione in una posizione esterna in grado di supportare ripristini di emergenza e requisiti di conformità 
 
-  Processo di backup e ripristino remoto semplificato 
 
 Di seguito è riportato un elenco delle funzionalità di backup e ripristino di SQL Server per scenari locali e di cloud: 
 
-  Il [SQL Server Backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) funzionalità consente di eseguire il backup in archiviazione di Azure specificando l'URL come destinazione di backup. Grazie a questa funzionalità, è possibile eseguire un backup manuale o configurare la propria strategia di backup allo stesso modo di una risorsa di archiviazione locale o di altre soluzioni esterne. 
 
-  Il [crittografia dei Backup](../relational-databases/backup-restore/backup-encryption.md) funzionalità consente di crittografare i dati durante la creazione di un backup per le destinazioni di archiviazione: da sito locale e archiviazione di Azure. 
 
-  Il [compressione dei Backup (SQL Server)](../relational-databases/backup-restore/backup-compression-sql-server.md) funzionalità consente di creare un backup, che è minore di un backup non compresso degli stessi dati. La compressione di un backup richiede una minore quantità di I/O del dispositivo e pertanto la velocità del backup aumenta in genere in modo significativo. Ciò può comportare notevoli vantaggi quando si archiviano i file di backup in archiviazione di Azure. 
 
-  Il [SQL Server Managed Backup to Azure](https://msdn.microsoft.com/library/dn606152(v=sql.120).aspx) funzionalità consente automaticamente il backup nei database di SQL Server per [archiviazione di Azure](http://www.azure.com/documentation/services/storage/). Grazie a questa funzionalità, è possibile configurare SQL Server in modo da gestire la strategia di backup e pianificare i backup per un singolo database o più database oppure impostare i valori predefiniti a livello di istanza. 
 
-  Il [Backup di SQL Server per lo strumento Azure](https://www.microsoft.com/download/details.aspx?id=40740) Abilita backup in archiviazione Blob di Azure e crittografare e comprimere i backup di SQL Server archiviati in locale o nel cloud. Tramite questo strumento viene abilitata una singola strategia di backup nel cloud in diverse versioni di SQL Server, ad esempio SQL Server 2005, 2008, 2008 R2 e 2014. 
 
#### <a name="replica"></a> Gestire repliche di Database in macchine virtuali di Azure 
 Una soluzione di ripristino di emergenza stabile per i database è essenziale per il successo dell'azienda. La maggior parte dei clienti deve configurare un sito per i ripristini di emergenza e acquistare dell'hardware aggiuntivo per le repliche di database. Con SQL Server e Azure, è possibile mantenere una o più repliche dei database nel cloud. 
 
 Vantaggi principali di gestione di repliche secondarie in Azure includono: 
 
-  Soluzione di ripristino di emergenza a costo contenuto 
 
-  Failover trasparente dell'applicazione 
 
-  Repliche disponibili per la ripartizione di carichi di lavoro di lettura e backup 
 
 Si possono mantenere repliche secondarie in Azure usando una delle tecniche seguenti: 
 
-  Il [Aggiungi Replica Azure](https://msdn.microsoft.com/library/dn463980\(v=sql.120\).aspx) consente di distribuire uno o più repliche dei database in una macchina virtuale in Azure per il ripristino di emergenza. 
 
-  Gruppi di disponibilità AlwaysOn, mirroring del database e log shipping sono le tecnologie più comuni che è possibile usare per risolvere la disponibilità elevata dell'applicazione e che necessita il ripristino di emergenza. Per informazioni, vedere [disponibilità elevata e ripristino di emergenza per SQL Server in macchine virtuali Azure](https://msdn.microsoft.com/library/azure/jj870962.aspx). 
 
#### <a name="store"></a> Store il file di dati SQL Server in archiviazione di Azure 
 L'archiviazione file di dati di SQL Server locali in archiviazione di Azure offre un'archiviazione di una posizione esterna flessibile, affidabile e illimitata per i database. A partire da SQL Server 2014, è possibile usare [file di dati di SQL Server in Miceosoft Azure](https://docs.microsoft.com/sql/relational-databases/databases/sql-server-data-files-in-microsoft-azure) per archiviare i file di database di SQL Server in archiviazione di Azure. Con questa funzionalità, è possibile spostare i dati e file di log dal database locale in archiviazione di Azure, mantenendo il nodo di calcolo di SQL Server in esecuzione in locale. Questa funzionalità consente di avere la capacità di archiviazione illimitata in archiviazione di Azure. 
 
 I principali vantaggi dell'archiviazione dei file di dati di SQL Server archiviazione di Azure includono: 
 
-  Senza limiti di archiviazione a costo contenuto in archiviazione di Azure 
 
-  Soluzione ottimale per la ripartizione di carichi di lavoro di lettura cronologici nel cloud per supportare applicazioni di creazione di report locali 
 
-  Semplificazione del ripristino di emergenza tramite separazione dell'istanza di calcolo (un'istanza di SQL Server) e dei dati (file di dati di SQL Server). In questo modo è possibile collegare facilmente il database in un'altra istanza di SQL Server in un ambiente locale o in una macchina virtuale di Azure in caso di emergenza. 
 
#### <a name="migrate"></a> Eseguire la migrazione di database di SQL Server esistenti a macchine virtuali di Azure 
 Il cloud computing offre alcuni vantaggi chiave alle organizzazioni, ad esempio risorse virtualizzate senza limiti disponibili con addebito in base all'utilizzo. È infatti possibile utilizzare i data center del cloud disponibili pubblicamente anziché compilare e gestire data center di proprietà; di conseguenza, è possibile ridurre i costi di hardware e di soluzioni IT. 
 
 Con [SQL Server in macchine virtuali Azure](https://msdn.microsoft.com/library/azure/jj823132.aspx), è possibile spostare le applicazioni locali esistenti in Azure con il minimo o nessuna modifica al codice. Gli amministratori e gli sviluppatori possono comunque utilizzare gli stessi strumenti di sviluppo e amministrazione disponibili in locale. 
 
 Spostare un database da un'istanza locale di SQL Server in SQL Server in esecuzione in una macchina virtuale di Azure in genere ha uno di questi percorsi: 
 
-  **Spostamento solo del database:** Esistono diversi strumenti e tecniche disponibili per spostare i database locali esistenti in SQL Server in macchine virtuali di Azure. Per linee guida e consigli sulla migrazione a SQL Server in macchine virtuali di Azure, vedere [preparazione della migrazione a SQL Server in macchine virtuali di Azure](https://msdn.microsoft.com/library/dn133142.aspx) nonché [migrazione a SQL Server in una macchina virtuale di Azure ](https://msdn.microsoft.com/library/jj156165.aspx). 
 
   Inoltre, a partire da SQL Server 2014, una nuova procedura guidata [distribuire un Database di SQL Server a una macchina virtuale di Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md) è disponibile per la distribuzione del database in un'altra istanza di SQL Server in esecuzione in una macchina virtuale di Azure. 
 
-  **Lo spostamento dell'intera macchina virtuale:** È possibile trasferire le proprie macchine virtuali di SQL Server in Azure o crearne uno usando l'immagine della piattaforma. È quindi possibile caricare e collegare un disco di dati in cui sono già contenuti dati alla macchina virtuale oppure collegare un disco vuoto alla macchina. Con un'istanza di dati di SQL Server in macchine virtuali con dischi dati collegati fornisce un altro archivio permanente per i file di dati e i dati dell'applicazione. Per informazioni complete e procedure dettagliate, vedere [distribuzione di SQL Server in macchine virtuali Azure](https://msdn.microsoft.com/library/dn133141.aspx). 
 
 Se si prevede di spostare i livelli applicazione (ad esempio il livello di presentazione, il livello business e il livello di database) per le macchine virtuali di Azure, è consigliabile esaminare i consigli forniti nel [sviluppo e i modelli di applicazione Strategie per SQL Server in macchine virtuali Azure](https://msdn.microsoft.com/library/dn574746.aspx) articolo. L'obiettivo di questo articolo è fornire agli sviluppatori e architetti di soluzioni una base per la progettazione, che potranno seguire nella migrazione delle applicazioni esistenti in Azure, nonché sviluppano nuove applicazioni in Azure e architettura efficace delle applicazioni. Per ogni criterio applicazione, nell'articolo viene descritto uno scenario locale, la rispettiva soluzione cloud e i consigli tecnici correlati. L'articolo discute inoltre strategie di sviluppo specifiche di Azure in modo che è possibile progettare correttamente le applicazioni. 
 
## <a name="see-also"></a>Vedere anche 
 [Guida di SQL Server 2014 CTP2](https://www.microsoft.com/download/details.aspx?id=39269)  
 [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx)  
 [Serie di Blog di Cloud ibrido di Microsoft SQL Server](https://azure.microsoft.com/blog/microsoft-sql-server-hybrid-cloud-blog-series/)  
 [Migrazione di applicazioni incentrate sui dati in Azure](https://azure.microsoft.com/blog/cloud-services-series-migrating-data-centric-applications-to-windows-azure/) 
 
 
