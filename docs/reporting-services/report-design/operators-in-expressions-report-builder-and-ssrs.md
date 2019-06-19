---
title: Operatori nelle espressioni (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3edfb8c885fbb8f7436f21271fc73d89599adfc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65582238"
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>Operatori nelle espressioni (Generatore report e SSRS)
  Un operatore è un simbolo che rappresenta le azioni applicate a uno o più termini di un'espressione. In un'espressione sono supportate le categorie di operatori seguenti: aritmetico, di confronto, di concatenazione, logico o bit per bit e di scorrimento bit.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>Aritmetico  
 Gli operatori aritmetici eseguono operazioni matematiche su due termini numerici in un'espressione.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|^|Eleva un numero alla potenza di un altro numero.|  
|*|Moltiplica due numeri.|  
|/|Divide due numeri e restituisce un risultato a virgola mobile.|  
|\|Divide due numeri e restituisce un risultato intero.|  
|Mod|Restituisce il resto intero di una divisione, ad esempio 7 Mod 5 = 2 perché il resto di 7 diviso 5 è 2.|  
|+|Somma due numeri.|  
|-|Restituisce la differenza tra due numeri o indica il valore negativo di un termine numerico.|  
  
### <a name="comparison"></a>Confronto  
 Gli operatori di confronto consentono di confrontare due espressioni.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|<|Minore di.|  
|\<=|Minore o uguale a.|  
|>|Maggiore di.|  
|>=|Maggiore o uguale a.|  
|=|Uguale a.|  
|<>|Diverso da.|  
|Simile a|Determina se una stringa di caratteri specifica corrisponde a un modello specificato. Il modello può contenere caratteri specifici e caratteri jolly. In una ricerca in base a un modello i normali caratteri devono corrispondere esattamente ai caratteri specificati nella stringa di caratteri del modello. I caratteri jolly tuttavia possono venire abbinati a frammenti arbitrari della stringa. L'utilizzo di caratteri jolly rende l'operatore LIKE più flessibile rispetto all'utilizzo degli operatori di confronto tra stringhe = e !=.<br /><br /> Nella tabella seguente sono elencati i caratteri che è possibile utilizzare come caratteri jolly:<br /><br /> %: qualsiasi stringa composta da zero o più caratteri.<br /><br /> _: qualsiasi carattere singolo.<br /><br /> [ ]: qualsiasi carattere singolo compreso nell'intervallo ([a-f]) o nel set ([aeiou]) specificato.<br /><br /> [^]: qualsiasi carattere singolo non compreso nell'intervallo ([^a-f]) o nel set ([^aeiou]) specificato|  
|Is|Confronta due riferimenti a oggetti.|  
  
### <a name="string-concatenation"></a>Concatenazione di stringhe  
 La concatenazione di stringhe aggiunge la seconda stringa alla prima in un'espressione. Per le altre operazioni con stringhe, utilizzare le funzioni predefinite.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|&|Concatena due stringhe|  
|+|Concatena due stringhe|  
  
### <a name="logical-and-bitwise"></a>Logico e bit per bit  
 Gli operatori logici e bit per bit eseguono modifiche logiche tra due termini interi in un'espressione.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|And|Esegue una congiunzione logica di due espressioni booleane oppure una congiunzione bit per bit di due espressioni numeriche.|  
|Not|Esegue una negazione logica di un'espressione booleana oppure una negazione bit per bit di un'espressione numerica.|  
|e|Esegue una disgiunzione logica di due espressioni booleane oppure una disgiunzione bit per bit di due valori numerici.|  
|Xor|Esegue un'operazione di esclusione logica di due espressioni booleane oppure un'esclusione bit per bit di due espressioni numeriche.|  
|AndAlso|Esegue una congiunzione logica di due espressioni.|  
|OrElse|Esegue una disgiunzione logica di due espressioni.|  
  
### <a name="bit-shift"></a>Scorrimento di bit  
 Gli operatori bit per bit eseguono modifiche di bit tra due termini interi in un'espressione.  
  
|Operatore|Descrizione|  
|--------------|-----------------|  
|<\<|Esegue uno scorrimento a sinistra aritmetico a sinistra in un modello di bit.|  
|>>|Esegue uno scorrimento a destra aritmetico in un modello di bit.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Espressione](https://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Finestra di dialogo dell'espressione &#40;Generatore report&#41;](https://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  
