---
title: 'Esercitazione SSIS: Creazione di un pacchetto ETL | Microsoft Docs'
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: quickstart
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a22e24e2abe0d69e4ecbeda2b644eaef39fe6bf9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002321"
---
# <a name="ssis-how-to-create-an-etl-package"></a>Esercitazione SSIS: Creazione di un pacchetto ETL semplice

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa esercitazione viene illustrato come usare Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per creare un pacchetto semplice di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Tale pacchetto preleva i dati da un file flat, li riformatta e quindi li inserisce in una tabella dei fatti. Nelle lezioni successive il pacchetto viene espanso per illustrare i loop, le configurazioni del pacchetto, la registrazione e il flusso degli errori.  
  
Contestualmente all'installazione dei dati di esempio usati nell'esercitazione, vengono installate anche le versioni complete dei pacchetti creati in ogni lezione. Questi pacchetti completi consentono di iniziare l'esercitazione dalla lezione desiderata. Se è la prima volta che si usano i pacchetti o il nuovo ambiente di sviluppo, è consigliabile iniziare dalla lezione 1.  

## <a name="what-is-sql-server-integration-services-ssis"></a>Definizione di SQL Server Integration Services (SSIS)

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) è una piattaforma per la compilazione di soluzioni di integrazione di dati dalle prestazioni elevate, in cui sono incluse funzionalità per l'estrazione, la trasformazione e il caricamento (ETL) di pacchetti per il data warehousing. In SSIS sono disponibili strumenti grafici e procedure guidate per la compilazione e il debug di pacchetti, attività per l'esecuzione di funzioni di flusso di lavoro quali operazioni FTP, esecuzione di istruzioni SQL e invio di messaggi di posta elettronica, origini dei dati e destinazioni per l'estrazione e il caricamento dei dati, trasformazioni per la pulizia, l'aggregazione, l'unione e la copia dei dati, un servizio di gestione `SSISDB`, per l'amministrazione dell'esecuzione e dell'archiviazione dei pacchetti, nonché API (Application Programming Interface) per la programmazione del modello a oggetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  

## <a name="what-you-learn"></a>Informazioni ottenute dall'esercitazione  
Il modo più efficace per acquisire familiarità con i nuovi strumenti e controlli e con le caratteristiche disponibili in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consiste nell'usarli. Questa esercitazione illustra l'uso di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per creare un pacchetto ETL semplice che include i cicli, le configurazioni, la logica del flusso degli errori e la registrazione.  
  
## <a name="prerequisites"></a>Prerequisites  
Questa esercitazione è destinata agli utenti esperti nelle operazioni fondamentali sui database ma con una conoscenza limitata delle nuove funzionalità disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  

Per eseguire questa esercitazione, è necessario che nel sistema siano installati i componenti seguenti:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per installare SQL Server e SSIS, vedere [Installare Integration Services](install-windows/install-integration-services.md).

-   Database di esempio **AdventureWorksDW2012**. Per scaricare il database **AdventureWorksDW2012**, scaricare `AdventureWorksDW2012.bak` dai [database di esempio AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) e ripristinare il backup.  

-   I file dei **dati di esempio**. I dati di esempio sono inclusi nei pacchetti di lezioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per scaricare i dati di esempio e i pacchetti di lezioni come file con estensione zip, vedere i [file delle esercitazioni di SQL Server Integration Services](https://www.microsoft.com/download/details.aspx?id=56827).

    - La maggior parte dei file nel file ZIP è di sola lettura per evitare modifiche accidentali. Per scrivere l'output in un file o per modificarlo, potrebbe essere necessario disattivare l'attributo di sola lettura nelle proprietà del file.
    - I pacchetti di esempio presuppongono che i file di dati si trovino nella cartella `C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Creating a Simple ETL Package`. Se il download viene decompresso in un'altra posizione, potrebbe essere necessario aggiornare il percorso del file in più posizioni nei pacchetti di esempio.

## <a name="lessons-in-this-tutorial"></a>Lezioni dell'esercitazione  
[Lezione 1: Creare un progetto e un pacchetto di base con SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
In questa lezione viene creato un pacchetto ETL semplice che estrae i dati da un unico file flat, li trasforma usando le trasformazioni Ricerca e infine carica il risultato in una destinazione tabella dei fatti.  
  
[Lezione 2: Aggiungere cicli con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
In questa lezione si espande il pacchetto creato nella lezione 1 per usare le nuove funzionalità di ciclo che consentono di estrarre più file flat in un unico processo di flusso di dati.  
  
[Lezione 3: Aggiungere la registrazione con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
In questa lezione si espande il pacchetto creato nella lezione 2 per usare le nuove funzionalità di registrazione.  
  
[Lezione 4: Aggiungere il reindirizzamento del flusso degli errori con SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
In questa lezione si espande il pacchetto creato nella lezione 3 per usare le nuove configurazioni di output degli errori.  
  
[Lezione 5: Aggiungere configurazioni del pacchetto SSIS per il modello di distribuzione del pacchetto](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
In questa lezione si espande il pacchetto creato nella lezione 4 per usare le nuove opzioni di configurazione del pacchetto.  
  
[Lezione 6: Uso dei parametri con il modello di distribuzione del progetto in SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
In questa lezione si espande il pacchetto creato nella lezione 5 per usare i nuovi parametri con il modello di distribuzione del progetto.  
  
  
  
