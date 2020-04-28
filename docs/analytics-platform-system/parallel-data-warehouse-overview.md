---
title: Componenti data warehouse paralleli
description: Questo articolo illustra il software del dispositivo e i componenti software non appliance del sistema di piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400937"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>Componenti data warehouse paralleli-sistema della piattaforma Analytics
Questo articolo illustra il software del dispositivo e i componenti software non appliance del sistema di piattaforma di analisi.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Software data warehouse parallelo](media/parallel-data-warehouse-software.png "Software data warehouse parallelo")  
  
## <a name="appliance-software---query-processing-and-user-data-storage"></a><a name="sec1"></a>Software appliance-elaborazione query e archiviazione dati utente  
  
### <a name="control-node"></a>nodo di controllo  
Motore MPP  
Il motore MPP è il cervello del sistema MPP (Massive Parallel Processing). Esegue le operazioni seguenti:  
  
-   Crea piani di query paralleli e coordina l'esecuzione di query parallele nei nodi di calcolo.  
  
-   Archivia e coordina i metadati e i dati di configurazione per tutti i database.  
  
-   Gestisce SQL Server PDW l'autenticazione e l'autorizzazione del database.  
  
-   Tiene traccia dello stato dell'hardware e del software.  
  
### <a name="data-movement-service-dms"></a>Servizio di spostamento dati (DMS)  
Il servizio di spostamento dei dati (DMS) fa parte della "salsa segreta" di PDW. Esegue le operazioni seguenti:  
  
-   Trasferisce i dati da e verso i nodi del SQL Server PDW.  
  
-   Elabora le operazioni di query che richiedono il trasferimento dei dati tra i nodi.  
  
-   Migliora le prestazioni delle query ottimizzando le velocità di trasferimento dei dati.  
  
### <a name="admin-console"></a>Console di amministrazione  
La console di amministrazione è un'applicazione Web che presenta le informazioni sullo stato, l'integrità e le prestazioni dell'appliance.  
  
### <a name="configuration-manager"></a>Configuration Manager  
Il Configuration Manager (dwconfig. exe) è lo strumento usato dagli amministratori di appliance per configurare il sistema di piattaforma di analisi.  
  
### <a name="control-node-databases"></a>Database del nodo di controllo  
SQL Server gestisce tutti i database nel nodo di controllo.  
  
-   Il database della shell gestisce i metadati per tutti i database utente distribuiti.  
  
-   TempDB contiene i metadati per tutte le tabelle temporanee utente nell'appliance.  
  
-   Master è la tabella master per SQL Server nel nodo di controllo.  
  
### <a name="compute-node"></a>Nodo di calcolo  
I nodi di calcolo sono unità di archiviazione e di elaborazione parallela dei dati. Hanno un archivio collegato diretto e usano SQL Server per gestire i dati utente.  
  
### <a name="data-movement-service-dms"></a>Servizio di spostamento dati (DMS)  
Il servizio di spostamento dei dati (DMS) viene eseguito in ogni nodo di calcolo per eseguire le operazioni seguenti:  
  
-   Come parte dell'elaborazione di query parallele, il DMS trasferisce i dati da e verso altri nodi del computer e il nodo di controllo.  
  
-   DMS, in esecuzione in ogni nodo di calcolo, riceve i caricamenti dei dati in parallelo. I dati vengono caricati in parallelo direttamente dal server di caricamento ai nodi di calcolo  
  
-   DMS trasferisce i dati da ogni nodo di calcolo direttamente al server di backup.  
  
-   Con la polibase, DMS trasferisce i dati da e verso un cluster Hadoop esterno o BLOB del servizio di archiviazione di Azure.  
  
### <a name="compute-node-databases"></a>Database dei nodi di calcolo 
Ogni nodo di calcolo esegue un'istanza di SQL Server per elaborare le query e gestire i dati utente.  
  
## <a name="appliance-fabric"></a>Infrastruttura Appliance  
Appliance Fabric fornisce il sistema operativo, i servizi e l'infrastruttura di rete per il dispositivo.  
  
### <a name="domain-controller"></a>Controller di dominio  
Servizi di dominio Active Directory (AD) (DS)  
Analytics Platform System esegue l'autenticazione tra i nodi di sistema della piattaforma di analisi e gestisce l'autenticazione di SQL Server PDW account di accesso con autenticazione di Windows.  
  
Servizio DNS  
Windows Domain Name Service (DNS) risolve i nomi di dominio in indirizzi IP per l'appliance del sistema della piattaforma di analisi.  
  
### <a name="windows-deployment-service"></a>Servizio di distribuzione Windows  
Il servizio di distribuzione Windows (WDS) distribuisce il sistema operativo Windows Server nell'appliance. Viene distribuito in ogni host e macchina virtuale nell'appliance.  
  
Il servizio DHCP crea indirizzi IP in modo che gli host all'interno del dominio Appliance possano partecipare alla rete Appliance senza avere un indirizzo IP preconfigurato.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Il sistema di piattaforma di analisi usa la virtualizzazione per ottenere la disponibilità elevata. Il Virtual Machine Manager ospita System Center per distribuire il sistema operativo negli host fisici.  
  
Windows Server Update Services (WSUS) per applicare o rimuovere gli aggiornamenti di Windows in tutti gli host e le macchine virtuali.  
  
### <a name="windows-server"></a>Windows Server  
Tutti gli host e le macchine virtuali nell'appliance eseguono il sistema operativo Windows Server.  
  
### <a name="failover-clustering"></a>Clustering di failover  
Il clustering di failover di Windows offre la possibilità di riavviare i processi in un host passivo nel caso in cui si verifica un errore in un host.  
  
