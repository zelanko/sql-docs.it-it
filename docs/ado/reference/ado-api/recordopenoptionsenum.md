---
title: RecordOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordOpenOptionsEnum
helpviewer_keywords:
- RecordOpenOptionsEnum enumeration [ADO]
ms.assetid: 9028aba4-90fc-4dfc-88e4-fa8a7b6fedee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba165d51dde5224dac65467061eac0d38aeefc7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931422"
---
# <a name="recordopenoptionsenum"></a>RecordOpenOptionsEnum
Specifica le opzioni per l'apertura di un [record](../../../ado/reference/ado-api/record-object-ado.md). Questi valori possono essere combinati usando o.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adDelayFetchFields**|0x8000|Indica al provider che i campi associati al **record** non devono essere recuperati inizialmente, ma possono essere recuperati al primo tentativo di accesso al campo. Il comportamento predefinito, indicato dall'assenza di questo flag, consiste nel recuperare tutti i campi dell'oggetto **record** .|  
|**adDelayFetchStream**|0x4000|Indica al provider che non è necessario recuperare inizialmente il flusso predefinito associato al **record** . Il comportamento predefinito, indicato dall'assenza di questo flag, consiste nel recuperare il flusso predefinito associato all'oggetto **record** .|  
|**adOpenAsync**|0x1000|Indica che l'oggetto **record** viene aperto in modalità asincrona.|  
|**adOpenExecuteCommand**|0x10000|Indica che la stringa di origine contiene il testo del comando da eseguire. Questo valore è equivalente all'opzione **adCmdText** in **Recordset. Open**.|  
|**adOpenRecordUnspecified**|-1|Default. Indica che non è specificata alcuna opzione.|  
|**adOpenOutput**|0x800000|Indica che se l'origine punta a un nodo che contiene uno script eseguibile, ad esempio. Pagina ASP), il **record** aperto conterrà i risultati dello script eseguito. Questo valore è valido solo con record non di raccolta.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (Record - ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
