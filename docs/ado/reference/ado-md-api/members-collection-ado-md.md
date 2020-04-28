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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949438"
---
# <a name="members-collection-ado-md"></a>Raccolta Members (ADO MD)
Contiene gli oggetti [membro](../../../ado/reference/ado-md-api/member-object-ado-md.md) di un livello o di una posizione lungo un asse.  
  
## <a name="remarks"></a>Osservazioni  
 Una raccolta **Members** viene utilizzata per contenere i seguenti tipi di membri:  
  
-   Membri che costituiscono un livello in un cubo. Questi sono contenuti nella raccolta **Members** di un oggetto [Level](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Ad esempio, usando l'esempio da [Panoramica di schemi e dati multidimensionali](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md), i quattro membri del livello paesi sono Canada, USA, Regno Unito e Germania.  
  
-   Membri figlio di un membro specifico all'interno di una gerarchia. Questi membri vengono restituiti dalla proprietà [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) dell'oggetto **membro** padre. Ad esempio, usando di nuovo lo stesso esempio, i due figli del membro Canada sono Canada-Est e Canada-West.  
  
-   Membri che definiscono una posizione specifica lungo un asse di un insieme di [celle](../../../ado/reference/ado-md-api/cellset-object-ado-md.md). Se si usa un insieme di celle [con dati multidimensionali](../../../ado/guide/multidimensional/working-with-multidimensional-data.md) come esempio, i due membri della prima posizione sull'asse x sono Valentine e Seattle. Questi membri sono contenuti nella raccolta **Members** di un oggetto [position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
 **Members** è una raccolta ADO standard. Con le proprietà e i metodi di una raccolta, è possibile eseguire le operazioni seguenti:  
  
-   Ottenere il numero di oggetti nella raccolta con la proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
-   Restituisce un oggetto dalla raccolta con la proprietà dell' [elemento](../../../ado/reference/ado-api/item-property-ado.md) predefinito.  
  
-   Aggiornare gli oggetti della raccolta dal provider con il metodo [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) .  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/members-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di members (VBScript)](../../../ado/reference/ado-md-api/members-example-vbscript.md)   
 [Oggetto Member (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
