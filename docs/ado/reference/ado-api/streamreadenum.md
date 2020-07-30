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
author: rothja
ms.author: jroth
ms.openlocfilehash: 92c599665548c36b8349290b02d197393f707fbf
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243192"
---
# <a name="streamreadenum"></a>StreamReadEnum
Specifica se l'intero flusso o la riga successiva devono essere letti da un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|Valore predefinito. Legge tutti i byte dal flusso, dalla posizione corrente verso l'indicatore [EOS](../../../ado/reference/ado-api/eos-property.md) . Si tratta dell'unico valore **StreamReadEnum** valido con flussi binari (il[tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) è **adTypeBinary**).|  
|**adReadLine**|-2|Legge la riga successiva dal flusso (designato dalla proprietà [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) ).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Read (metodo)](../../../ado/reference/ado-api/read-method.md)  
    :::column-end:::
    :::column:::
        [Metodo ReadText](../../../ado/reference/ado-api/readtext-method.md)  
    :::column-end:::
:::row-end:::
