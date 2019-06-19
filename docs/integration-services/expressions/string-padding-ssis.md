---
title: Riempimento di stringhe (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cddc755a958850c7042ec59c7c4703ee77716c76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724953"
---
# <a name="string-padding-ssis"></a>Riempimento di stringhe (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'analizzatore di espressioni non verifica se una stringa contiene spazi iniziali e finali, né applica riempimenti alle stringhe in modo che abbiano la stessa lunghezza, prima di confrontarle. Nelle espressioni che richiedono il riempimento delle stringhe è possibile utilizzare l'operatore + per concatenare valori di colonna e stringhe vuote. Per altre informazioni, vedere [+ &#40;concatenazione&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/concatenate-ssis-expression.md).  
  
 Se invece è necessario rimuovere spazi, l'analizzatore di espressioni fornisce le funzioni LTRIM, RTRIM e TRIM, che consentono di rimuovere gli spazi iniziali, gli spazi finali o entrambi. Per altre informazioni, vedere [LTRIM &#40;espressione SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md), [RTRIM &#40;espressione SSIS&#41;](../../integration-services/expressions/rtrim-ssis-expression.md) e [TRIM &#40;espressione SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md).  
  
> [!NOTE]  
>  La funzione LEN include nel conteggio anche gli spazi vuoti iniziali e finali.  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo al [foglio d'aiuto per le espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=746575)sul sito Web pragmaticworks.com  
  
  
