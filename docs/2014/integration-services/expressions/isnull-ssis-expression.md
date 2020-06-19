---
title: ISNULL (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a4f15d786ccc4ef367ff5e16065f9221991fc021
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967321"
---
# <a name="isnull-ssis-expression"></a>ISNULL (espressione SSIS)
  Restituisce un risultato booleano che varia a seconda che un'espressione abbia o meno un valore Null.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ISNULL(expression)  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression*  
 Espressione valida con qualsiasi tipo di dati.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_BOOL  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito TRUE se nella colonna **DiscontinuedDate** è contenuto un valore Null.  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 In questo esempio viene restituito il testo "Unknown last name" se il valore nella colonna **LastName** è Null, in caso contrario viene restituito il valore in **LastName**.  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 In questo esempio se la colonna **DaysToManufacture** ha valore Null, verrà sempre restituito TRUE indipendentemente dal valore della variabile **AddDays**.  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/coalesce-transact-sql)  
  
  
