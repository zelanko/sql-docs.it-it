---
title: Oggetto Cellset (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9524e9801f284d3dff3125b850cdd1fd32a361a3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928641"
---
# <a name="cellset-object-ado-md"></a>Oggetto Cellset (ADO MD)
Rappresenta i risultati di una query multidimensionale. È una raccolta di celle selezionate da cubi o altri set di celle.  
  
## <a name="remarks"></a>Note  
 I dati all'interno di un **Cellset** vengono recuperati tramite accesso diretto di tipo matrice. È possibile eseguire il drill down un membro specifico per ottenere dati relativi a tale membro. Ad esempio, il codice seguente restituisce la didascalia del membro del primo in prima posizione del primo asse di un set di celle denominato `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Note  
 Non è prevista di una cella corrente all'interno di un set di celle. Al contrario, il [articoli](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) proprietà recupera una specifica [cella](../../../ado/reference/ado-md-api/cell-object-ado-md.md) oggetto dal set di celle. Gli argomenti del **elemento** proprietà determina quale cella viene recuperata. È possibile specificare il valore ordinale univoco di una cella. È inoltre possibile recuperare le celle con i numeri di posizione lungo ogni asse del set di celle. Per altre informazioni sul recupero delle celle, vedere la [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) proprietà.  
  
 Con le raccolte, i metodi e proprietà di un **Cellset** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Associare una connessione aperta con un **Cellset** oggetto impostando relativo [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) proprietà.  
  
-   Eseguire e recuperare i risultati di una query multidimensionale con il [aperto](../../../ado/reference/ado-md-api/open-method-ado-md.md) (metodo).  
  
-   Recuperare un **cella** dalle **Cellset** con il [elemento](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) proprietà.  
  
-   Restituire il [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md) oggetti che definiscono il **Cellset** con il [assi](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) raccolta.  
  
-   Recuperare le informazioni sulle dimensioni usate per filtrare i dati nel **Cellset** con il [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) proprietà.  
  
-   Restituire o specificare la query usata per definire le **Cellset** con il [origine](../../../ado/reference/ado-md-api/source-property-ado-md.md) proprietà.  
  
-   Restituire lo stato corrente della **Cellset** (aperte, chiuse, l'esecuzione o ci si connette) con il [stato](../../../ado/reference/ado-md-api/state-property-ado-md.md) proprietà.  
  
-   Chiudere un oggetto aperto **Cellset** con il [Chiudi](../../../ado/reference/ado-md-api/close-method-ado-md.md) (metodo).  
  
-   Recuperare informazioni specifiche del provider il **Cellset** con l'oggetto ADO standard [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Cellset (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Raccolta Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Oggetto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
