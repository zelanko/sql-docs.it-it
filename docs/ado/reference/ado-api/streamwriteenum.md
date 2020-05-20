---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 479bc032cf779752f11dccca73ee56fc05a8ebdd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759567"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Specifica se un separatore di riga viene aggiunto alla stringa scritta in un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Valore predefinito. Scrive la stringa di testo specificata (specificata dal parametro *dati* ) nell'oggetto **flusso** .|  
|**adWriteLine**|1|Scrive una stringa di testo e un carattere separatore di riga in un oggetto **flusso** . Se la proprietà [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) non è definita, viene restituito un errore di run-time.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo WriteText](../../../ado/reference/ado-api/writetext-method.md)
