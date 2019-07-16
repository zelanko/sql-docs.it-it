---
title: Invio di comandi al Provider di dati sottostante | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924941"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Invio di comandi al provider di dati sottostante
Tutti i comandi che non iniziano con forma viene passato al provider di dati. Ciò equivale a eseguire un comando shape nel formato "Comando SHAPE con {provider}". Eseguire questi comandi *non* è necessario produrre una **Recordset**. Ad esempio, "forma {DROP TABLE MyTable} è un comando shape perfettamente valido, presupponendo che il provider di dati supporta DROP TABLE.  
  
 Questa funzionalità consente sia i comandi del provider normale e i comandi di forma per condividere la stessa connessione e transazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
