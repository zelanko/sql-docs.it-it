---
description: CustomData (MDX)
title: CustomData (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ed7bfe2841caf9bd5b2c6e6caf102323db6d62ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413167"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  Restituisce il valore della proprietà della stringa di connessione **CustomData** se definito; in caso contrario, **null**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>Valore restituito  
 La funzione **CustomData** può recuperare la proprietà della stringa di connessione **CustomData** e passare un'impostazione di configurazione che verrà utilizzata dalle funzioni MDX (Multidimensional Expressions) e dalle istruzioni, ad esempio [username (MDX)](../mdx/username-mdx.md) e [Call Statement (MDX)](../mdx/mdx-data-manipulation-call.md). Questa funzione, ad esempio, può essere usata in un'espressione di sicurezza dinamica per selezionare i membri impostati consentiti/negati per il valore stringa nella proprietà della stringa di connessione **CustomData** .  
  
## <a name="example"></a>Esempio  
 Nella query seguente viene visualizzato il valore restituito dalla funzione **CustomData** in una misura calcolata:  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
