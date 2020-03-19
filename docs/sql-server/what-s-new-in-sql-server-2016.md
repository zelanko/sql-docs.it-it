---
title: Novità di SQL Server 2016
description: Informazioni sulle nuove funzionalità di sicurezza di SQL Server 2016, sulle funzionalità di query, Hadoop e integrazione cloud, analisi R e altro ancora.
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
keywords:
- novità di sql server
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b0b4a72519a0fa20d0c4a7472760a8f06a9ced32
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2020
ms.locfileid: "79190617"
---
# <a name="whats-new-in-sql-server-2016"></a>Novità di SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]  
 Con SQL Server 2016 è possibile creare applicazioni intelligenti di importanza critica con una piattaforma di database ibrida e scalabile che dispone di tutti gli strumenti necessari, da prestazioni in memoria e sicurezza avanzata a funzionalità di analisi nel database. SQL Server 2016 aggiunge nuove funzionalità di sicurezza e di query, l'integrazione di Hadoop e cloud, analisi R e altro ancora, oltre a numerosi miglioramenti e ottimizzazioni. 

Questa pagina include informazioni di riepilogo e collegamenti a informazioni più dettagliate sulle novità dei singoli componenti di SQL Server 2016. 

![SQL Server 2016](../sql-server/media/sql-server-2016.png)

 **Per provare subito SQL Server** 
