---
title: StreamReadEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7700fc1ddc3cc619db224ac46006370898af1d62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928667"
---
# <a name="streamreadenum"></a>StreamReadEnum
Specifica se l'intero flusso o nella riga successiva deve essere letti da un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Valore predefinito. Legge e versioni successive a tutti i byte dal flusso, dalla posizione corrente di [EOS](../../../ado/reference/ado-api/eos-property.md) marcatore. Ciò è valido solo **StreamReadEnum** valore con flussi binari ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) viene **adTypeBinary**).|  
|**adReadLine**|-2|Legge la riga successiva dal flusso (definito dal [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) proprietà).|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Queste costanti non dispongono di equivalenti di ADO o WFC.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo Read](../../../ado/reference/ado-api/read-method.md)|[Metodo ReadText](../../../ado/reference/ado-api/readtext-method.md)|
