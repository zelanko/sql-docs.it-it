---
title: '&lt;query&gt; sui dati di origine | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e523d33da502a971b950e33ec0bd935149ed26f7
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892339"
---
# <a name="ltsource-data-querygt"></a>&lt;query sui dati di origine&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Per eseguire il training di un modello di data mining e creare stime da un modello di data mining, è necessario accedere ai dati [!INCLUDE[msCoName](../includes/msconame-md.md)] esterni al [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] database. Per definire questi \<dati esterni, è possibile utilizzare la clausola > di query sui dati di origine in DMX (Data Mining Extensions). Le istruzioni [Insert &#40;into&#41;DMX](../dmx/insert-into-dmx.md), [Select &#60;from&#62; Model Prediction &#40;join&#41;DMX](../dmx/select-from-model-prediction-join-dmx.md)e [Select from natural prediction join](../dmx/select-from-model-prediction-join-dmx.md) utilizzano **\<tutte query sui dati di origine >** .  
  
## <a name="query-types"></a>Tipi di query  
 I tre modi più comuni per specificare i dati di origine sono i seguenti:  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 Questa istruzione consente di eseguire una query su dati esterni a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], utilizzando un'origine dei dati esistente.  
  
 Sebbene **OPENQUERY** funzioni in modo analogo a **OPENROWSET**, **OPENQUERY** offre i vantaggi seguenti:  
  
-   Una query DMX è molto più facile da scrivere con **OPENQUERY**. Anziché creare una nuova stringa di connessione ogni volta che si scrive una query, è possibile avvalersi della stringa di connessione esistente nell'origine dei dati. L'oggetto origine dei dati consente inoltre di controllare l'accesso ai dati per i singoli utenti.  
  
-   L'amministratore dispone di un maggiore controllo sulla modalità di accesso ai dati sul server. Può ad esempio stabilire quali provider caricare nel server e a quali dati esterni è possibile accedere.  
  
 [DMX &#40;OPENROWSET&#41;](../dmx/source-data-query-openrowset.md)  
 Questa istruzione consente di eseguire una query su dati esterni a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], utilizzando un'origine dei dati esistente.  
  
 [DMX &#40;DI FORMA&#41;](../dmx/source-data-query-shape.md)  
 Questa istruzione consente di eseguire query su più origini dei dati per creare una tabella nidificata. Utilizzando la **forma**è possibile combinare dati di più origini in una singola tabella gerarchica. In questo modo è possibile avvalersi della capacità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] di nidificare tabelle incorporando una tabella in un'altra tabella.  
  
 Per specificare i dati di origine è inoltre possibile utilizzare uno degli elementi seguenti:  
  
-   Qualsiasi istruzione DMX valida  
  
-   Qualsiasi istruzione MDX (Multidimensional Expressions) valida  
  
-   Una tabella che restituisce una stored procedure  
  
-   Un set di righe di XML for Analysis (XMLA)  
  
-   Un parametro di set di righe  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di manipolazione &#40;dei&#41; dati DMX di Data Mining Extensions](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento &#40;alle&#41; istruzioni DMX di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Analysis Services di &#40;tabelle nidificate-data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
