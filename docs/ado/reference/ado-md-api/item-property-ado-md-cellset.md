---
title: Elemento proprietà (Cellset-ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 641a08567e990134d49d32ae7ebecaf7d2b8de5a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533088"
---
# <a name="item-property-ado-md-cellset"></a>Proprietà Item (Cellset - ADO MD)
Recupera una cella da un [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) utilizzando le coordinate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parametri  
 *Posizioni*  
 Oggetto **VariantArray** di valori che specificano in modo univoco una cella. *Le posizioni* può essere uno dei seguenti:  
  
-   Una matrice di numeri di posizione  
  
-   Una matrice di nomi di membro  
  
-   La posizione ordinale  
  
## <a name="remarks"></a>Note  
 Usare il **elemento** proprietà da restituire una [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md) dell'oggetto all'interno di un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto. Se il **elemento** proprietà non è possibile trovare la cella corrispondente il *posizioni* si verifica un errore di argomento.  
  
 Il **elemento** proprietà è la proprietà predefinita per il **Cellset** oggetto. Le seguenti forme di sintassi sono intercambiabili tramite:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>Note  
 Il *posizioni* argomento specifica la cella da restituire. È possibile specificare la cella in base alla posizione ordinale o dalla posizione lungo ogni asse. Quando si specifica la cella in base alla posizione lungo ogni asse, è possibile specificare il valore numerico della posizione o i nomi dei membri per ogni posizione.  
  
 La posizione ordinale è un numero che identifica in modo univoco una cella all'interno di **Cellset**. Concettualmente, le celle sono numerate in un **Cellset** come se il **Cellset** sono stati un *p*-matrice dimensionale, dove *p* è il numero di assi. Le celle sono indirizzate in ordine di riga. Di seguito è la formula per calcolare il numero ordinale di una cella:  
  
 Se i nomi dei membri vengono passati come stringhe a **elemento**, i membri devono essere elencati in ordine crescente di identificatori numerici dell'asse. All'interno di un asse, i membri devono essere elencati in ordine crescente di nidificazione di dimensione, vale a dire, membro della dimensione più esterna viene raggiunto per primo, seguiti dai membri delle dimensioni interne. Ogni dimensione deve essere rappresentato da una stringa distinta, e l'elenco di stringhe di membro deve essere separato da virgole.  
  
> [!NOTE]
>  Il recupero di celle in base al nome di membro non può essere supportato da provider di dati. Vedere la documentazione per il provider per altre informazioni.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
