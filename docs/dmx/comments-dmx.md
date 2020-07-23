---
title: Commenti (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 37e646df007684ee8e68f9d39119e42014415715
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/23/2020
ms.locfileid: "86969902"
---
# <a name="comments-dmx"></a>Commenti (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  I commenti in DMX (Data Mining Extensions) sono stringhe di testo nel codice del programma che [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non vengono eseguite. I commenti sono noti anche come osservazioni. È possibile utilizzare i commenti per documentare il codice o disabilitare temporaneamente parti di uno script o di un'istruzione DMX durante la diagnostica del codice.  
  
 Se si utilizzano i commenti per documentare il codice del programma, la successiva manutenzione del codice risulterà più semplice. È possibile utilizzare i commenti per registrare dettagli quali il nome del programma, il nome dello sviluppatore che ha scritto il codice e le date delle principali modifiche apportate al codice. È inoltre possibile utilizzare i commenti per descrivere calcoli complessi o un metodo di programmazione.  
  
 Di seguito sono riportate le linee guida di base per la scrittura dei commenti:  
  
-   In un commento è possibile utilizzare caratteri alfanumerici o simboli. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora tutti i caratteri all'interno di un commento.  
  
-   Per i commenti di uno script o istruzione non è prevista una lunghezza massima. Un commento può essere formato da una o più righe.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta gli indicatori di commento seguenti:  
  
-   **(barre doppie).** Usare questi caratteri di commento per scrivere un commento nella stessa riga di codice da eseguire oppure per scrivere un commento in una riga distinta. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera tutti i caratteri situati tra la barra doppia e la fine della riga come commento. Per creare commenti su più righe, specificare la barra doppia all'inizio di ogni riga di commento. Per ulteriori informazioni su questo carattere di commento, vedere la [barra doppia &#40;commento&#41; &#40;&#41;DMX ](../dmx/double-slash-comment-dmx.md).  
  
-   **--(trattini doppi).** Usare questi caratteri di commento per scrivere un commento nella stessa riga di codice da eseguire oppure per scrivere un commento in una riga distinta. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera tutti i caratteri situati tra il trattino doppio e la fine della riga come commento. Per creare commenti su più righe, specificare il trattino doppio all'inizio di ogni riga di commento. Per ulteriori informazioni su questo carattere di commento, vedere [&#40;commento&#41; &#40;riepilogo&#41; DMX](../dmx/comment-dmx-summary.md).  
  
-   **/\*... \* /(coppie di caratteri barra-asterisco).** Usare questi caratteri di commento per scrivere un commento nella stessa riga di codice da eseguire oppure per scrivere un commento in una riga distinta, o anche per scrivere commenti in un codice eseguibile. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]valuta tutti gli elementi dalla coppia di caratteri di apertura (/*) alla coppia di caratteri di chiusura ( \* /) come parte del commento. Per creare un commento su più righe, iniziare il commento con la coppia di caratteri di apertura del commento (/ \* ) e terminare il commento con la coppia di caratteri di chiusura del commento ( \* /). Nelle righe del commento non deve essere inserito nessun altro simbolo di commento. Per ulteriori informazioni su questo carattere di commento, vedere la pagina relativa al [Commento a Slash Star &#40;&#41; &#40;&#41;DMX ](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle estensioni di data mining &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Guida di riferimento alle funzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Guida di riferimento agli operatori DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)   
 [Data Mining Extensions &#40;le convenzioni della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Data Mining Extensions &#40;elementi della sintassi DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generali &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
