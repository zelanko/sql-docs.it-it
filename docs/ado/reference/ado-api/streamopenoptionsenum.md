---
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 1d61b11ee6fedd4229433570f6b159cccf658853
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759587"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Specifica le opzioni per l'apertura di un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) . I valori possono essere combinati con un'operazione OR.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Apre l'oggetto **flusso** in modalità asincrona.|  
|**adOpenStreamFromRecord**|4|Identifica il contenuto del parametro di *origine* come oggetto [record](../../../ado/reference/ado-api/record-object-ado.md) già aperto. Il comportamento predefinito consiste nel considerare *source* come un URL che punta direttamente a un nodo in una struttura ad albero. Viene aperto il flusso predefinito associato al nodo.|  
|**adOpenStreamUnspecified**|-1|Valore predefinito. Specifica l'apertura dell'oggetto **flusso** con le opzioni predefinite.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
