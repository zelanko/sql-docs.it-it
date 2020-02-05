---
title: CEILING (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a50fd15830d3509cd086ad4b62938658e1866494
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297681"
---
# <a name="ceiling-ssis-expression"></a>CEILING (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Restituisce il più piccolo valore integer maggiore o uguale a un'espressione numerica specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *numeric_expression*  
 Espressione numerica valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 Tipo di dati dell'espressione numerica inviata alla funzione.  
  
## <a name="remarks"></a>Osservazioni  
 Se l'argomento è Null, CEILING restituirà Null.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questi esempi la funzione CEILING viene applicata a valori positivi, negativi e zero.  
  
```  
CEILING(123.74)  
```  
  
 Restituisce 124,00.  
  
```  
CEILING(-124.27)  
```  
  
 Restituisce -124,00.  
  
```  
CEILING(0.00)  
```  
  
 Restituisce 0,00.  
  
## <a name="see-also"></a>Vedere anche  
 [FLOOR &#40;espressione SSIS&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
