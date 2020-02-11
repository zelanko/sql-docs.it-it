---
title: Invio di comandi all'provider di dati sottostante | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02a861daa78b798c1b19b5fc2607cfcaf0ce5968
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924941"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Invio di comandi al provider di dati sottostante
Qualsiasi comando che non inizia con SHAPE viene passato al provider di dati. Equivale a emettere un comando SHAPE nel formato "SHAPE {provider Command}". Questi comandi *non* devono produrre un **Recordset**. Ad esempio, "SHAPE {DROP TABLE MyTable} è un comando Shape perfettamente valido, presupponendo che il provider di dati supporti DROP TABLE.  
  
 Questa funzionalità consente sia ai comandi del provider normali che ai comandi di forma di condividere la stessa connessione e la stessa transazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica forma formale](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
