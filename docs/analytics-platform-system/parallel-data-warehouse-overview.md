---
title: I componenti Data Warehouse - sistema di piattaforma Analitica in parallelo | Microsoft Docs
description: Questo articolo illustra il software di appliance e i componenti software non appliance del sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 87525a741c1d0081b366394c0c5dd1b152ad15f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960470"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>I componenti Data Warehouse - sistema di piattaforma Analitica in parallelo
Questo articolo illustra il software di appliance e i componenti software non appliance del sistema di piattaforma Analitica.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Software di Data Warehouse in parallelo](media/parallel-data-warehouse-software.png "software Parallel Data Warehouse")  
  
## <a name="sec1"></a>Appliance Software - Query di elaborazione ed archiviazione dati utente  
  
### <a name="control-node"></a>Nodo di controllo  
Motore MPP  
Il motore MPP è il meccanismo alla base del sistema Massively Parallel Processing (MPP). Esegue le operazioni seguenti:  
  
-   Crea piani di query parallele e coordina l'esecuzione di query parallele sui nodi di calcolo.  
  
-   Archivia e coordina i metadati e dati di configurazione per tutti i database.  
  
-   Gestisce l'autorizzazione e l'autenticazione del database SQL Server PDW.  
  
-   Tiene traccia dello stato di hardware e software.  
  
### <a name="data-movement-service-dms"></a>Data Movement Service (DMS)  
Data Movement Service (DMS) fa parte il "segreto" di PDW. Esegue le operazioni seguenti:  
  
-   Trasferisce i dati da e verso i nodi di SQL Server PDW.  
  
-   Processi operazioni che richiedono il trasferimento dei dati tra i nodi di query.  
  
-   Migliora le prestazioni delle query, ottimizzando la velocità di trasferimento dei dati.  
  
### <a name="admin-console"></a>Console di amministrazione  
La Console di amministrazione è un'applicazione web che presenta la stato dello strumento, l'integrità e le informazioni sulle prestazioni.  
  
### <a name="configuration-manager"></a>Gestione configurazione  
Configuration Manager (dwconfig.exe), è lo strumento che appliance agli amministratori di configurare il sistema di piattaforma Analitica.  
  
### <a name="control-node-databases"></a>Database di nodo di controllo  
SQL Server gestisce tutti i database nel nodo di controllo.  
  
-   Lo scheletro di database gestisce i metadati per tutti i database utente distribuita.  
  
-   Database TempDB contiene i metadati per tutte le tabelle temporanee utente attraverso l'appliance.  
  
-   Master è la tabella master di SQL Server nel nodo di controllo.  
  
### <a name="compute-node"></a>Nodo di calcolo  
I nodi di calcolo sono elaborazione parallela dei dati e le unità di archiviazione. Essi hanno archiviazione collegata direttamente e utilizzare SQL Server per gestire i dati utente.  
  
### <a name="data-movement-service-dms"></a>Data Movement Service (DMS)  
Data Movement Service (DMS) in esecuzione in ogni nodo di calcolo per eseguire le operazioni seguenti:  
  
-   Come parte dell'elaborazione di query parallele, DMS trasferire i dati da e verso altri nodi di Computer e il nodo di controllo.  
  
-   Servizio migrazione del database, in esecuzione in ogni nodo di calcolo, riceve i caricamenti di dati in parallelo. I dati vengono caricati in parallelo direttamente dal server di caricamento per i nodi di calcolo  
  
-   Servizio migrazione del database trasferisce i dati da ogni nodo di calcolo direttamente al server di backup.  
  
-   Usando PolyBase, DMS trasferisce i dati da e verso un cluster Hadoop esterno o un archivio Blob di Azure.  
  
### <a name="compute-node-databases"></a>I database di nodo di calcolo 
Ogni nodo di calcolo viene eseguito un'istanza di SQL Server per elaborare query e gestire i dati utente.  
  
## <a name="appliance-fabric"></a>Infrastruttura di Appliance  
L'infrastruttura di appliance fornisce il sistema operativo, servizi e infrastruttura di rete per l'appliance.  
  
### <a name="domain-controller"></a>Controller di dominio  
Active Directory (AD) Domain Services (DS)  
Sistema di piattaforma Analitica esegue l'autenticazione tra i nodi del sistema di piattaforma Analitica e gestisce l'autenticazione di accesso con autenticazione di Windows di SQL Server PDW.  
  
Servizio DNS  
Windows del servizio DNS (Domain Name) risolve i nomi di dominio in indirizzi IP per l'appliance del sistema di piattaforma Analitica.  
  
### <a name="windows-deployment-service"></a>Servizi di distribuzione Windows  
Servizio di distribuzione Windows (WDS) consente di distribuire il sistema operativo Windows Server nell'appliance. In ogni host e macchina virtuale viene distribuita nell'intera appliance.  
  
Il servizio DHCP consente di creare gli indirizzi IP in modo che gli host all'interno del dominio appliance possono accedere alla rete appliance senza la necessità di un indirizzo IP configurato in precedenza.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Sistema di piattaforma Analitica utilizza la virtualizzazione per ottenere disponibilità elevata. Il Virtual Machine Manager ospita System Center per distribuire il sistema operativo negli host fisici.  
  
Windows Server Update Services (WSUS) per applicare o rimuovere gli aggiornamenti di Windows in tutti gli host e macchine virtuali.  
  
### <a name="windows-server"></a>Windows Server  
Tutti gli host e macchine virtuali nell'appliance eseguiti sistema operativo Windows Server.  
  
