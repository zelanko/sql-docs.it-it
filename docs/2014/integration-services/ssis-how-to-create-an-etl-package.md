---
title: 'Esercitazione SSIS: Creazione di un pacchetto ETL semplice | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2a99169168eb21f0a7d42f133e7e882141c776e6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357911"
---
# <a name="ssis-tutorial-creating-a-simple-etl-package"></a>Esercitazione SSIS: Creazione di un pacchetto ETL semplice
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) è una piattaforma per la creazione di soluzioni di integrazione dei dati, ad esempio estrazione, trasformazione e caricamento (ETL) di pacchetti per il data warehousing ad alte prestazioni. In SSIS sono disponibili strumenti grafici e procedure guidate per la compilazione e il debug di pacchetti, attività per l'esecuzione di funzioni di flusso di lavoro quali operazioni FTP, esecuzione di istruzioni SQL e invio di messaggi di posta elettronica, origini dei dati e destinazioni per l'estrazione e il caricamento dei dati, trasformazioni per la pulizia, l'aggregazione, l'unione e la copia dei dati, il servizio di gestione [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , per l'amministrazione dell'esecuzione e dell'archiviazione dei pacchetti, nonché API (Application Programming Interface) per la programmazione del modello a oggetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 In questa esercitazione verrà illustrato come usare Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per creare un pacchetto semplice di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Tale pacchetto preleva i dati da un file flat, li riformatta e quindi li inserisce in una tabella dei fatti. Nelle lezioni successive il pacchetto viene espanso per illustrare i loop, le configurazioni del pacchetto, la registrazione e il flusso degli errori.  
  
 Contestualmente all'installazione dei dati di esempio utilizzati nell'esercitazione, vengono installate anche le versioni complete dei pacchetti creati in ogni lezione. Questi pacchetti completi consentono di iniziare l'esercitazione dalla lezione desiderata. Se è la prima volta che si utilizzano i pacchetti o il nuovo ambiente di sviluppo, è consigliabile iniziare dalla lezione 1.  
  
## <a name="what-you-will-learn"></a>Lezioni dell'esercitazione  
 Il modo più efficace per acquisire familiarità con i nuovi strumenti e controlli e con le caratteristiche disponibili in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consiste nell'usarli. Questa esercitazione illustra l'utilizzo di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] per creare un pacchetto ETL semplice che include i loop, le configurazioni, la logica del flusso degli errori e la registrazione.  
  
## <a name="requirements"></a>Requisiti  
 Questa esercitazione è destinata agli utenti esperti nelle operazioni fondamentali sui database ma con una conoscenza limitata delle nuove funzionalità disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Per utilizzare l'esercitazione è necessario che nel sistema siano installati i componenti seguenti:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con il database **AdventureWorksDW2012** . Per una maggiore sicurezza, i database di esempio non vengono installati per impostazione predefinita. Per scaricare il database **AdventureWorksDW2012** , vedere la pagina relativa ad [Adventure Works per SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=275026).  
  
    > [!IMPORTANT]  
    >  Quando si collega il database (file\*.mdf), per impostazione predefinita [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] cerca un file con estensione ldf. È necessario rimuovere manualmente questo file prima di fare clic su OK nella finestra di dialogo **Collega database** .  
    >   
    >  Per altre informazioni sul collegamento di database, vedere [Collegare un database](../relational-databases/databases/attach-a-database.md).  
  
-   Dati di esempio I dati di esempio sono inclusi nei pacchetti di lezioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per scaricare i dati di esempio e i pacchetti di lezioni, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **DOWNLOADS** .  
  
    3.  Fare clic sul file SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
## <a name="lessons-in-this-tutorial"></a>Lezioni dell'esercitazione  
 [Lezione 1: Creazione del progetto e il pacchetto di base](lesson-1-create-a-project-and-basic-package-with-ssis.md)  
 In questa lezione verrà creato un pacchetto ETL semplice che estrae i dati da un unico file flat, li trasforma utilizzando le trasformazioni Ricerca e infine carica il risultato in una destinazione tabella dei fatti.  
  
 [Lezione 2: Aggiungere cicli](lesson-2-adding-looping-with-ssis.md)  
 In questa lezione si espanderà il pacchetto creato nella lezione 1 per utilizzare le nuove funzionalità di loop che consentono di estrarre più file flat in un unico processo di flusso di dati.  
  
 [Lezione 3: Aggiunta di registrazione](lesson-3-add-logging-with-ssis.md)  
 In questa lezione si espanderà il pacchetto creato nella lezione 2 per utilizzare le nuove funzionalità di registrazione.  
  
 [Lezione 4: Aggiunta del reindirizzamento del flusso di errore](lesson-4-add-error-flow-redirection-with-ssis.md)  
 In questa lezione si espanderà il pacchetto creato nella lezione 3 per utilizzare le nuove configurazioni di output degli errori.  
  
 [Lezione 5: Aggiunta delle configurazioni di pacchetto per il modello di distribuzione del pacchetto](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
 In questa lezione si espanderà il pacchetto creato nella lezione 4 per utilizzare le nuove opzioni di configurazione del pacchetto.  
  
 [Lezione 6: Utilizzo di parametri con il modello di distribuzione](lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
 In questa lezione si espanderà il pacchetto creato nella lezione 5 per utilizzare i nuovi parametri con il modello di distribuzione del progetto.  
  
  
