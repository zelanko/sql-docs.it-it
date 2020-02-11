---
title: Informazioni sugli errori correlati al campo | Microsoft Docs
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
ms.openlocfilehash: 7094c2dba004e35593f5ab11b1162efbdf3283c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925316"
---
# <a name="field-related-error-information"></a>Informazioni sugli errori correlati ai campi
Se un errore è direttamente correlato a un campo, ad esempio se i dati risultano mancanti o se il tipo non è corretto per il campo, è possibile recuperare ulteriori informazioni sulla causa del problema esaminando la proprietà di **stato** dell'oggetto **campo** . Questa proprietà è stata migliorata per fornire informazioni specifiche sul problema. Quindi, ad esempio, quando una chiamata a **UpdateBatch** ha esito negativo, la causa del problema può essere determinata esaminando la proprietà **status** dei **campi** in ognuno dei record effettivi. La proprietà conterrà uno dei valori della costante **FieldStatusEnum** . La tabella seguente include i valori che sono di particolare interesse quando si verifica un errore.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|Indica che il campo non può essere recuperato o archiviato senza perdita di dati.|  
|**adFieldDataOverflow**|6|Indica che i dati restituiti dal provider hanno causato un overflow del tipo di dati del campo.|  
|**adFieldDefault**|13|Indica che durante l'impostazione dei dati è stato utilizzato il valore predefinito per il campo.|  
|**adFieldIgnore**|15|Indica che questo campo è stato ignorato durante l'impostazione dei valori dei dati nell'origine. Nessun valore è stato impostato dal provider.|  
|**adFieldIntegrityViolation**|10|Indica che il campo non può essere modificato perché è un'entità calcolata o derivata.|  
|**adFieldIsNull**|3|Indica che il provider ha restituito un valore null.|  
|**adFieldOutOfSpace**|22|Indica che il provider non è in grado di ottenere spazio di archiviazione sufficiente per completare un'operazione di spostamento o copia.|
