---
title: Configurazione del cursore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59ade343f282933e05619996b119bc08e2dfb2ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445913"
---
# <a name="setting-up-the-cursor"></a>Configurazione del cursore
L'applicazione può specificare il tipo di cursore prima di impostare l'esecuzione di un'istruzione che crea un risultato. Ciò avviene con l'attributo SQL_ATTR_CURSOR_TYPE di istruzione. Se l'applicazione non specifica in modo esplicito un tipo, verrà utilizzato un cursore forward-only. Per ottenere un cursore misto, un'applicazione specifica un cursore gestito da keyset ma dichiara una dimensione del keyset minore di dimensioni del set di risultati.  
  
 Per i cursori keyset e misti, l'applicazione può inoltre specificare la dimensione del keyset. Ciò avviene con l'attributo di istruzione SQL_ATTR_KEYSET_SIZE. Se la dimensione del keyset è impostata su 0, ovvero l'impostazione predefinita, la dimensione del keyset è impostata per la dimensione del set di risultati e viene utilizzato un cursore gestito da keyset. La dimensione del keyset può essere modificata dopo l'apertura di cursore.  
  
 L'applicazione può anche impostare le dimensioni del set di righe. per altre informazioni, vedere [cursori a blocchi usando](../../../odbc/reference/develop-app/using-block-cursors.md), più indietro in questa sezione.
