---
title: Metodo Open (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 089fad427989c26ed1ed22ec3e9267297a29b820
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949382"
---
# <a name="open-method-ado-md"></a>Metodo Open (ADO MD)
Recupera i risultati di una query multidimensionale e restituisce i risultati a un tipo di [cella](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativa. **Variante** che restituisce una query multidimensionale valida, ad esempio una query MDX (Multidimensional Expression). L'argomento di *origine* corrisponde alla proprietà di [origine](../../../ado/reference/ado-md-api/source-property-ado-md.md) . Per ulteriori informazioni su MDX, vedere la documentazione relativa alla [OLE DB per l'elaborazione analitica in linea (OLAP)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) in Microsoft Data Access Components SDK.  
  
 *ActiveConnection*  
 Facoltativa. **Variante** che restituisce una stringa che specifica un nome di variabile oggetto di [connessione](../../../ado/reference/ado-api/connection-object-ado.md) ADO o una definizione per una connessione. L'argomento *ActiveConnection* specifica la connessione in cui aprire l'oggetto [cellt](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) . Se si passa una definizione di connessione per questo argomento, ADO apre una nuova connessione usando i parametri specificati. L'argomento *ActiveConnection* corrisponde alla proprietà [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **Open** genera un errore se uno dei parametri viene omesso e il valore della proprietà corrispondente non è stato impostato prima di tentare di aprire il set di **celle**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di celle (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Proprietà ActiveConnection (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Metodo Close (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Proprietà Source (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [Proprietà State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
