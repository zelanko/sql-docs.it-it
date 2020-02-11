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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67928667"
---
# <a name="streamreadenum"></a>StreamReadEnum
Specifica se l'intero flusso o la riga successiva devono essere letti da un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Default. Legge tutti i byte dal flusso, dalla posizione corrente verso l'indicatore [EOS](../../../ado/reference/ado-api/eos-property.md) . Si tratta dell'unico valore **StreamReadEnum** valido con flussi binari (il[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeBinary**).|  
|**adReadLine**|-2|Legge la riga successiva dal flusso (designato dalla proprietà [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) ).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo Read](../../../ado/reference/ado-api/read-method.md)|[Metodo ReadText](../../../ado/reference/ado-api/readtext-method.md)|
