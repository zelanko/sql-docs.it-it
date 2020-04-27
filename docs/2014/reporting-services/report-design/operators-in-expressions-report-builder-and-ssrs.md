---
title: Operatori nelle espressioni (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cb4ea26e646453b3acd85a4f5e13ab9557f950fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105496"
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
|Simile a|Determina se una stringa di caratteri specifica corrisponde a un modello specificato. Il modello può contenere caratteri specifici e caratteri jolly. In una ricerca in base a un modello i normali caratteri devono corrispondere esattamente ai caratteri specificati nella stringa di caratteri del modello. I caratteri jolly tuttavia possono venire abbinati a frammenti arbitrari della stringa. L'utilizzo di caratteri jolly rende l'operatore LIKE più flessibile rispetto all'utilizzo degli operatori di confronto tra stringhe = e !=.<br /><br /> Di seguito sono elencati i caratteri che è possibile utilizzare come caratteri jolly:<br /><br /> **%**: Qualsiasi stringa di zero o più caratteri.<br /><br /> **_**: Qualsiasi carattere singolo.<br /><br /> **[]**: Qualsiasi carattere singolo compreso nell'intervallo specificato (ad esempio, [a-f]) o set (ad esempio, [aeiou]).<br /><br /> **[^]**: Qualsiasi carattere singolo non compreso nell'intervallo specificato (ad esempio, [^ a-f]) o set (ad esempio, [^ aeiou]).|  
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
|e|Esegue una congiunzione logica di due espressioni booleane oppure una congiunzione bit per bit di due espressioni numeriche.|  
|Not|Esegue una negazione logica di un'espressione booleana oppure una negazione bit per bit di un'espressione numerica.|  
|Oppure|Esegue una disgiunzione logica di due espressioni booleane oppure una disgiunzione bit per bit di due valori numerici.|  
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
 [Finestra di dialogo Espressione](../expression-dialog-box.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](data-types-in-expressions-report-builder-and-ssrs.md)   
 [Finestra di dialogo dell'espressione &#40;Generatore report&#41;](../expression-dialog-box-report-builder.md)  
  
  
