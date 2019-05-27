---
title: Creare Set di Testing (Creazione guidata di Data Mining dati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0e4d1a384995c0c49c346102f8fddbcdf47f68
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086786"
---
# <a name="create-testing-set-data-mining-wizard"></a>Crea set di testing (Creazione guidata modello di data mining)
  Usare la pagina **Crea set di testing** per specificare la quantità di dati da usare per il training e la quantità di dati da riservare per l'uso come set di test. La separazione dei dati in set di training e set di testing durante la creazione di una struttura di data mining rende molto più facile la determinazione dell'accuratezza dei modelli di data mining che vengono creati successivamente.  
  
 È possibile specificare la quantità di dati da testare in percentuale oppure è possibile specificare un numero per limitare il numero di case utilizzato per il test. Se si specifica sia una percentuale che un numero massimo di case da utilizzare per il test, entrambe le impostazioni vengono utilizzate e il set di dati del test contiene il numero più basso di case. Per impostazione predefinita, il 30 per cento dei dati viene utilizzato per il testing e il 70 per cento per il training, senza numero massimo di test case.  
  
 Per impostazione predefinita, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] genera un valore di inizializzazione numerico che viene utilizzato per avviare il partizionamento. Questo valore di inizializzazione è basato sul nome della struttura di data mining. Per assicurarsi che la partizione non venga modificata se viene modificato il nome della struttura di data mining, è possibile specificare un valore per il valore di inizializzazione, configurando la proprietà HoldoutSeed della struttura di data mining. Se si modifica il valore di inizializzazione di controllo, è necessario rielaborare la struttura.  
  
 Se in un secondo momento si desidera modificare la quantità di dati di training o test, è possibile modificare il `HoldoutMaxCases` e `HoldoutMaxPercent` delle proprietà nella struttura di data mining utilizzando il **proprietà** finestra. Tuttavia, dopo avere apportato la modifica è necessario rielaborare la struttura di data mining e tutti i modelli di data mining associati. Vengono applicate anche le seguenti limitazioni:  
  
-   Il partizionamento di una struttura di data mining è supportato solo quando la struttura di data mining è archiviata in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Le versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non supportano la memorizzazione nella cache delle informazioni sulle partizioni per le strutture di data mining.  
  
-   Non è possibile partizionare una struttura di data mining se contiene una colonna Key Time, necessaria per i modelli di data mining della serie temporale.  
  
-   Non è possibile partizionare i dati se si sta tentando di stimare un valore archiviato in una tabella nidificata.  
  
 **Per altre informazioni:** [Test e convalida &#40;Data Mining&#41;](data-mining/testing-and-validation-data-mining.md), [creare una struttura di Data Mining relazionale](data-mining/create-a-relational-mining-structure.md), [esercitazione di base di Data Mining](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>Opzioni  
 **Percentuale di dati per i test**  
 Fare clic sulle frecce verso l'alto e verso il basso per aumentare o ridurre la percentuale di dati da utilizzare come set di training oppure digitare un valore compreso tra 0 e 100 nella casella di testo.  
  
 **Numero massimo di case nel set di dati**  
 Digitare un numero per limitare il numero di case che possono essere utilizzati per il testing.  
  
 Se si specifica un numero superiore al numero effettivo di case nei dati, verranno utilizzati tutti i case.  
  
 Il valore predefinito è NULL. Ciò significa che non sono presenti limiti.  
  
## <a name="see-also"></a>Vedere anche  
 [I dati della Guida F1 di procedura guidata di Data Mining &#40;Analysis Services - Data Mining&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Suggerisci colonne correlate &#40;Creazione guidata di Data Mining&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Specificare i tipi di tabella &#40;Creazione guidata di Data Mining&#41;](specify-table-types-data-mining-wizard.md)   
 [Specificare il contenuto e il tipo di dati della colonna &#40;Creazione guidata di Data Mining&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
