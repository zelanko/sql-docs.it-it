---
title: Commenti (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f319457da85378000ef974c3ace1ddbba87d18e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62709088"
---
# <a name="comments-dmx"></a>Commenti (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  I commenti nel Data Mining Extensions (DMX) sono stringhe di testo in programma il codice [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] non viene eseguito. I commenti sono noti anche come osservazioni. È possibile utilizzare i commenti per documentare il codice o disabilitare temporaneamente parti di uno script o di un'istruzione DMX durante la diagnostica del codice.  
  
 Se si utilizzano i commenti per documentare il codice del programma, la successiva manutenzione del codice risulterà più semplice. È possibile utilizzare i commenti per registrare dettagli quali il nome del programma, il nome dello sviluppatore che ha scritto il codice e le date delle principali modifiche apportate al codice. È inoltre possibile utilizzare i commenti per descrivere calcoli complessi o un metodo di programmazione.  
  
 Di seguito sono riportate le linee guida di base per la scrittura dei commenti:  
  
-   In un commento è possibile utilizzare caratteri alfanumerici o simboli. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora tutti i caratteri all'interno di un commento.  
  
-   Per i commenti di uno script o istruzione non è prevista una lunghezza massima. Un commento può essere formato da una o più righe.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] supporta gli indicatori di commento seguenti:  
  
-   **(barra doppia).** Usare questi caratteri di commento per scrivere un commento nella stessa riga di codice da eseguire oppure per scrivere un commento in una riga distinta. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera tutti i caratteri situati tra la barra doppia e la fine della riga come commento. Per creare commenti su più righe, specificare la barra doppia all'inizio di ogni riga di commento. Per altre informazioni su questo indicatore di commento, vedere [barre doppie &#40;commento&#41; &#40;DMX&#41;](../dmx/double-slash-comment-dmx.md).  
  
-   **-(trattino doppio).** Usare questi caratteri di commento per scrivere un commento nella stessa riga di codice da eseguire oppure per scrivere un commento in una riga distinta. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] considera tutti i caratteri situati tra il trattino doppio e la fine della riga come commento. Per creare commenti su più righe, specificare il trattino doppio all'inizio di ogni riga di commento. Per altre informazioni su questo indicatore di commento, vedere [- &#40;commento&#41; &#40;DMX&#41; riepilogo](../dmx/comment-dmx-summary.md).  
  
-   **/\* ... \*/ (barra-asterisco coppia di caratteri).** Usare questi caratteri di commento per scrivere un commento nella stessa riga di codice da eseguire oppure per scrivere un commento in una riga distinta, o anche per scrivere commenti in un codice eseguibile. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] situati tra la coppia di caratteri di commento Apri (/ *) per la coppia di chiusura del commento (\*/) come parte del commento. Per creare un commento su più righe, iniziare il commento con la coppia di caratteri di apertura del commento (/\*) e terminarlo con la coppia di caratteri di chiusura del commento (\*/). Nelle righe del commento non deve essere inserito nessun altro simbolo di commento. Per altre informazioni su questo indicatore di commento, vedere [barra asterisco &#40;commento&#41; &#40;DMX&#41;](../dmx/slash-star-comment-dmx.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle funzioni](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; di riferimento agli operatori](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; riferimento alle istruzioni](../dmx/data-mining-extensions-dmx-statements.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; convenzioni della sintassi](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Le estensioni di Data Mining di dati &#40;DMX&#41; gli elementi della sintassi](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funzioni di stima generale &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Struttura e utilizzo di query di stima DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Informazioni sull'istruzione DMX Select](../dmx/understanding-the-dmx-select-statement.md)  
  
  
