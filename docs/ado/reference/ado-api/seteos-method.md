---
title: Metodo SetEos | Microsoft Docs
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
ms.openlocfilehash: 357778765f0c7ac59d924518340ca34226853fc0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916920"
---
# <a name="seteos-method"></a>Metodo SetEOS
Imposta la posizione che rappresenta la fine del flusso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Osservazioni  
 **SetEOS** aggiorna il valore della proprietà [EOS](../../../ado/reference/ado-api/eos-property.md) , rendendo la [posizione](../../../ado/reference/ado-api/position-property-ado.md) corrente la fine del flusso. Tutti i byte o i caratteri successivi alla posizione corrente vengono troncati.  
  
 Poiché [Write](../../../ado/reference/ado-api/write-method.md), [WRITETEXT](../../../ado/reference/ado-api/writetext-method.md)e [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) non troncano valori aggiuntivi negli oggetti **flusso** esistenti, è possibile troncare questi byte o caratteri impostando la nuova posizione di fine del flusso con **SetEOS**.  
  
> [!CAUTION]
>  Se si imposta **EOS** su una posizione prima della fine effettiva del flusso, si perderanno tutti i dati dopo la nuova posizione **EOS** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
