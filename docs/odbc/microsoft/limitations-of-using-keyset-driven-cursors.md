---
description: Limitazioni dell'uso dei cursori gestiti da keyset
title: Limitazioni dell'utilizzo di cursori gestiti da keyset | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 611bc032c51760742e5dce4dfbd8e1fa4fe33d0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483474"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitazioni dell'uso dei cursori gestiti da keyset
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 È necessario essere in grado di recuperare una singola colonna ROWID per la tabella sottoposta a query. Non è possibile usare un cursore gestito da keyset in join, query o istruzioni che contengono clausole DISTINCT, GROUP BY, UNION, INTERSECT o MINUs.  
  
 Inoltre, se l'applicazione utilizza alias di tabella, i cursori gestiti da keyset non funzioneranno. sono necessari i tipi di cursore di tipo inoltr o static. Se si utilizza il tipo di cursore keyset con alias di tabella, si verificherà l'errore seguente: "[Microsoft] [driver ODBC per Oracle] non può utilizzare il cursore gestito da keyset al join, con Union, Intersect o meno o il set di risultati di sola lettura".  
  
> [!NOTE]  
>  A causa del modo in cui il driver gestisce l'istruzione SQL inviata al server Oracle, Oracle restituisce internamente il seguente messaggio di errore: "ORA-00964: nome tabella non presente nell'elenco."
