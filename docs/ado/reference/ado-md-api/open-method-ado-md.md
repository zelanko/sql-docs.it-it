---
title: Metodo (ADO MD) Open | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: e22ab07f40ad6b4ef916d950909957b04c9d5be1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708712"
---
# <a name="open-method-ado-md"></a>Metodo Open (ADO MD)
Recupera i risultati di una query multidimensionale e restituisce i risultati in un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativo. Oggetto **Variant** che restituisce una query multidimensionale valida, ad esempio una query MDX (Multidimensional Expression). Il *origine* argomento corrispondente per il [origine](../../../ado/reference/ado-md-api/source-property-ado-md.md) proprietà. Per altre informazioni su MDX, vedere la [OLE DB per Online Analytical Processing (OLAP)](https://msdn.microsoft.com/8a7673c6-3ca1-4411-9f1e-adf1e47df4f3) documentazione in Microsoft Data Access Components SDK.  
  
 *ActiveConnection*  
 Facoltativo. Oggetto **Variant** che restituisce una stringa che specifica un valido ADO [connessione](../../../ado/reference/ado-api/connection-object-ado.md) nome di variabile o una definizione per una connessione dell'oggetto. Il *ActiveConnection* argomento specifica la connessione in cui aprire il [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) oggetto. Se si passa una definizione della connessione per questo argomento, ADO apre una nuova connessione utilizzando i parametri specificati. Il *ActiveConnection* argomento corrispondente per il [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) proprietà.  
  
## <a name="remarks"></a>Note  
 Il **apre** metodo genera un errore se viene omesso uno dei relativi parametri e il valore della proprietà corrispondente non è stato impostato prima di tentare di aprire le **Cellset**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Cellset (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Proprietà ActiveConnection (ADO MD)](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)   
 [Close (metodo) (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Proprietà Source (ADO MD)](../../../ado/reference/ado-md-api/source-property-ado-md.md)   
 [Proprietà State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
