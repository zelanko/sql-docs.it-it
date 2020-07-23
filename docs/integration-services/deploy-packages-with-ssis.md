---
title: 'Esercitazione SSIS: Distribuzione di pacchetti | Microsoft Docs'
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d6636cbd74f31448381b1f6cb2c3dd3826324a5
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916647"
---
# <a name="deploy-packages-with-ssis"></a>Esercitazione SSIS: Distribuzione di pacchetti

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include strumenti che consentono di distribuire in modo semplice i pacchetti in un altro computer. Gli strumenti di distribuzione consentono inoltre di gestire eventuali dipendenze, ad esempio configurazioni e file necessari per il pacchetto. In questa esercitazione verrà illustrato come utilizzare tali strumenti per installare pacchetti e relative dipendenze in un computer di destinazione.    
    
Verranno innanzitutto eseguite le attività di preparazione alla distribuzione. Verrà creato un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] al quale verranno aggiunti i pacchetti e i file di dati esistenti. Non verrà creato alcun nuovo pacchetto da zero, bensì si utilizzeranno solo i pacchetti completi creati appositamente ai fini di questa esercitazione. Non sarà necessario modificare le funzionalità dei pacchetti dell'esercitazione, tuttavia, dopo avere aggiunto i pacchetti al progetto, potrebbe risultare utile aprirli in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] ed esaminarne i contenuti. In questo modo sarà possibile acquisire familiarità con i tipi di dipendenze dei pacchetti, ad esempio i file di log, e con le interessanti caratteristiche dei pacchetti.    
    
Ai fini della distribuzione, si procederà inoltre all'aggiornamento dei pacchetti affinché utilizzino le configurazioni. Queste ultime rendono le proprietà e gli oggetti dei pacchetti aggiornabili in fase di esecuzione. In questa esercitazione le configurazioni verranno utilizzate per aggiornare le stringhe di connessione di file di testo e di log e i percorsi dei file XML e XSD utilizzati dai pacchetti. Per altre informazioni, vedere [Configurazioni di pacchetto](../integration-services/packages/package-configurations.md) e [Creazione di configurazioni dei pacchetti](../integration-services/packages/create-package-configurations.md).    
    
Dopo aver verificato che i pacchetti vengono eseguiti correttamente in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], si creerà un pacchetto di distribuzione da utilizzare per installare i pacchetti. Il pacchetto di distribuzione include i file del pacchetto e altri elementi aggiunti al progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , le dipendenze del pacchetto incluse automaticamente da [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e l'utilità di distribuzione compilata dall'utente. Per altre informazioni, vedere [Creazione di un'utilità di distribuzione](../integration-services/packages/create-a-deployment-utility.md).    
    
Il pacchetto di distribuzione verrà quindi copiato nel computer di destinazione su cui verrà eseguita l'Installazione guidata pacchetti che consente di installare i pacchetti e le relative dipendenze. I pacchetti verranno installati nel database msdb di SQL Server, mentre i file ausiliari e di supporto verranno installati nel file system. Poiché i pacchetti distribuiti utilizzano le configurazioni, sarà necessario aggiornare queste ultime in modo che riflettano i nuovi valori necessari per l'esecuzione corretta dei pacchetti nell'ambiente in cui sono stati installati.    
    
I pacchetti verranno infine eseguiti in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] mediante l'Utilità di esecuzione pacchetti.    
    
L'obiettivo di questa esercitazione è simulare la complessità delle problematiche di una possibile distribuzione reale. Se non è possibile distribuire i pacchetti in un altro computer è comunque possibile eseguire l'esercitazione installando i pacchetti nel database msdb nell'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e quindi eseguirli in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] nella medesima istanza.    

**Tempo stimato per il completamento dell'esercitazione:** 2 ore

## <a name="what-you-learn"></a>Informazioni ottenute dall'esercitazione    
Il modo più efficace per acquisire familiarità con i nuovi strumenti e controlli e con le caratteristiche disponibili in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] è quello di usarli. Questa esercitazione consente di eseguire in modo semplificato i passaggi necessari per creare un progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e quindi aggiungervi i pacchetti e gli altri file necessari. Dopo aver completato il progetto, si procederà alla creazione di un pacchetto di distribuzione, alla copia del pacchetto nel computer di destinazione e quindi all'installazione in quest'ultimo dei pacchetti.    
    