- È possibile scaricare **gratuitamente** [**SQL Server 2016 Developer Edition**](https://www.microsoft.com/cloud-platform/sql-server-editions-developers).
- Scaricare la versione più recente di [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md). 
- Se si ha un account di Azure, accedere a una [macchina virtuale con SQL Server 2016 già installato](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016).

## <a name="sql-server-2016-database-engine"></a>Motore di database di SQL Server 2016
- È ora possibile configurare **più file di database tempDB** durante l'installazione e la configurazione di SQL Server.
- La nuova funzionalità **Query Store** consente di archiviare i testi delle query, i piani di esecuzione e le metriche delle prestazioni all'interno del database, in modo da poter monitorare e risolvere facilmente i problemi di prestazioni. In un dashboard vengono visualizzate le query che usano la quantità maggiore di tempo, di memoria o di risorse della CPU.
- Le **tabelle temporali** sono tabelle cronologiche nelle quali vengono registrate tutte le modifiche dei dati, incluse data e ora in cui si sono verificate.
- Il nuovo **supporto di JSON** incorporato in SQL Server supporta importazioni, esportazioni, l'analisi e l'archiviazione JSON.
- Il nuovo motore di query **PolyBase** consente di integrare SQL Server con dati esterni in Hadoop o nell'archivio BLOB di Azure. È possibile importare ed esportare i dati, oltre a eseguire query.
- La nuova funzionalità **Stretch Database** consente di archiviare i dati in modo dinamico e sicuro da un database di SQL Server locale a un database SQL di Azure nel cloud. SQL Server consente di eseguire automaticamente query su dati locali e remoti nei database collegati. 
- **OLTP in memoria:** 
    - Sono ora supportati i vincoli FOREIGN KEY, UNIQUE e CHECK e le stored procedure compilate native OR, NOT, SELECT DISTINCT, OUTER JOIN, nonché sottoquery in SELECT.
    - Sono supportate tabelle fino a 2 TB (da 256 GB). 
    - Sono disponibili miglioramenti per l'indice columnstore per l'ordinamento e il supporto di gruppi di disponibilità AlwaysOn.
- Nuove funzionalità di sicurezza:
    - **Always Encrypted:** Quando questa funzionalità è abilitata, solo l'applicazione con la chiave di crittografia può accedere ai dati sensibili crittografati nel database di SQL Server 2016. La chiave non viene mai passata a SQL Server.
    - **Dynamic Data Masking:** Se specificato nella definizione della tabella, i dati mascherati sono nascosti per la maggior parte degli utenti e solo gli utenti con l'autorizzazione UNMASK possono visualizzare i dati completi.
    - **Sicurezza a livello di riga:** L'accesso ai dati può essere limitato a livello del motore di database in modo che gli utenti visualizzino solo gli elementi pertinenti. 

## <a name="sql-server-2016-analysis-services-ssas"></a>SQL Server 2016 Analysis Services (SSAS)
SQL Server 2016 Analysis Services offre prestazioni migliori, funzionalità di creazione, gestione di database, filtraggio, elaborazione e molto altro per i database con modello tabulare basati sul **livello di compatibilità 1200**.
- **[SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)** integra in SQL Server il linguaggio di programmazione R, usato per l'analisi statistica. 
- La nuova funzionalità di **verifica di coerenza del database (DBCC)** viene eseguita internamente per rilevare possibili problemi di danneggiamento dei dati.
- La funzionalità **query diretta**, che consente di eseguire query su dati esterni dinamici invece di importarli in primo luogo, ora supporta più origini dati, tra le quali SQL Azure, Oracle e Teradata. 
- Sono disponibili numerose nuove **funzioni DAX (Data Access Expressions)** .
- Il nuovo spazio dei nomi **[Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx)** gestisce istanze e modelli della modalità tabulare. 
- È stato eseguito il refactoring di [Analysis Services Management (AMO)](https://msdn.microsoft.com/library/mt436122.aspx) per includere un secondo assembly, **Microsoft.AnalysisServices.Core.dll**.

Vedere [Motore Analysis Services (SSAS)](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services). 

## <a name="sql-server-2016-integration-services-ssis"></a>SQL Server 2016 Integration Services (SSIS)
- Supporto dei **gruppi di disponibilità AlwaysOn**
- **Distribuzione di pacchetti incrementale**
- Supporto di **Always Encrypted**
- Nuovo ruolo a livello di database **ssis_logreader**
- Nuovo **livello di registrazione personalizzato**
- **Nomi di colonna per gli errori** nel flusso di dati 
- Nuovi **connettori**
- Supporto per il **file system Hadoop (HDFS)**

Vedere [Integration Services (SSIS)](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="sql-server-2016-master-data-services-mds"></a>SQL Server 2016 Master Data Services (MDS)
- **Miglioramenti alle gerarchie derivate**, incluso il supporto per le gerarchie ricorsive e molti-a-molti
- Filtraggio di **attributi basati su dominio**
- **Sincronizzazione delle entità** per la condivisione di dati sulle entità tra i modelli
- Flussi di lavoro di approvazione tramite **insiemi di modifiche**
- **Indici personalizzati** per migliorare le prestazioni delle query
- Nuovi **livelli di autorizzazione** per migliorare la sicurezza
- Nuova progettazione dell'esperienza di **gestione delle regole business**

Vedere [Master Data Services (MDS)](../master-data-services/what-s-new-in-master-data-services-mds.md).

## <a name="sql-server-2016-reporting-services-ssrs"></a>SQL Server 2016 Reporting Services (SSRS)
Reporting Services è stato rinnovato completamente in questa versione. 
- Nuovo **portale Web per i report** con funzionalità KPI
- Nuovo **Mobile Report Publisher**
- **Motore di rendering dei report riprogettato** che supporta HTML5 
- Nuova mappa ad albero e **tipi di grafico** radiali 

Vedere [Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## <a name="next-steps"></a>Passaggi successivi   
- [Installazione di SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)   
- [Note sulla versione di SQL Server 2016](../sql-server/sql-server-2016-release-notes.md) 
- [Foglio dati di SQL Server 2016](https://download.microsoft.com/download/C/5/3/C53C3AEF-653C-4598-8721-D522E8AC6A3A/SQL_Server_2016_Everything_Built-In_Datasheet_EN_US.pdf)
- [Funzionalità supportate dalle edizioni di SQL Server](https://msdn.microsoft.com/library/cc645993.aspx)
- [Requisiti hardware e software per l'installazione di SQL Server 2016](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [Installare SQL Server 2016 dall'Installazione guidata](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [Installazione dei servizi e configurazione](https://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
- [Nuovo modulo di SQL PowerShell](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update/)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
