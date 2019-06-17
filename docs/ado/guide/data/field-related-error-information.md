---
title: Informazioni sugli errori associati ai campi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e18698d7fba50ce6a63938df574408367b8b20cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702017"
---
# <a name="field-related-error-information"></a>Informazioni sugli errori correlati ai campi
Se un errore è direttamente correlato a un campo, ad esempio, se i dati sono mancanti o se è di tipo non corretto per il campo - è possibile recuperare altre informazioni sulla causa del problema esaminando la **campo** dell'oggetto **stato**  proprietà. Questa proprietà è stata migliorata per fornire informazioni specifiche relative al problema. In questo caso, ad esempio, quando una chiamata a **UpdateBatch** ha esito negativo, la causa del problema può essere determinata esaminando la **stato** proprietà del **campi** in ognuna dell'interessati record. La proprietà conterrà uno dei valori di **FieldStatusEnum** costante. La tabella seguente include i valori che sono di particolare interesse quando si verifica un errore.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica che il campo non può essere recuperato o archiviato senza perdita di dati.|  
|**adFieldDataOverflow**|6|Indica che i dati restituiti dal provider di overflow rispetto al tipo di dati del campo.|  
|**adFieldDefault**|13|Indica che il valore predefinito per il campo è stato utilizzato durante l'impostazione dei dati.|  
|**adFieldIgnore**|15|Indica che questo campo è stato ignorato durante l'impostazione dati i valori nell'origine. È stato impostato alcun valore dal provider.|  
|**adFieldIntegrityViolation**|10|Indica che il campo non può essere modificato perché è un'entità calcolata o derivata.|  
|**adFieldIsNull**|3|Indica che il provider ha restituito un valore null.|  
|**adFieldOutOfSpace**|22|Indica che il provider è in grado di ottenere spazio di archiviazione sufficiente per completare un'operazione di spostamento o l'operazione di copia.|