### <a name="failover-clustering"></a>Clustering di failover  
Clustering di Failover di Windows offre la possibilità di riavviare i processi in un host passivo nel caso in cui si verifica un errore di un host.  
  
### <a name="storage-spaces"></a>Spazi di archiviazione  
Spazi di archiviazione Windows gestisce i dati utente come un pool di archiviazione per un piccolo gruppo di nodi di calcolo. Se un nodo di calcolo non riesce, i dati sono ancora accessibili tramite un altro nodo di calcolo nel gruppo.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server offre una soluzione di virtualizzazione affidabile e semplice. Sistema di piattaforma Analitica Usa virtualizzazione: per bilanciare le risorse di CPU e per fornire disponibilità elevata per i nodi PDW e appliance componenti dell'infrastruttura.  
  
## <a name="sec2"></a>Dati non relazionali
La tecnologia PolyBase si integra i dati pwd di SQL Server con dati Hadoop esterne. I dati di Hadoop possono essere archiviati in uno qualsiasi di queste origini dati di Hadoop:  
  
-   Distribuzione di Hadoop di Hortonworks  
  
-   Cloudera distribuzione di Hadoop  
  
-   Dati archiviati in archivio Blob di Azure in HDInsight  
  
## <a name="query-tools"></a>Strumenti di query   
  
Le query sono scritte con Transact\-SQL modificati a seconda della natura MPP delle query. Tutte le query vengono inviate al nodo di controllo, che genera un piano di query in parallelo per eseguire query tra più nodi di calcolo.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools viene eseguito all'interno di Visual Studio ed è nostro strumento GUI consigliato per l'invio di query in SQL Server PDW. È simile a SQL Server Management Studio, consentendo di passare tramite Esplora oggetti.  
  
Se non si dispone già di Visual Studio, è possibile scaricare gli strumenti che è necessario gratuitamente. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Strumento di Query della riga di comando SQLCMD  
SQLCMD è lo strumento da riga di comando di SQL Server per l'esecuzione di Transact\-SQL istruzioni e i comandi del sistema. Funziona con SQL Server PDW ed è nostro strumento da riga di comando consigliato per l'esecuzione di query SQL Server PDW. Con sqlcmd è possibile eseguire Transact\-istruzioni SQL in modo interattivo dalla riga di comando, come un file batch o da Windows PowerShell.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
È possibile utilizzare Integration Services per eseguire query SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Server collegato  
Usando una connessione del server collegato di SQL Server, è possibile usare SQL Server per inviare Transact\-istruzioni SQL in SQL Server PDW. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Strumenti di Business Intelligence
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW è un'origine dati valida per i modelli di PowerPivot per Excel e database di Analysis Services. Usa il provider OLE DB, è possibile configurare un cubo di Analysis Services per usare elaborazione analitica in linea multidimensionale (MOLAP) o l'archiviazione relazionale OLAP (ROLAP).  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Generatore report  
È possibile usare SQL Server PDW come origine dati SQL Server per i report che si sviluppano per Reporting Services usando Generatore Report di SQL Server. È anche possibile usare SQL Server PDW come origine di SQL Server per i modelli di report. Utilizzando Gestione Report o l'API del server di report, è possibile generare un modello da un database di SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot per Excel  
È possibile connettersi a SQL Server PDW con PowerPivot per Excel, un download gratuito che consente di espandere in modo significativo le funzionalità di analisi dei dati di Excel.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Strumenti di caricamento 
  
### <a name="integration-services"></a>Integration Services  
Installare gli adapter di destinazione PDW specifici che consentono di usare servizi ServerIntegration SQL per caricare i dati in SQL Server PDW.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Caricatore della riga di comando dwloader  
dwloader è uno strumento di caricamento della riga di comando che carica i dati in parallelo dal server di caricamento per i nodi di calcolo di SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase per l'integrazione di Hadoop  
Con la tecnologia PolyBase, è possibile caricare i dati non relazionali da un Hadoop Cluster in una tabella relazionale di SQL Server PDW. I dati di Hadoop possono trovarsi in un Hadoop Cluster esterno o in un archivio Blob di Azure.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Ripristino e Backup del database  
SQL Server PDW Usa backup di database Transact-SQL e ripristinare i comandi backup e ripristino dei database utente, in parallelo, da e verso un server di backup. SQL Server PDW scrive il backup in una directory in una condivisione file di Windows e quindi ripristinare in modo analogo i dati da una condivisione file di Windows.  
  
Per altre informazioni, vedere [pianificare per il Backup e il caricamento di Hardware](backup-and-loading-hardware.md) e [Panoramica di Backup e ripristino](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Copia della tabella remota  
La funzionalità di copia della tabella remota consente di copiare tabelle da database di SQL Server PDW a database di SQL Server SMP remoti (non appliance). Questo consente scenari di hub e spoke per SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Monitoraggio  
Sistema di piattaforma Analitica ha diversi modi per monitorare l'attività di appliance  
  
### <a name="admin-console"></a>Console di amministrazione  
La Console di amministrazione consente di visualizzare lo stato corrente sull'integrità appliance. Ciò viene eseguito come un'applicazione web nel nodo di controllo ed è accessibile tramite https.  
  
Per altre informazioni, vedere [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Viste di sistema  
La Console di amministrazione è basata sulle query di vista di sistema. È possibile eseguire query di viste di sistema per ottenere la parte specifica di informazioni che necessarie.  

Per altre informazioni, vedere [monitorare l'Appliance usando le viste di sistema &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Sono presenti System Center Operations Manager (SCOM) Management Pack per SQL Server PDW. 

Per configurare l'appliance per SCOM, vedere [monitorare l'Appliance tramite System Center Operations Manager &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
