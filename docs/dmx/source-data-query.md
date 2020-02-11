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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892339"
---
# <a name="ltsource-data-querygt"></a>&lt;query sui dati di origine&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Per eseguire il training di un modello di data mining e creare stime da un modello di data mining, è necessario accedere ai dati [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] esterni al database. Per definire questi \<dati esterni, è possibile utilizzare la clausola> di query sui dati di origine in DMX (Data Mining Extensions). L'istruzione [Insert into &#40;DMX&#41;](../dmx/insert-into-dmx.md), [Select from &#60;Model&#62; prediction join &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)e [Select from natural prediction join](../dmx/select-from-model-prediction-join-dmx.md) all use ** \<source data query>**.  
  
## <a name="query-types"></a>Tipi di query  
 I tre modi più comuni per specificare i dati di origine sono i seguenti:  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 Questa istruzione consente di eseguire una query su dati esterni a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], utilizzando un'origine dei dati esistente.  
  
 Sebbene **OPENQUERY** funzioni in modo analogo a **OPENROWSET**, **OPENQUERY** offre i vantaggi seguenti:  
  
-   Una query DMX è molto più facile da scrivere con **OPENQUERY**. Anziché creare una nuova stringa di connessione ogni volta che si scrive una query, è possibile avvalersi della stringa di connessione esistente nell'origine dei dati. L'oggetto origine dei dati consente inoltre di controllare l'accesso ai dati per i singoli utenti.  
  
-   L'amministratore dispone di un maggiore controllo sulla modalità di accesso ai dati sul server. Può ad esempio stabilire quali provider caricare nel server e a quali dati esterni è possibile accedere.  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 Questa istruzione consente di eseguire una query su dati esterni a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], utilizzando un'origine dei dati esistente.  
  
 [FORMA &#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 Questa istruzione consente di eseguire query su più origini dei dati per creare una tabella nidificata. Utilizzando la **forma**è possibile combinare dati di più origini in una singola tabella gerarchica. In questo modo è possibile avvalersi della capacità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] di nidificare tabelle incorporando una tabella in un'altra tabella.  
  
 Per specificare i dati di origine è inoltre possibile utilizzare uno degli elementi seguenti:  
  
-   Qualsiasi istruzione DMX valida  
  
-   Qualsiasi istruzione MDX (Multidimensional Expressions) valida  
  
-   Una tabella che restituisce una stored procedure  
  
-   Un set di righe di XML for Analysis (XMLA)  
  
-   Un parametro di set di righe  
  
## <a name="see-also"></a>Vedere anche  
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Tabelle nidificate &#40;Analysis Services-&#41;di data mining](https://docs.microsoft.com/analysis-services/data-mining/nested-tables-analysis-services-data-mining)  
  
  
