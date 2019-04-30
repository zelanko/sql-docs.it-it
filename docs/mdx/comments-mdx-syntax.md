---
title: Commenti (sintassi MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17693d0dc76dd6cb8b3a4d0c3ead9f95c0599580
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181559"
---
# <a name="comments-mdx-syntax"></a>Commenti (sintassi MDX)


  I commenti sono stringhe di testo contenute nel codice di un programma ma che non vengono eseguite . È possibile utilizzare i commenti per documentare il codice o disabilitare temporaneamente parti di un'istruzione MDX (Multidimensional Expressions) o di uno script durante la diagnostica del codice. Se si utilizzano i commenti per documentare il codice, la successiva manutenzione del codice risulterà più semplice. I commenti vengono in genere utilizzati per registrare dettagli quali il nome del programma, il nome dell'autore e le date delle principali modifiche apportate al codice. È inoltre possibile utilizzare i commenti per descrivere calcoli complessi o illustrare un metodo di programmazione.  
  
 Di seguito sono riportate le linee guida per l'utilizzo dei commenti in MDX:  
  
-   In un commento è possibile utilizzare qualsiasi carattere alfanumerico o simbolo.  Tutti i caratteri all'interno di un commento vengono ignorati.  
  
-   Per i commenti di uno script o istruzione non è prevista una lunghezza massima. Un commento può essere formato da una o più righe.  
  
 MDX supporta gli indicatori di commento seguenti:  
  
 // (barra doppia)  
 Questo indicatore di commento può essere utilizzato sulla stessa riga del codice da eseguire o su una riga a parte. Tutti i caratteri situati tra la barra doppia e la fine della riga vengono trattati come commento. Per commenti su più righe, specificare la barra doppia all'inizio di ogni riga di commento. Per altre informazioni, vedere [ &#40;commento&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md).  
  
 -- (trattino doppio)  
 Questo indicatore di commento può essere utilizzato sulla stessa riga del codice da eseguire o su una riga a parte. Tutti i caratteri situati tra il trattino doppio e la fine della riga vengono trattati come commento. Per commenti su più righe, specificare il trattino doppio all'inizio di ogni riga di commento. Per altre informazioni, vedere [- &#40;commento&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md).  
  
 /* ... \*/ (barra-asterisco coppia di caratteri)  
 Questo indicatore di commento può essere utilizzato sulla stessa riga del codice da eseguire, su una riga a parte o all'interno del codice eseguibile. Tutti gli elementi della coppia di commenti di apertura (/\*) per la coppia di chiusura del commento (\*/) è considerato parte del commento. Per commenti su più righe, la coppia di caratteri di apertura del commento (/\*) deve iniziare il commento e la coppia di caratteri di chiusura del commento (\*/) deve terminare il commento. Nelle righe del commento non deve essere inserito nessun altro simbolo di commento. Per altre informazioni, vedere [/ *... \*/ (Commento)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>Esempio  
 Nella query seguente vengono illustrati esempi dei tre tipi di commento:  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi della sintassi MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
