---
title: Wide World Importers - database di esempio per SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db3d3720291ee80c3e5889ff80ed23edaea3df34
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52402186"
---
# <a name="wide-world-importers-sample-databases-for-microsoft-sql"></a>Database di esempio Wide World Importers per Microsoft SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Questa è una panoramica di Wide World Importers la società fittizia e i flussi di lavoro sono stati risolti in database di esempio WideWorldImporters per SQL Server e Database SQL di Azure.  

Wide World Importers (WWI) è un'utilità di importazione di vendita all'ingrosso originalità beni di consumo e server di distribuzione operativo dall'area di San Francisco alloggiamenti.

Come un ingrosso, i clienti di WWI sono principalmente le aziende che rivendono a singoli utenti. WWI viene venduto ai clienti di vendita al dettaglio degli Stati Uniti inclusi archivi di specializzazione, supermercati, computing archivi, negozi attrazione da turismo e alcune persone. WWI vende anche per altri grossisti tramite una rete di agenti che promuove i prodotti per conto del WWI. Anche se tutti i clienti di WWI si basano attualmente negli Stati Uniti, la società non sia progettata per eseguire il push per l'espansione in altri paesi.

WWI acquista prodotti da fornitori incluse originalità e produttori di giocattoli e altri grossisti originalità. Essi azionari i beni nel proprio warehouse WWI e riordino da fornitori in base alle necessità per soddisfare gli ordini dei clienti. Sono anche grandi volumi di creazione del pacchetto di materiali di acquistare e vendere in piccole quantità per maggiore praticità dei clienti.

Recentemente WWI avviato per la vendita numerose novità commestibili, ad esempio derivati interessanti.  L'azienda in precedenza non aveva gestire gli elementi trattati. A questo punto, per soddisfare trattamento i requisiti di prodotti alimentari, devono monitorare la temperatura nelle stanze refrigeratore e uno qualsiasi dei loro Van chiller sezioni.

## <a name="workflow-for-warehouse-stock-items"></a>Flusso di lavoro per articoli di scorte di magazzino

Il tipico flusso per come gli elementi sono immagazzinati e distribuiti è come indicato di seguito:
- WWI crea gli ordini di acquisto e invia gli ordini per i fornitori.
- Gli elementi di trasmissione fornitori, WWI li riceve e li forniti nel loro warehouse.
- I clienti ordinano gli elementi da WWI
- WWI riempie l'ordine del cliente con le voci del warehouse e quando non è disponibile sufficiente stock, vengono ordinate le azioni aggiuntive da fornitori.
- Alcuni clienti non si desidera attendere che gli elementi non in magazzino. Se si ordina ad esempio cinque diversi elementi azionari e quattro sono disponibili, che vogliono ricevere i quattro elementi e ordine arretrato l'elemento rimanente. L'elemento viene loro inviati più avanti in una spedizione separata.
- I clienti per gli elementi di titoli, le fatture in genere WWI convertendo l'ordine in una fattura.
- I clienti potrebbero ordinare gli elementi non in magazzino. Questi elementi sono relativi a ordini inevasi.
- WWI Invia elementi azionari ai clienti tramite i propri furgoni o tramite altri metodi di spedizione o il corriere.
- I clienti di pagare le fatture per WWI.
- Periodicamente, WWI paga fornitori per gli elementi che sono stati negli ordini di acquisto. Si tratta spesso di qualche minuto dopo che sono stati ricevuti i beni di consumo.

## <a name="data-warehouse-and-analysis-workflow"></a>Flusso di lavoro Data Warehouse e analisi

Anche se il team di WWI Usa SQL Server Reporting Services per generare report operativi dal database WideWorldImporters, devono anche eseguire analitica dei dati ed è necessario generare report strategiche. Il team di aver creato un modello dimensionale dati in un database WideWorldImportersDW. Questo database viene popolato da un pacchetto di Integration Services.

SQL Server Analysis Services viene utilizzato per creare modelli di dati analitici dai dati nel modello di dati unidimensionale. SQL Server Reporting Services viene utilizzato per generare report strategica direttamente dal modello di dati dimensionali e anche dal modello di analisi. Power BI consente di creare i dashboard dagli stessi dati. I dashboard vengono usati in siti Web e su telefoni e Tablet. *Nota: questi modelli di dati e i report non sono ancora disponibili*

## <a name="additional-workflows"></a>Flussi di lavoro aggiuntivi

Questi sono flussi di lavoro aggiuntivi.
- Note sulla carta di credito problemi WWI quando un cliente non riceve good per qualche motivo, o quando le merci sono difettosi. Tali valori vengono considerati fatture negative.
- WWI conta periodicamente le quantità di scorte di elementi azionari da garantire che la quantità di scorte indicata come disponibile nel sistema siano accurate. (Il processo di questa operazione viene chiamato un stocktake).
- A freddo delle temperature chat room. Beni di consumo perishable vengono archiviati in locali frigoriferi. I dati del sensore da queste chat vengono inseriti nel database per scopi di monitoraggio e analitica.
- Rilevamento della posizione del veicolo. Veicoli che trasportano beni di WWI includono sensori che tiene traccia del percorso. Questo percorso verrà nuovamente inserito nel database per il monitoraggio e ulteriormente analitica.

## <a name="fiscal-year"></a>Anno fiscale

L'azienda opera con un esercizio che inizia il 1 ° novembre.

## <a name="terms-of-use"></a>Condizioni d'uso

La licenza per il database di esempio e il codice di esempio descritto qui: [file License. txt](https://github.com/Microsoft/sql-server-samples/blob/master/license.txt)

Il database di esempio include i dati pubblici che sono stati caricati dal data.gov ed EarthData naturale. Le condizioni d'uso si trovano qui: [https://www.naturalearthdata.com/about/terms-of-use/](https://www.naturalearthdata.com/about/terms-of-use/)
