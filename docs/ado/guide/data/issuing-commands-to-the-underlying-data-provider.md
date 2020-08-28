---
description: Invio di comandi al provider di dati sottostante
title: Invio di comandi all'provider di dati sottostante | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: rothja
ms.author: jroth
ms.openlocfilehash: d4f1db51d54b69bf42fe185d30b78df57b89df39
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980432"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Invio di comandi al provider di dati sottostante
Qualsiasi comando che non inizia con SHAPE viene passato al provider di dati. Equivale a emettere un comando SHAPE nel formato "SHAPE {provider Command}". Questi comandi *non* devono produrre un **Recordset**. Ad esempio, "SHAPE {DROP TABLE MyTable} è un comando Shape perfettamente valido, presupponendo che il provider di dati supporti DROP TABLE.  
  
 Questa funzionalità consente sia ai comandi del provider normali che ai comandi di forma di condividere la stessa connessione e la stessa transazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](./data-shaping-example.md)   
 [Grammatica forma formale](./formal-shape-grammar.md)   
 [Comandi Shape in generale](./shape-commands-in-general.md)