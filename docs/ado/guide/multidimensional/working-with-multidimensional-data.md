---
title: Utilizzo dei dati multidimensionali | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a284254c058eae0362fe23860e1b406a97f0bf49
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507252"
---
# <a name="working-with-multidimensional-data"></a>Utilizzo dei dati multidimensionali
Oggetto *cellset* è il risultato di una query sui dati multidimensionali. È costituito da una raccolta di assi, in genere non più di quattro assi e in genere solo due o tre. Un' *asse* è una raccolta di membri di uno o più dimensioni, che consente di individuare o filtrare i valori specifici in un cubo.  
  
 Oggetto *posizione* è un punto lungo un asse. Per un asse è costituito da una singola dimensione, queste posizioni sono un subset di membri della dimensione. Se un asse è costituito da più di una dimensione, quindi ogni posizione è un'entità composta che contiene *n* parti where *n* è il numero di dimensioni orientati lungo l'asse. Ogni parte della posizione è un membro da una dimensione che lo costituiscono.  
  
 Ad esempio, se le dimensioni di geografia e prodotto da un cubo contenente i dati di vendita sono orientate lungo l'asse x di un set di celle, una posizione dell'asse può contenere membri "USA" e "Computer". In questo esempio, per stabilire una posizione lungo l'asse x è necessario che i membri da ogni dimensione sono orientati lungo l'asse.  
  
 Oggetto *cella* è un oggetto posizionato in corrispondenza dell'intersezione delle coordinate dell'asse. Ogni cella dispone di più parti di informazioni associate, tra cui i dati stessi, una stringa formattata (visualizzabile forma dei dati delle celle) e il valore ordinale della cella. (Ogni cella è un valore ordinale univoco nel set di celle. Il valore ordinale della prima cella nel set di celle è zero, mentre la cella a sinistra nella seconda riga di un set di celle con otto colonne avrebbe un valore ordinale pari a otto.)  
  
 Ad esempio, un cubo con le sei dimensioni seguenti (si noti che questo schema cubo differisce leggermente dall'esempio considerato [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   Venditore  
  
-   Geography (gerarchia naturale) - continenti, paesi, stati e così via  
  
-   Trimestri-trimestri, mesi, giorni  
  
-   Years  
  
-   Misure: vendite, valori, VenditePreviste  
  
-   Products  
  
 Il set di celle seguente rappresenta le vendite per 1991 per tutti i prodotti:  
  
> [!NOTE]
>  I valori delle celle nell'esempio possono essere considerati come coppia ordinata di numeri ordinali di posizione dell'asse in cui la prima cifra rappresenta la posizione dell'asse x e la seconda cifra alla posizione di asse y.  
  
 Come indicato di seguito sono riportate le caratteristiche di questo set di celle:  
  
-   Dimensioni dell'asse: Trimestri, venditore, Geography  
  
-   Dimensioni di filtro: Le misure, anni, i prodotti  
  
-   Due assi: COLONNA (x o asse 0) e riga (y, o asse 1)  
  
-   asse x: due dimensioni nidificate, venditore e area geografica  
  
-   asse y: Dimensione trimestri  
  
 L'asse x dispone di due dimensioni annidate: Venditore e area geografica. Da geografia, sono selezionati quattro membri: Seattle, Boston, Stati Uniti-meridionale e Giappone. Dall'agente sono selezionati due membri: San Valentino e Nash. Ciò produce un totale di otto posizioni in questo asse (4 * 8 = 2).  
  
 Ogni coordinata è rappresentato come una posizione con due membri: uno dalla dimensione di venditore e l'altro della dimensione Geografia:  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 L'asse y contiene solo una dimensione, che contiene otto posizioni riportate di seguito:  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 Set di celle, le celle, assi e le posizioni sono tutti rappresentate in ADO MD dagli oggetti corrispondenti: [Set di celle](../../../ado/reference/ado-md-api/cellset-object-ado-md.md), [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), e [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modello a oggetti ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO (multidimensionale) (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programmazione con ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Uso di ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
