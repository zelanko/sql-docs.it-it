---
title: Divisione (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 5bde9223-872d-443e-8a27-57735e1d8f3d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0ab03e6965d80c3f77276df4218b6a8fdd66f2a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725463"
---
# <a name="divide-ssis-expression"></a>Divisione (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene divisa la prima espressione numerica per la seconda.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
dividend / divisor  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *dividend*  
 Espressione numerica da dividere. *dividend* può essere qualsiasi espressione numerica valida. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 *divisor*  
 Espressione numerica per cui dividere il dividendo. *divisor* può essere qualsiasi espressione numerica valida, tranne zero.  
  
## <a name="result-types"></a>Tipi restituiti  
 Dipendenti dai tipi di dati dei due argomenti. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
## <a name="remarks"></a>Remarks  
 Se uno degli operandi è Null, il risultato sarà Null.  
  
 La divisione per zero non è consentita. A seconda della modalità con cui viene valutata la sottoespressione *divisor* , può verificarsi uno degli errori seguenti:  
  
-   Se la sottoespressione *divisor* che restituisce zero è una costante, l'errore verrà rilevato in fase di progettazione, impedendo la convalida dell'espressione.  
  
-   Se la sottoespressione *divisor* che restituisce zero contiene variabili ma non colonne di input, il componente a cui appartiene l'espressione non supererà la convalida di pre-elaborazione, che avviene prima dell'esecuzione del pacchetto.  
  
-   Se nella sottoespressione *divisor* tramite cui viene restituito zero sono contenute colonne di input, l'errore verrà visualizzato in fase di esecuzione e verrà gestito secondo le regole del flusso degli errori del componente flusso di dati.  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene eseguita una divisione tra due valori letterali numerici.  
  
```  
25 / 5  
```  
  
 In questo esempio i valori nella colonna **ListPrice** vengono divisi per i valori nella colonna **StandardCost** .  
  
```  
ListPrice / StandardCost  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
