---
title: GETDATE (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b17deb29406ff70d777e45ceed8db8ca23275f1
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71289752"
---
# <a name="getdate-ssis-expression"></a>GETDATE (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 [GETUTCDATE &#40;espressione SSIS&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
