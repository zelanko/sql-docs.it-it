---
title: 'Lezione 1: Creare un progetto e un pacchetto di base con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 84d0b877-603f-4f8e-bb6b-671558ade5c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ff31579a425f9e86fed11811c9d0a42c3113ee15
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "79288135"
---
# <a name="lesson-1-create-a-project-and-basic-package-with-ssis"></a>Lezione 1: Creare un progetto e un pacchetto di base con SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa lezione viene creato un pacchetto ETL semplice che estrae i dati da un'unica origine file flat, li trasformai usando due trasformazioni Ricerca e scrive i dati trasformati in una copia della tabella dei fatti **FactCurrencyRate** del database di esempio **AdventureWorksDW2012**. In questa lezione si apprenderà come creare nuovi pacchetti, aggiungere e configurare connessioni origine e destinazione dati e usare nuovi componenti flusso di controllo e flusso di dati.  
  
Prima di creare un pacchetto è necessario conoscere bene la formattazione usata nei dati di origine e nella destinazione. Sarà quindi possibile definire le trasformazioni necessarie per eseguire il mapping tra i dati di origine e la destinazione.  

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione si basa su Microsoft SQL Server Data Tools, un set di pacchetti di esempio e un database di esempio.

* Per installare SQL Server Data Tools, vedere [Scaricare SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md).  
  
* Per scaricare tutti i pacchetti di lezioni di questa esercitazione:

    1.  Passare alla pagina [Integration Services tutorial files](https://www.microsoft.com/download/details.aspx?id=56827) (File dell'esercitazione su Integration Services).

    2.  Selezionare il pulsante **DOWNLOAD** (Scarica).

    3.  Selezionare il file **Creating a Simple ETL Package.zip** e quindi selezionare **Next** (Avanti).

    4.  Al termine del download, decomprimere il contenuto in una directory locale.  

* Per installare e distribuire il database di esempio **AdventureWorksDW2012**, vedere [Installare e configurare il database di esempio AdventureWorks - SQL](../samples/adventureworks-install-configure.md).
  
## <a name="look-at-the-source-data"></a>Esaminare i dati di origine
In questa esercitazione i dati di origine sono costituiti da dati valutari cronologici all'interno del file flat **SampleCurrencyData.txt**. I dati di origine sono contenuti nelle quattro colonne seguenti: il tasso medio della valuta, un codice valuta, un codice data e il tasso di fine giornata.  
  
Ecco un esempio dei dati di origine presenti nel file SampleCurrencyData.txt:  
  
<pre>1.00070049USD9/3/05 0:001.001201442  
1.00020004USD9/4/05 0:001  
1.00020004USD9/5/05 0:001.001201442  
1.00020004USD9/6/05 0:001  
1.00020004USD9/7/05 0:001.00070049  
1.00070049USD9/8/05 0:000.99980004  
1.00070049USD9/9/05 0:001.001502253  
1.00070049USD9/10/05 0:000.99990001  
1.00020004USD9/11/05 0:001.001101211  
1.00020004USD9/12/05 0:000.99970009</pre>  
  
Quando si usano dati di origine file flat, è importante capire in che modo Gestione connessione file flat interpreta i dati dei file di questo tipo. Se l'origine del file flat è Unicode, tutte le colonne vengono definite nella gestione connessione file flat come [DT_WSTR] con una larghezza predefinita di 50. Se la codifica dell'origine file flat è ANSI, le colonne sono definite come [DT_STR] con una larghezza predefinita pari a 50. Sarà probabilmente necessario cambiare le impostazioni predefinite per adattare meglio i tipi di colonna stringa ai dati. È necessario esaminare il tipo di dati della destinazione e quindi scegliere il tipo corrispondente all'interno di Gestione connessione file flat.  
  
## <a name="look-at-the-destination-data"></a>Esaminare i dati di destinazione
La destinazione dei dati di origine è una copia della tabella dei fatti **FactCurrencyRate** in **AdventureWorksDW**. La tabella **FactCurrencyRate** presenta quattro colonne ed ha relazioni con due tabelle delle dimensioni, come illustrato nella tabella seguente.  
  
|Nome colonna|Tipo di dati|Tabella di ricerca|colonna di ricerca|  
|---------------|-------------|----------------|-----------------|  
|AverageRate|float|nessuno|nessuno|  
|CurrencyKey|int (FK)|DimCurrency|CurrencyKey (PK)|  
|DateKey|int (FK)|DimDate|DateKey (PK)|  
|EndOfDayRate|float|nessuno|nessuno|  
  
## <a name="map-the-source-data-to-the-destination"></a>Eseguire il mapping dei dati di origine alla destinazione  
L'analisi dei formati dei dati di origine e di destinazione indica che per i valori **CurrencyKey** e **DateKey** sono necessarie ricerche. Le trasformazioni che eseguono queste ricerche ottengono tali valori tramite le chiavi alternative derivate dalle tabelle delle dimensioni **DimCurrency** e **DimDate**.  
  
|Colonna file flat|Nome tabella|Nome colonna|Tipo di dati|  
|--------------------|--------------|---------------|-------------|  
|0|FactCurrencyRate|AverageRate|float|  
|1|DimCurrency|CurrencyAlternateKey|nchar (3)|  
|2|DimDate|FullDateAlternateKey|Data|  
|3|FactCurrencyRate|EndOfDayRate|float|  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Creare un nuovo progetto di Integration Services](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
-   [Passaggio 2: Aggiungere e configurare una gestione connessione file flat](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
-   [Passaggio 3: Aggiungere e configurare una gestione connessione OLE DB](../integration-services/lesson-1-3-adding-and-configuring-an-ole-db-connection-manager.md)  
  
-   [Passaggio 4: Aggiungere un'attività Flusso di dati al pacchetto](../integration-services/lesson-1-4-adding-a-data-flow-task-to-the-package.md)  
  
-   [Passaggio 5: Aggiungere e configurare l'origine file flat](../integration-services/lesson-1-5-adding-and-configuring-the-flat-file-source.md)  
  
-   [Passaggio 6: Aggiungere e configurare le trasformazioni Ricerca](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
-   [Passaggio 7: Aggiungere e configurare la destinazione OLE DB](../integration-services/lesson-1-7-adding-and-configuring-the-ole-db-destination.md)  
  
-   [Passaggio 8: Annotare e formattare il pacchetto della lezione 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
-   [Passaggio 9: Testare il pacchetto della lezione 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
[Passaggio 1: Creare un nuovo progetto di Integration Services](../integration-services/lesson-1-1-creating-a-new-integration-services-project.md)  
  
