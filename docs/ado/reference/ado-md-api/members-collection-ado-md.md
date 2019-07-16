---
title: Raccolta Members (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Members
- Members
- Position::Members
helpviewer_keywords:
- Members collection [ADO MD]
ms.assetid: 3a647cde-efdc-4394-b1b9-8cbb1b9d689f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79394abee5b12bb10f34a34e882d2ac0562722fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949438"
---
# <a name="members-collection-ado-md"></a>Raccolta Members (ADO MD)
Contiene il [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) oggetti da un livello o una posizione lungo un asse.  
  
## <a name="remarks"></a>Note  
 Oggetto **membri** raccolta viene usata per contenere i seguenti tipi di membri:  
  
-   I membri che costituiscono un livello in un cubo. Sono contenute nel **membri** raccolta di un [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) oggetto. Ad esempio, usando l'esempio dal [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), i quattro membri del livello paesi sono negli Stati Uniti, il Canada, Regno Unito e Germania.  
  
-   I membri che sono figli di un membro specifico all'interno di una gerarchia. Questi membri vengono restituiti per il [figli](../../../ado/reference/ado-md-api/children-property-ado-md.md) proprietà dell'elemento padre **membro** oggetto. Ad esempio, Canada orientale e Canada-occidentale utilizzando nuovamente lo stesso esempio, sono due figli del membro Canada.  
  
-   I membri che definiscono una specifica posizione lungo un asse di una [cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Usando il set di celle da [utilizzo dei dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) ad esempio, i due membri della prima posizione sull'asse x sono San Valentino e Seattle. Questi membri sono inclusi i **membri** raccolta di un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md) oggetto.  
  
 **I membri** è un insieme standard di ADO. Con le proprietà e metodi di una raccolta, è possibile eseguire le operazioni seguenti:  
  
-   Ottenere il numero di oggetti nella raccolta con il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà.  
  
-   Restituisce un oggetto dalla raccolta con il valore predefinito [elemento](../../../ado/reference/ado-api/item-property-ado.md) proprietà.  
  
-   Aggiornare gli oggetti nella raccolta dal provider con il [Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md) (metodo).  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Members (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
