---
title: Contenuto di FORE_COLOR e contenuto di BACK_COLOR (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- FORE_COLOR contents
- backgrounds [MDX]
- cells [MDX]
- colors [MDX]
- storing cell color information
- cell backgrounds
- BACK_COLOR contents
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd8bb157d7b501d29230c91d87f148ae738ff45
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074405"
---
# <a name="forecolor-and-backcolor-contents-mdx"></a>Contenuto di FORE_COLOR e BACK_COLOR (MDX)
  Nelle proprietà `FORE_COLOR` e `BACK_COLOR` di una cella sono archiviate, rispettivamente, informazioni sui colori del testo e dello sfondo della cella, nel formato RGB di Microsoft Windows.  
  
 I valori validi per i colori RGB standard sono compresi tra zero (0) e 16.777.215 (&H00FFFFFF). Il primo byte di un numero in questo intervallo è sempre uguale a 0. I 3 byte successivi, dal meno significativo al più significativo, determinano rispettivamente le quantità di rosso, verde e blu. Ognuno dei componenti rosso, verde e blu è rappresentato da un numero compreso tra 0 e 255 (&HFF).  
  
## <a name="see-also"></a>Vedere anche  
 [Uso delle proprietà delle celle &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)  
  
  
