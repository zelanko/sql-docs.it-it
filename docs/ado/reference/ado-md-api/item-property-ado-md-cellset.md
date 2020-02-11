---
title: Proprietà Item (ADO MD Cellt) | Microsoft Docs
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
ms.openlocfilehash: 0c7fbce544cac188db7ed3b3d40478aa63809405
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949628"
---
# <a name="item-property-ado-md-cellset"></a>Proprietà Item (Cellset - ADO MD)
Recupera una cella da un oggetto [Cell](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) usando le coordinate.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parametri  
 *Posizioni*  
 **VariantArray** di valori che specificano una cella in modo univoco. Le *posizioni* possono essere una delle seguenti:  
  
-   Matrice di numeri di posizione  
  
-   Matrice di nomi di membri  
  
-   Posizione ordinale  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Item** per restituire un oggetto [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md) all'interno di un oggetto [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) . Se la proprietà **Item** non riesce a trovare la cella corrispondente all'argomento *Positions* , si verificherà un errore.  
  
 La proprietà **Item** è la proprietà predefinita per l'oggetto **cellt** . I formati di sintassi seguenti sono intercambiabili:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>Osservazioni  
 L'argomento *Positions* specifica la cella da restituire. È possibile specificare la cella in base alla posizione ordinale o alla posizione lungo ogni asse. Quando si specifica la cella per posizione lungo ogni asse, è possibile specificare il valore numerico della posizione o i nomi dei membri per ogni posizione.  
  
 La posizione ordinale è un numero che identifica in modo univoco una cella all'interno del **celle**. Dal punto di vista concettuale, le celle sono numerate in un insieme di **celle** come se il numero di **celle** fosse una matrice *p*-dimensionale, dove *p* è il numero di assi. Le celle sono indirizzate in ordine di riga. Di seguito è riportata la formula per il calcolo del numero ordinale di una cella:  
  
 Se i nomi dei membri vengono passati come stringhe all' **elemento**, i membri devono essere elencati in ordine crescente degli identificatori dell'asse numerico. All'interno di un asse, i membri devono essere elencati in ordine crescente di annidamento delle dimensioni, ovvero il membro della dimensione più esterna viene innanzitutto seguito da membri di dimensioni interne. Ogni dimensione deve essere rappresentata da una stringa separata e l'elenco di stringhe membro deve essere separato da virgole.  
  
> [!NOTE]
>  Il recupero di celle in base al nome del membro potrebbe non essere supportato dal provider di dati. Per ulteriori informazioni, vedere la documentazione relativa al provider.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
