---
description: Configurazione del cursore
title: Impostazione del cursore | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 307245dc403167f5bd857005f084ed22498d3ee8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424583"
---
# <a name="setting-up-the-cursor"></a>Configurazione del cursore
L'applicazione può specificare il tipo di cursore prima di eseguire un'istruzione che crea un set di risultati. Questa operazione viene eseguita con l'attributo SQL_ATTR_CURSOR_TYPE Statement. Se l'applicazione non specifica in modo esplicito un tipo, verrà utilizzato un cursore di tipo "solo". Per ottenere un cursore misto, un'applicazione specifica un cursore gestito da keyset ma dichiara una dimensione del keyset inferiore alla dimensione del set di risultati.  
  
 Per i cursori gestiti da keyset e misti, l'applicazione può anche specificare le dimensioni del keyset. Questa operazione viene eseguita con l'attributo SQL_ATTR_KEYSET_SIZE Statement. Se la dimensione del keyset è impostata su 0, ovvero il valore predefinito, le dimensioni del keyset vengono impostate sulle dimensioni del set di risultati e viene utilizzato un cursore gestito da keyset. Le dimensioni del keyset possono essere modificate dopo l'apertura del cursore.  
  
 L'applicazione può inoltre impostare le dimensioni del set di righe. Per ulteriori informazioni, vedere [utilizzo di cursori a blocchi](../../../odbc/reference/develop-app/using-block-cursors.md), più indietro in questa sezione.
