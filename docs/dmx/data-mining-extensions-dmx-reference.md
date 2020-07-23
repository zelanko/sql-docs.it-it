---
title: Guida di riferimento a DMX (Data Mining Extensions) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 02c7185ebbf264ebf8ed8adda4915170f888e74b
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971783"
---
# <a name="data-mining-extensions-dmx-reference"></a>Guida di riferimento a DMX (Data Mining Extensions)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Data Mining Extensions (DMX) è un linguaggio che è possibile utilizzare per creare e utilizzare i modelli di data mining in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . DMX consente di creare la struttura di nuovi modelli di data mining, eseguirne il training, nonché esplorarli, gestirli ed eseguire stime basate su tali modelli. DMX comprende istruzioni DDL (Data Definition Language) e DML (Data Manipulation Language), nonché funzioni e operatori.  
  
## <a name="microsoft-ole-db-for-data-mining-specification"></a>Specifica Microsoft OLE DB for Data Mining  
 Le funzionalità data mining di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sono compilate per essere conformi al [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB per la specifica di data mining.  
  
 Il [!INCLUDE[msCoName](../includes/msconame-md.md)] OLE DB per la specifica di data mining definisce gli elementi seguenti:  
  
-   Una struttura per contenere le informazioni che definiscono un modello di data mining.  
  
-   Un linguaggio per la creazione e l'utilizzo di modelli di data mining.  
  
 La specifica definisce gli aspetti fondamentali del data mining, ad esempio l'oggetto virtuale modello di data mining. L'oggetto modello di data mining incapsula tutte le informazioni note su un determinato modello di data mining. Tale oggetto è strutturato come una tabella SQL, con colonne, tipi di dati e metainformazioni che descrivono il modello. Grazie a questa struttura è possibile utilizzare il linguaggio DMX, che è un'estensione di SQL, per creare e utilizzare i modelli.  
  
 **Per ulteriori informazioni: strutture di** [data mining &#40;Analysis Services-Data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining)  
  
##  <a name="dmx-statements"></a><a name="BKMK_DMXStatements"></a>Istruzioni DMX  
 È possibile utilizzare istruzioni DMX per creare, elaborare, eliminare, copiare ed esplorare modelli di data mining e generare stime basate su tali modelli. DMX include due tipi di istruzioni, le istruzioni per la definizione dei dati e istruzioni per la manipolazione dei dati. Ogni tipo di istruzione consente di eseguire attività diverse.  
  
 Ulteriori informazioni sull'utilizzo delle istruzioni DMX sono disponibili nelle sezioni seguenti:  
  
-   [Istruzioni per la definizione dei dati](#BKMK_DDL)  
  
-   [Istruzioni di manipolazione dei dati](#BKMK_DML)  
  
-   [Nozioni fondamentali sulle query](#BKMK_Queries)  
  
###  <a name="data-definition-statements"></a><a name="BKMK_DDL"></a>Istruzioni per la definizione dei dati  
 Le istruzioni DMX per la definizione dei dati consentono di creare e definire nuovi modelli e strutture di data mining, importare ed esportare modelli e strutture di data mining ed eliminare i modelli esistenti da un database. Le istruzioni DMX per la definizione dei dati fanno parte del linguaggio DDL (Data Definition Language).  
  
 Le istruzioni DMX per la definizione dei dati consentono di eseguire le attività seguenti:  
  
-   Creare una struttura di data mining utilizzando l'istruzione [create Mining Structure](../dmx/create-mining-structure-dmx.md) e aggiungere un modello di data mining alla struttura di data mining utilizzando l'istruzione [ALTER MINING STRUCTURE](../dmx/alter-mining-structure-dmx.md) .  
  
-   Creare contemporaneamente un modello di data mining e una struttura di data mining associata utilizzando l'istruzione [create Mining Model](../dmx/create-mining-model-dmx.md) per compilare un oggetto del modello di data mining vuoto.  
  
-   Esportare in un file un modello di data mining e la struttura di data mining associata utilizzando l'istruzione [Export](../dmx/export-dmx.md) . Importare un modello di data mining e la struttura di data mining associata da un file creato dall'istruzione EXPORT utilizzando l'istruzione [Import](../dmx/import-dmx.md) .  
  
-   Copiare la struttura di un modello di data mining esistente in un nuovo modello ed eseguirne il training con gli stessi dati utilizzando l'istruzione [select into](../dmx/select-into-dmx.md) .  
  
-   Rimuovere completamente un modello di data mining da un database utilizzando l'istruzione [Drop Mining Model](../dmx/drop-mining-model-dmx.md) . Rimuovere completamente una struttura di data mining e tutti i modelli di data mining associati dal database utilizzando l'istruzione [Drop Mining Structure](../dmx/drop-mining-structure-dmx.md) .  
  
 Per ulteriori informazioni sulle attività data mining che è possibile eseguire utilizzando le istruzioni DMX, vedere [informazioni di riferimento sulle estensioni di data mining &#40;dmx&#41; Istruzione](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Torna a Istruzioni DMX](#BKMK_DMXStatements)  
  
###  <a name="data-manipulation-statements"></a><a name="BKMK_DML"></a>Istruzioni di manipolazione dei dati  
 Le istruzioni DMX per la manipolazione dei dati consentono di utilizzare modelli di data mining esistenti, esplorare i modelli e creare stime basate su di essi. Le istruzioni DMX per la manipolazione dei dati fanno parte del linguaggio DML (Data Manipulation Language).  
  
 Le istruzioni DMX per la manipolazione dei dati consentono di eseguire le attività seguenti:  
  
-   Eseguire il training di un modello di data mining utilizzando l'istruzione [Insert into](../dmx/insert-into-dmx.md) . Tale istruzione non inserisce i dati effettivi dell'origine in un oggetto modello di data mining, ma crea un'astrazione che descrive il modello di data mining creato dall'algoritmo. La query di origine per un'istruzione INSERT INTO è descritta in [\<source data query>](../dmx/source-data-query.md) .  
  
-   Estendere l'istruzione SELECT per visualizzare le informazioni calcolate durante il training del modello e archiviate nel modello di data mining, ad esempio le statistiche dei dati di origine. Di seguito sono riportate le clausole che è possibile includere per estendere le potenzialità dell'istruzione SELECT:  
  
    -   [Selezionare DISTINCT FROM &#60;Model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)  
  
    -   [Selezionare da &#60;modello&#62;. CONTENUTO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)  
  
    -   [Selezionare da &#60;modello&#62;. CASI &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)  
  
    -   [Selezionare da &#60;modello&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)  
  
    -   [Selezionare da &#60;modello&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)  
  
-   Creare stime basate su un modello di data mining esistente utilizzando la clausola [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) dell'istruzione SELECT. La query di origine per un'istruzione PREDICtion JOIN è descritta in [\<source data query>](../dmx/source-data-query.md) .  
  
-   Rimuovere tutti i dati sottoposti a training da un modello o una struttura utilizzando l'istruzione [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) .  
  
 Per ulteriori informazioni sulle attività data mining che è possibile eseguire utilizzando le istruzioni DMX, vedere [informazioni di riferimento sulle estensioni di data mining &#40;dmx&#41; Istruzione](../dmx/data-mining-extensions-dmx-statements.md).  
  
 [Torna a Istruzioni DMX](#BKMK_DMXStatements)  
  
###  <a name="dmx-query-fundamentals"></a><a name="BKMK_Queries"></a>Nozioni fondamentali sulle query DMX  
 L'istruzione SELECT costituisce la base per la maggior parte delle query DMX. A seconda delle clausole utilizzate con tale istruzione, è possibile visualizzare o copiare modelli di data mining oppure eseguire stime basate su tali modelli. La query di stima utilizza un modulo di selezione per creare stime basate su modelli di data mining esistenti. È inoltre possibile utilizzare funzioni per estendere oltre le capacità intrinseche del modello di data mining le funzionalità di esplorazione e per l'esecuzione di query sui modelli di data mining.  
  
 Le funzioni DMX consentono di calcolare nuove informazioni e di ottenere informazioni individuate durante il training dei modelli. È possibile utilizzare tali funzioni per vari scopi, inclusa la generazione di statistiche che descrivono i dati sottostanti o l'accuratezza di una stima oppure una descrizione dettagliata di una stima.  
  
 **Per ulteriori**  **informazioni:** [informazioni sull'istruzione DMX SELECT](../dmx/understanding-the-dmx-select-statement.md), sulle [funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), sulla [struttura e sull'utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md), [Data Mining Extensions &#40;DMX&#41; Function Reference](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
 [Torna a Istruzioni DMX](#BKMK_DMXStatements)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
