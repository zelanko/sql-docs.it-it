---
title: Riempimento di stringhe (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7141a102efe167c07147dce19ac2a88aa4606f3b
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359323"
---
# <a name="string-padding-ssis"></a>Riempimento di stringhe (SSIS)
  L'analizzatore di espressioni non verifica se una stringa contiene spazi iniziali e finali, né applica riempimenti alle stringhe in modo che abbiano la stessa lunghezza, prima di confrontarle. Nelle espressioni che richiedono il riempimento delle stringhe è possibile utilizzare l'operatore + per concatenare valori di colonna e stringhe vuote. Per altre informazioni, vedere [+ &#40;concatenazione&#41; &#40;espressione SSIS&#41;](concatenate-ssis-expression.md).  
  
 Se invece è necessario rimuovere spazi, l'analizzatore di espressioni fornisce le funzioni LTRIM, RTRIM e TRIM, che consentono di rimuovere gli spazi iniziali, gli spazi finali o entrambi. Per altre informazioni, vedere [LTRIM &#40;espressione SSIS&#41;](trim-ssis-expression.md), [RTRIM &#40;espressione SSIS&#41;](rtrim-ssis-expression.md) e [TRIM &#40;espressione SSIS&#41;](trim-ssis-expression.md).  
  
> [!NOTE]  
>  La funzione LEN include nel conteggio anche gli spazi vuoti iniziali e finali.  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo tecnico relativo al [foglio d'aiuto per le espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=217683)sul sito Web pragmaticworks.com  
  
  
