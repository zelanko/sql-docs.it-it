---
title: GETDATE (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bd9ffb03358be051647322cd9cb5a125ddf239cf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966611"
---
# <a name="getdate-ssis-expression"></a>GETDATE (espressione SSIS)
  Viene restituita la data corrente del sistema in formato DT_DBTIMESTAMP. La funzione GETDATE non accetta argomenti.  
  
> [!NOTE]  
>  La lunghezza del risultato restituito dalla funzione GETDATE è 29 caratteri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>Argomenti  
 nessuno  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito l'anno della data corrente.  
  
```  
DATEPART("year",GETDATE())  
```  
  
 Questo esempio restituisce il numero di giorni tra una data nella colonna **ModifiedDate** e la data corrente.  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 In questo esempio vengono aggiunti tre mesi alla data corrente.  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>Vedere anche  
 [GETUTCDATE &#40;espressione SSIS&#41;](getutcdate-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](functions-ssis-expression.md)  
  
  
