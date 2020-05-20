---
title: Proprietà di Update Resync-Dynamic (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: rothja
ms.author: jroth
ms.openlocfilehash: e9d000150cc86a8c838ac5dea827b5c376f3a79f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759487"
---
# <a name="update-resync-property-dynamic-ado"></a>Proprietà dinamica Update Resync (ADO)
Specifica se il metodo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) è seguito da un'operazione implicita di [Risincronizzazione](../../../ado/reference/ado-api/resync-method.md) del metodo e, in tal caso, dall'ambito di tale operazione.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce uno o più valori [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 È possibile combinare i valori di ADCPROP_UPDATERESYNC_ENUM, ad eccezione di adResyncAll, che rappresenta già la combinazione degli altri valori.  
  
 La costante **adResyncConflicts** archivia i valori di risincronizzazione come valori sottostanti, ma non esegue l'override delle modifiche in sospeso.  
  
 La **Risincronizzazione degli aggiornamenti** è una proprietà dinamica aggiunta alla raccolta delle [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) quando la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
