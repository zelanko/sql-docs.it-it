---
title: FINDSTRING (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- FINDSTRING function
ms.assetid: c83cb1b1-3c52-4496-b518-4c9253b9336d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2617179156a7102314a8687bb27706e51018d1e3
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428708"
---
# <a name="findstring-ssis-expression"></a>FINDSTRING (espressione SSIS)
  Viene restituita la posizione dell'occorrenza specificata di una determinata stringa in un'espressione di caratteri. Il risultato restituito è l'indice in base 1 dell'occorrenza. Il parametro stringa deve restituire un'espressione di caratteri, mentre il parametro che indica l'occorrenza deve restituire un valore integer. Se la stringa non viene trovata, verrà restituito il valore 0. Se il numero delle occorrenze della stringa è inferiore a quello specificato dall'argomento occurrence, verrà restituito il valore 0.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
FINDSTRING(character_expression, searchstring, occurrence)  
```  
  
## <a name="arguments"></a>Argomenti  
 *character_expression*  
 Stringa di caratteri in cui eseguire la ricerca.  
  
 *searchstring*  
 Stringa di caratteri da cercare.  
  
 *occurrence*  
 Numero intero con o senza segno che specifica l'occorrenza di *searchstring* di cui restituire la posizione.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_I4  
  
## <a name="remarks"></a>Osservazioni  
 È possibile utilizzare FINDSTRING solo con il tipo di dati DT_WSTR.  Per gli argomenti*character_expression* e *searchstring* costituiti da valori letterali stringa o da colonne di dati con tipo di dati DT_STR, prima di eseguire l'operazione della funzione FINDSTRING viene eseguito il cast implicito al tipo di dati DT_WSTR. Per gli altri tipi di dati è necessario il cast esplicito al tipo di dati DT_WSTR. Per altre informazioni, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md) e [Cast &#40;espressione SSIS&#41;](cast-ssis-expression.md).  
  
 FINDSTRING restituirà Null se il valore *character_expression* o *searchstring* sono Null.  
  
 Utilizzare un valore 1 nell'argomento *occurrence* per ottenere l'indice della prima occorrenza, 2 per la seconda occorrenza e così via.  
  
 L'argomento *occurrence* deve essere un numero intero maggiore di 0.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene utilizzato un valore letterale stringa. Il valore restituito è 11.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 1)   
```  
  
 In questo esempio viene utilizzato un valore letterale stringa. Poiché la stringa "NY" ricorre solo due volte, il risultato restituito è 0.  
  
```  
FINDSTRING("New York, NY, NY", "NY", 3)   
```  
  
 In questo esempio viene utilizzata la colonna **Name** . Viene restituita la posizione del valore n nella colonna **Name** . Il risultato restituito dipende dal valore di **Name**. Se **Name** contiene Anderson, la funzione restituirà 8.  
  
```  
FINDSTRING(Name,"n", 2)   
```  
  
 In questo esempio vengono utilizzate le colonne **Name** e **Size** . Viene restituita la posizione del primo carattere a sinistra del valore **Size** nella colonna **Name** . Il risultato restituito dipende dai valori delle colonne. Se **Name** contiene Mountain,500Red,42 e **Size** contiene 42, il risultato restituito sarà 17.  
  
```  
FINDSTRING(Name,Size,1)   
```  
  
## <a name="see-also"></a>Vedere anche  
 [REPLACE &#40;espressione SSIS&#41;](replace-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
