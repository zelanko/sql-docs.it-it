---
description: Clausole COMPUTE intermedie di Shape
title: Clausole COMPUTE di forme coinvolte | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- COMPUTE clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: a576bf81-8f3c-4ba1-817b-87e89a8da684
author: rothja
ms.author: jroth
ms.openlocfilehash: 8a4be3fb7f70ba41e24cd757da34e7272e51f87c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980442"
---
# <a name="intervening-shape-compute-clauses"></a>Clausole COMPUTE intermedie di Shape
È possibile incorporare una o più clausole COMPUTE tra l'elemento padre e l'elemento figlio in un comando Shape con parametri, come nell'esempio seguente:  
  
```  
SHAPE {select au_lname, state from authors} APPEND   
   ((SHAPE   
      (SHAPE   
         {select * from authors where state = ?} rs   
      COMPUTE rs, ANY(rs.state) state, ANY(rs.au_lname) au_lname   
      BY au_id) rs2   
   COMPUTE rs2, ANY(rs2.state) BY au_lname)   
RELATE state TO PARAMETER 0)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](./data-shaping-example.md)   
 [Grammatica forma formale](./formal-shape-grammar.md)   
 [Comandi Shape in generale](./shape-commands-in-general.md)