### <a name="storage-spaces"></a>Spazi di archiviazione  
Spazi di archiviazione Windows gestisce i dati utente come un pool di archiviazione per un piccolo gruppo di nodi di calcolo. Se un nodo di calcolo ha esito negativo, i dati sono ancora accessibili tramite un altro nodo di calcolo nel gruppo.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server offre una soluzione di virtualizzazione semplice e affidabile. Il sistema di piattaforma di analisi usa le virtualizzazione per bilanciare le risorse della CPU e fornire disponibilità elevata per i nodi PDW e i componenti dell'infrastruttura Appliance.  
  
## <a name="non-relational-data"></a><a name="sec2"></a>Dati non relazionali
La tecnologia polibase integra SQL Server PDW dati con dati Hadoop esterni. I dati Hadoop possono essere archiviati in una qualsiasi di queste origini dati Hadoop:  
  
-   Distribuzione Hadoop di Hortonworks  
  
-   Distribuzione Cloudera di Hadoop  
  
-   Dati HDInsight archiviati in BLOB del servizio di archiviazione di Azure  
  
## <a name="query-tools"></a>Strumenti di query   
  
Le query vengono scritte con\-Transact SQL modificato per adattarsi alla natura MPP delle query. Tutte le query vengono inviate al nodo di controllo, che genera un piano di query parallele per eseguire la query nei nodi di calcolo.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools viene eseguito all'interno di Visual Studio ed è lo strumento GUI consigliato per inviare query a SQL Server PDW. È simile a SQL Server Management Studio consentendo di spostarsi in Esplora oggetti.  
  
Se non si dispone già di Visual Studio, è possibile scaricare gli strumenti necessari gratuitamente. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Strumento query della riga di comando sqlcmd  
sqlcmd è lo strumento da riga di comando SQL Server per l'\-esecuzione di istruzioni Transact SQL e comandi di sistema. Funziona con SQL Server PDW ed è lo strumento da riga di comando consigliato per eseguire query SQL Server PDW. Con sqlcmd è possibile eseguire istruzioni\-Transact SQL in modo interattivo dalla riga di comando, come file batch o da Windows PowerShell.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
È possibile utilizzare Integration Services per eseguire query SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Server collegato  
Utilizzando una connessione al server collegato SQL Server, è possibile utilizzare SQL Server per inviare istruzioni\-Transact-SQL al SQL Server PDW. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Strumenti di business intelligence
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW è un'origine dati valida per i database Analysis Services e i modelli PowerPivot di Excel. Utilizzando il provider di OLE DB, è possibile configurare un cubo Analysis Services per utilizzare l'archiviazione MOLAP (Multidimensional Online Analytical Processing (MOLAP) o Online Analytical Processing relazionale (ROLAP).  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Generatore report  
È possibile utilizzare SQL Server PDW come origine dati SQL Server per i report sviluppati per Reporting Services utilizzando SQL Server Generatore report. È inoltre possibile utilizzare SQL Server PDW come origine SQL Server per i modelli di report. Utilizzando Gestione report o l'API del server di report, è possibile generare un modello da un database SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot per Excel  
È possibile connettersi a SQL Server PDW con PowerPivot per Excel, un download gratuito che espande in modo significativo le funzionalità di analisi dei dati di Excel.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Caricamento degli strumenti 
  
### <a name="integration-services"></a>Integration Services  
Installare schede di destinazione specifiche di PDW che consentono di usare i servizi SQL ServerIntegration per caricare i dati in SQL Server PDW.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Caricatore da riga di comando dwloader  
dwloader è uno strumento di caricamento da riga di comando che consente di caricare i dati in parallelo dal server di caricamento ai nodi di calcolo SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>Polibase per l'integrazione con Hadoop  
Con la tecnologia polibase è possibile caricare dati non relazionali da un cluster Hadoop a una tabella relazionale in SQL Server PDW. I dati Hadoop possono trovarsi in un cluster Hadoop esterno o in un BLOB del servizio di archiviazione di Azure.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Backup e ripristino del database  
SQL Server PDW usa i comandi di backup e ripristino del database Transact-SQL per eseguire il backup e il ripristino di database utente, in parallelo, da e verso un server di backup. SQL Server PDW scrive il backup in una directory in una condivisione file di Windows e quindi Ripristina i dati da una condivisione file di Windows.  
  
Per ulteriori informazioni, vedere [pianificare il backup e il caricamento di hardware](backup-and-loading-hardware.md) e [Cenni preliminari su backup e ripristino](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Copia della tabella remota  
La funzionalità di copia della tabella remota consente di copiare tabelle da database SQL Server PDW ai database SQL Server SMP remoti (non Appliance). In questo modo si abilitano gli scenari Hub e spoke per SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Monitoraggio  
Il sistema di piattaforma di analisi offre diversi modi per monitorare l'attività dell'appliance  
  
### <a name="admin-console"></a>Console di amministrazione  
La console di amministrazione consente di visualizzare lo stato corrente dell'integrità dell'appliance. Viene eseguito come applicazione Web nel nodo di controllo ed è accessibile tramite HTTPS.  
  
Per altre informazioni, vedere [monitorare l'appliance usando la console di amministrazione &#40;il sistema di piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Viste di sistema  
La console di amministrazione è basata sulle query di visualizzazione di sistema. È possibile eseguire query sulle viste di sistema singolarmente per ottenere le informazioni specifiche necessarie.  

Per altre informazioni, vedere [monitorare l'appliance usando le viste di sistema &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Sono disponibili System Center Operations Manager Management Pack (SCOM) per SQL Server PDW. 

Per configurare l'appliance per SCOM, vedere [monitorare l'appliance usando System Center Operations Manager &#40;piattaforma di analisi&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
