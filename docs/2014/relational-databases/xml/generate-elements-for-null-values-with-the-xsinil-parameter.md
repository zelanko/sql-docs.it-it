---
title: Generare elementi per valori NULL tramite il parametro XSINIL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d056959f5e05d3de79fa81d33331390f4decb49a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205610"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generazione di elementi per valori NULL tramite il parametro XSINIL
  La direttiva **ELEMENTS** costruisce codice XML nel quale viene eseguito il mapping di ogni valore di colonna a un elemento. Se il valore di colonna è NULL, non viene aggiunto alcun elemento. Se si specifica il parametro facoltativo **XSINIL** nella direttiva ELEMENTS, è anche possibile richiedere che venga creato un elemento per il valore NULL. In questo caso, per ogni valore di colonna NULL viene restituito un elemento con l'attributo **xsi:nil** impostato su TRUE.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo della modalità RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
