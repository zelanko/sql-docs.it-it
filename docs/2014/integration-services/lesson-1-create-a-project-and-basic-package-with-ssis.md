---
title: 'Lezione 1: Creazione del progetto e il pacchetto di base | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 652cf44f70e890b3203ed27890d06f98d70b7f1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767503"
---
# <a name="lesson-1-creating-the-project-and-basic-package"></a>Lezione 1: Creazione del progetto e il pacchetto di base
  In questa lezione verrà creato un pacchetto ETL semplice tramite cui vengono estratti i dati da un'unica origine file flat, trasformati i dati usando due componenti di trasformazione Ricerca e scritti i dati in questione nella tabella dei fatti **FactCurrency** di **AdventureWorksDW2012**. In questa lezione si imparerà a creare nuovi pacchetti, aggiungere e configurare connessioni origine e destinazione dati e usare nuovi componenti flusso di controllo e flusso di dati.  
  
> [!IMPORTANT]  
>  Per eseguire questa esercitazione, è necessario il database di esempio **AdventureWorksDW2012** . Per altre informazioni sull'installazione e distribuzione **AdventureWorksDW2012**, vedere [Microsoft SQL Server Product Samples: Reporting Services](https://archive.codeplex.com/?p=msftrsprodsamples).  
  
## <a name="understanding-the-package-requirements"></a>Informazioni sui requisiti del pacchetto  
 Per questa esercitazione è richiesto Microsoft SQL Server Data Tools.  
  
 Per altre informazioni sull'installazione di SQL Server Data Tools, vedere [Scaricare SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017).  
  
 Prima di creare un pacchetto è necessario conoscere bene la formattazione usata nei dati di origine e nella destinazione. Dopo avere acquisito familiarità con questi due formati di dati sarà possibile definire le trasformazioni necessarie per eseguire il mapping tra i dati di origine e la destinazione.  
  
### <a name="looking-at-the-source"></a>Esame dell'origine  
 In questa esercitazione vengono usati i dati valutari contenuti nel file flat SampleCurrencyData.txt. I dati di origine sono contenuti nelle quattro colonne seguenti: il tasso medio della valuta, un codice valuta, un codice data e il tasso di fine giornata.  
  
 Di seguito viene riportato un esempio dei dati di origine contenuti nel file SampleCurrencyData.txt:  
  
 `1.00070049USD9/3/05 0:001.001201442`  
  
 `1.00020004USD9/4/05 0:001`  
  
 `1.00020004USD9/5/05 0:001.001201442`  
  
 `1.00020004USD9/6/05 0:001`  
  
 `1.00020004USD9/7/05 0:001.00070049`  
  
 `1.00070049USD9/8/05 0:000.99980004`  
  
 `1.00070049USD9/9/05 0:001.001502253`  
  
 `1.00070049USD9/10/05 0:000.99990001`  
  
 `1.00020004USD9/11/05 0:001.001101211`  
  
 `1.00020004USD9/12/05 0:000.99970009`  
  
 Quando si usano dati di origine di file flat, è importante capire in che modo Gestione connessione file flat interpreta i relativi dati. Se l'origine del file flat è Unicode, tutte le colonne vengono definite nella gestione connessione file flat come [DT_WSTR] con una larghezza predefinita di 50. Se l'origine del file flat è con codifica ANSI, le colonne sono definite come [DT_STR] con una larghezza di 50. Le impostazioni predefinite sono liberamente modificabili per adattare al meglio i tipi di colonna ai dati. Per farlo, è necessario esaminare il tipi di dati della destinazione di scrittura dei dati e scegliere il tipo corretto all'interno di Gestione connessione file flat.  
  
### <a name="looking-at-the-destination"></a>Esame della destinazione  
 La destinazione finale dei dati di origine è la tabella dei fatti **FactCurrency** di **AdventureWorksDW**. La tabella dei fatti **FactCurrency** presenta quattro colonne e ha relazioni con due tabelle delle dimensioni, come mostrato nella tabella seguente.  
  
|Nome colonna|Tipo di dati|Tabella di ricerca|Colonna di ricerca|  
|-----------------|---------------|------------------|-------------------|  
|AverageRate|FLOAT|None|None|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|FLOAT|None|None|  
  
### <a name="mapping-source-data-to-be-compatible-with-the-destination"></a>Mapping dei dati di origine per la compatibilità con la destinazione  
 L'analisi dei formati dei dati di origine e di destinazione indica che per i valori **CurrencyKey** e **DateKey** saranno necessarie le ricerche. Tramite le trasformazioni mediante le quali verranno svolte queste ricerche si otterranno i valori **CurrencyKey** e **DateKey** usando le chiavi alternative ottenute dalle tabelle delle dimensioni **DimCurrency** e **DimDate** .  
  
|Colonna file flat|Nome tabella|Nome colonna|Tipo di dati|  
|----------------------|----------------|-----------------|---------------|  
|0|FactCurrency|AverageRate|FLOAT|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|DimDate|FullDateAlternateKey|Data|  
|3|FactCurrency|EndOfDayRate|FLOAT|  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Creazione di un nuovo progetto di Integration Services](lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [Passaggio 2: Aggiunta e configurazione della gestione connessione file flat](lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [Passaggio 3: Aggiunta e configurazione di una gestione connessione OLE DB](lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [Passaggio 4: Aggiunta di un'attività flusso di dati al pacchetto](lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [Passaggio 5: Aggiunta e configurazione dell'origine file flat](lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [Passaggio 6: Aggiunta e configurazione delle trasformazioni ricerca](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [Passaggio 7: Aggiunta e configurazione della destinazione OLE DB](lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [Passaggio 8: Effettua la comprensione del pacchetto della lezione 1](lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [Passaggio 9: Test del pacchetto dell'esercitazione della lezione 1](lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
 [Passaggio 1: Creazione di un nuovo progetto di Integration Services](lesson-1-1-creating-a-new-integration-services-project.md)  
  
  
