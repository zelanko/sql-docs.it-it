---
title: Funzionalità supportate dalle edizioni di SQL Server di Analysis Services | Microsoft Docs
ms.date: 06/25/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9947b10e01864f66bf26d6599e43814ab37dadc6
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388213"
---
# <a name="analysis-services-features-supported-by-sql-server-edition"></a>Funzionalità di Analysis Services supportate dall'edizione di SQL Server
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

Questo articolo descrive le funzionalità supportate dalle diverse edizioni di SQL Server 2016, 2017 2019 Analysis Services. Versione di valutazione supporta le funzionalità dell'edizione Enterprise.

## <a name="analysis-services-servers"></a>Analysis Services (server)
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Sviluppatore|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Database condivisi scalabili|Yes||||||Yes|  
|Backup/ripristino e collegamento/scollegamento di database|Yes|Yes|||||Yes|  
|Sincronizzare database|Yes||||||Yes|  
|Istanze del cluster di failover Always On|Yes<br /><br /> Il numero di nodi è il valore massimo del sistema operativo|Yes<br /><br /> Supporto per 2 nodi|||||Yes<br /><br /> Il numero di nodi è il valore massimo del sistema operativo|  
|Programmabilità (AMO, ADOMD.Net, OLEDB, XML/A, ASSL, TMSL)|Yes|Yes|||||Yes|  
  
## <a name="tabular-models"></a>Modelli tabulari 
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Sviluppatore|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Gerarchie|Yes|Yes|||||Yes|  
|KPI|Yes|Yes|||||Yes|  
|prospettive|Yes||||||Yes|  
|Traduzioni|Yes|Yes|||||Yes|  
|Calcoli DAX, query DAX, query MDX|Yes|Yes|||||Yes|  
|Sicurezza a livello di riga|Yes|Yes|||||Yes|  
|Più partizioni|Yes||||||Yes|  
|Gruppi di calcolo|Sì (che inizia con SQL Server 2019)|Sì (che inizia con SQL Server 2019)|||||Sì (che inizia con SQL Server 2019)|  
|Modalità di archiviazione in memoria|Yes|Yes|||||Yes|  
|Modalità DirectQuery|Yes|Sì (che inizia con SQL Server 2019)|||||Yes|  

## <a name="multidimensional-models"></a>Modelli multidimensionali 
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Sviluppatore|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Misure semiadditive|Yes|No <sup>1</sup>|||||Yes|  
|Gerarchie|Yes|Yes|||||Yes|  
|KPI|Yes|Yes|||||Yes|  
|prospettive|Yes||||||Yes|  
|Azioni|Yes|Yes|||||Yes|  
|Funzionalità di Business Intelligence per la contabilità|Yes|Yes|||||Yes|  
|Business Intelligence per gerarchie temporali|Yes|Yes|||||Yes|  
|Rollup personalizzati|Yes|Yes|||||Yes|  
|Cubo writeback|Yes|Yes|||||Yes|  
|Dimensioni writeback|Yes||||||Yes|  
|Celle writeback|Yes|Yes|||||Yes|  
|Drill-through|Yes|Yes|||||Yes|  
|Tipi di gerarchia avanzati (padre-figlio e gerarchie incomplete)|Yes|Yes|||||Yes|  
|Dimensioni avanzate (dimensioni di riferimento, dimensioni molti-a-molti)|Yes|Yes|||||Yes|  
|Dimensioni e misure collegate|Yes|Sì  <sup>2</sup> |||||Yes|  
|Traduzioni|Yes|Yes|||||Yes|  
|Aggregations|Yes|Yes|||||Yes|  
|Più partizioni|Yes|Sì, fino a 3|||||Yes|  
|Memorizzazione nella cache attiva|Yes||||||Yes|  
|Assembly personalizzati (stored procedure)|Yes|Yes|||||Yes|  
|Query e script MDX|Yes|Yes|||||Yes|  
|Query DAX|Yes|Yes|||||Yes|  
|Modello di sicurezza basato su ruoli|Yes|Yes|||||Yes|  
|Sicurezza a livello di cella e dimensione|Yes|Yes|||||Yes|  
|Archivio di stringhe scalabile|Yes|Yes|||||Yes|  
|Modelli di archiviazione MOLAP, ROLAP e HOLAP|Yes|Yes|||||Yes|  
|Trasporto XML binario e compresso|Yes|Yes|||||Yes|  
|Elaborazione in modalità push|Yes||||||Yes|  
|Espressioni di misura|Yes||||||Yes|  
  
 <sup>1</sup> La misura semiadattiva LastChild è supportata nell'edizione Standard, mentre altre misure semiadattive come None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren e ByAccount non lo sono. Le misure additive, ad esempio Sum, Count, Min, Max e quelle non additive (DistinctCount) sono supportate in tutte le edizioni.  
  <sup>2</sup> L'edizione Standard supporta il collegamento di misure e dimensioni all'interno dello stesso database, ma non da altri database o istanze.
  
## <a name="power-pivot-for-sharepoint"></a>PowerPivot per SharePoint  
  
|Funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Sviluppatore|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Integrazione di farm SharePoint basata sull'architettura di servizi condivisi|Yes||||||Yes|  
|Report sull'utilizzo|Yes||||||Yes|  
|Regole di monitoraggio dell'integrità|Yes||||||Yes|  
|Raccolta Power Pivot|Yes||||||Yes|  
|Aggiornamento dati Power Pivot|Yes||||||Yes|  
|Feed di dati Power Pivot|Yes||||||Yes|  
  
## <a name="data-mining"></a>Data Mining  
  
|Nome funzionalità|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|Sviluppatore|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|Algoritmi standard|Yes|Yes|||||Yes|  
|Strumenti di data mining (procedure guidate, editor, generatori di query)|Yes|Yes|||||Yes|  
|Convalida incrociata|Yes||||||Yes|  
|Modelli in base a subset filtrati di dati della struttura di data mining|Yes||||||Yes|  
|Serie temporale: Combinazione personalizzata tra metodi ARTXP e ARIMA|Yes||||||Yes|  
|Serie temporale: Stima con nuovi dati|Yes||||||Yes|  
|Query di data mining simultanee illimitate|Yes||||||Yes|  
|Opzioni di configurazione e ottimizzazione avanzate per algoritmi di data mining|Yes||||||Yes|  
|Supporto per algoritmi plug-in|Yes||||||Yes|  
|Elaborazione parallela dei modelli|Yes||||||Yes|  
|Time Series: stima incrociata tra serie|Yes||||||Yes|  
|Attributi illimitati per le regole di associazione|Yes||||||Yes|  
|Stima basata su sequenze|Yes||||||Yes|  
|Più destinazioni di stima per gli algoritmi Logistic Regression, Neural Network e Naïve Bayes|Yes||||||Yes|  
  