## <a name="prerequisites"></a>Prerequisites    
Questa esercitazione è destinata agli utenti già esperti nelle operazioni di base sul file system, ma con una limitata conoscenza delle nuove caratteristiche disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Ai fini dell'apprendimento dei concetti di base di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che verranno usati in questa esercitazione, potrebbe risultare utile completare prima la seguente esercitazione di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] : [Esercitazione SSIS: Creazione di un pacchetto ETL semplice](../integration-services/ssis-how-to-create-an-etl-package.md).    
    
### <a name="on-the-source-computer"></a>Nel computer di origine

Nel computer in cui si crea il pacchetto di distribuzione **devono essere installati i componenti seguenti:**

- SQL Server. Scaricare una versione di valutazione gratuita o un'edizione per sviluppatori di SQL da [Download di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).

- Dati di esempio, pacchetti completi, configurazioni e un file Leggimi. Per scaricare i dati di esempio e i pacchetti di lezioni come file con estensione zip, vedere i [file delle esercitazioni di SQL Server Integration Services](https://www.microsoft.com/download/details.aspx?id=56827). La maggior parte dei file nel file ZIP è di sola lettura per evitare modifiche accidentali. Per scrivere l'output in un file o per modificarlo, potrebbe essere necessario disattivare l'attributo di sola lettura nelle proprietà del file.

-   Database di esempio **AdventureWorks2014**. Per scaricare il database **AdventureWorks2014**, scaricare `AdventureWorks2014.bak` dai [database di esempio AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) e ripristinare il backup.  

-   È necessario avere le autorizzazioni per creare ed eliminare tabelle nel database AdventureWorks.
    
-   [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).    
    
### <a name="on-the-destination-computer"></a>Nel computer di destinazione

Nel computer in cui verranno distribuiti i pacchetti **devono essere installati i componenti seguenti**:    
    
- SQL Server. Scaricare una versione di valutazione gratuita o un'edizione per sviluppatori di SQL da [Download di SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).

- Dati di esempio, pacchetti completi, configurazioni e un file Leggimi. Per scaricare i dati di esempio e i pacchetti di lezioni come file con estensione zip, vedere i [file delle esercitazioni di SQL Server Integration Services](https://www.microsoft.com/download/details.aspx?id=56827). La maggior parte dei file nel file ZIP è di sola lettura per evitare modifiche accidentali. Per scrivere l'output in un file o per modificarlo, potrebbe essere necessario disattivare l'attributo di sola lettura nelle proprietà del file.

-   Database di esempio **AdventureWorks2014**. Per scaricare il database **AdventureWorks2014**, scaricare `AdventureWorks2014.bak` dai [database di esempio AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) e ripristinare il backup.  
    
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).    
    
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per installare SSIS, vedere [Installare Integration Services](install-windows/install-integration-services.md).
    
-   È necessario avere le autorizzazioni per creare ed eliminare tabelle nel database AdventureWorks e per eseguire i pacchetti SSIS in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].    
    
-   È necessario disporre delle autorizzazioni di lettura e scrittura sulla tabella `sysssispackages` nel database di sistema `msdb` di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].    
    
Se si prevede di distribuire i pacchetti nello stesso computer in cui si crea il pacchetto di distribuzione, è necessario che tale computer soddisfi i requisiti di entrambi i sistemi di origine e di destinazione.    
        
## <a name="lessons-in-this-tutorial"></a>Lezioni dell'esercitazione    
[Lezione 1: Preparazione alla creazione del pacchetto di distribuzione](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)    
In questa lezione verrà preparata la distribuzione di una soluzione ETL creando un nuovo progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e aggiungendovi i pacchetti e gli altri file necessari.    
    
[Lezione 2: Creare il pacchetto di distribuzione in SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)    
In questa lezione verrà compilata un'utilità di distribuzione e verrà verificato che il pacchetto di distribuzione includa i file necessari.    
    
[Lezione 3: Installare i pacchetti SSIS](../integration-services/lesson-3-install-ssis-packages.md)    
In questa lezione si procederà alla copia del pacchetto di distribuzione nel computer di destinazione, all'installazione e quindi all'esecuzione dei pacchetti.    
    

