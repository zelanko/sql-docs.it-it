---
title: Aggiornare la risincronizzazione proprietà dinamica (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed0e3ad8027c31a351ddb4506d3b420aa3a1124d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938800"
---
# <a name="update-resync-property-dynamic-ado"></a>Proprietà dinamica Update Resync (ADO)
Specifica se il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodo è seguito da implicita [Risincronizza](../../../ado/reference/ado-api/resync-method.md) operazione del metodo e in questo caso, l'ambito di tale operazione.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce uno o più i [ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md) valori.  
  
## <a name="remarks"></a>Note  
 I valori di ADCPROP_UPDATERESYNC_ENUM possono essere combinati, tranne adResyncAll che rappresenta già la combinazione del resto dei valori.  
  
 La costante **adResyncConflicts** archivia i valori di risincronizzazione come valori sottostanti, ma non esegue l'override delle modifiche in sospeso.  
  
 **Aggiornare risincronizzazione** viene aggiunta una proprietà dinamica per il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta quando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
