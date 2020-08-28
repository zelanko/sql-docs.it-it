---
description: Errori (ADO)
title: Errori (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB providers [ADO]
- ADO, OLE DB providers
ms.assetid: 8ae6611b-3069-4155-b014-c0c9da37be39
author: rothja
ms.author: jroth
ms.openlocfilehash: e779d6b0aac1e48f64d9544eda0c064f7278c496
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991312"
---
# <a name="errors-ado"></a>Errori (ADO)
Tutte le operazioni che coinvolgono oggetti ADO possono generare uno o più errori del provider. Quando si verifica ogni errore, uno o più oggetti **Error** vengono inseriti nella raccolta **Errors** dell'oggetto **Connection** . Per informazioni dettagliate sulla gestione degli avvisi e degli errori nell'applicazione ADO, vedere [gestione degli](./error-handling.md)errori.  
  
 Gli errori dell'applicazione possono essere generati da un meccanismo separato. Ad esempio, in Visual Basic, l'oggetto **Err** conterrà errori a livello di applicazione.