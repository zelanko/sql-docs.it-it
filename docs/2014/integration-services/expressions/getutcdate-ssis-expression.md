---
title: GETUTCDATE (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 5e8c8dbdee729b01ed4b49e5a38ff989c80fbc20
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428628"
---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (espressione SSIS)
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
 [GETDATE &#40;espressione SSIS&#41;](getdate-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
