---
title: Metodo SetEOS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 027468926d444b25e60ede18bbfb26ff7cedf729
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711407"
---
# <a name="seteos-method"></a>Metodo SetEOS
Imposta la posizione che rappresenta la fine del flusso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Note  
 **SetEOS** aggiorna il valore della [EOS](../../../ado/reference/ado-api/eos-property.md) proprietà, rendendo corrente [posizione](../../../ado/reference/ado-api/position-property-ado.md) la fine del flusso. Qualsiasi byte o caratteri che seguono la posizione corrente vengono troncati.  
  
 In quanto [scrivere](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md), e [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) troncano i valori aggiuntivi esistente **Stream** oggetti, è possibile troncare questi byte o caratteri impostando la nuova posizione finale del flusso con **SetEOS**.  
  
> [!CAUTION]
>  Se si imposta **EOS** in una posizione prima della fine del flusso effettiva, si perderanno tutti i dati dopo che il nuovo **EOS** posizione.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
