---
title: GETUTCDATE (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2ca0a021560dd99ec2ebdcd82c40255905cc0784
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916989"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (espressione SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Viene restituita la data corrente del sistema in base all'ora UTC (Universal Time Coordinated o ora di Greenwich) utilizzando un formato DT_DBTIMESTAMP. La funzione GETUTCDATE non accetta argomenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>Argomenti  
 nessuno  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito l'anno della data corrente in base all'ora UTC (Universal Time Coordinated o ora di Greenwich).  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 In questo esempio viene restituito il numero di giorni tra una data nella colonna **ModifiedDate** e la data UTC corrente.  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 In questo esempio vengono aggiunti tre mesi alla data UTC corrente.  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>Vedere anche  
 [GETDATE &#40;espressione SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
