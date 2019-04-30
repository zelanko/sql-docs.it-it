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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1e7e685e9d3f23d4d1c3317e24f63d7bdac23db
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180748"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Specifica le opzioni per aprire una [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto. I valori possono essere combinati con un'operazione OR.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Apre la **Stream** oggetto in modalità asincrona.|  
|**adOpenStreamFromRecord**|4|Identifica il contenuto del *origine* parametro sia una è già aperta [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto. Il comportamento predefinito consiste nel considerare *origine* sotto forma di URL che punta direttamente a un nodo in una struttura ad albero. Viene aperto il flusso predefinito associato a tale nodo.|  
|**adOpenStreamUnspecified**|-1|Valore predefinito. Specifica l'apertura il **Stream** oggetto con le opzioni predefinite.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Queste costanti non dispongono di equivalenti di ADO o WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)
