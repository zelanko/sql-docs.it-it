---
title: Limitazioni dell'utilizzo di cursori | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c4910ebd2c6dd988e937f1e9d6a3281bb0e9741
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192329"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>Limitazioni dell'uso dei cursori gestiti da keyset
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 È necessario essere in grado di recuperare una singola colonna ROWID per la tabella sottoposti a query. Impossibile utilizzare un cursore gestito da keyset in join, query o istruzioni che contengono una parola chiave DISTINCT, GROUP BY, UNION, INTERSECT o meno le clausole.  
  
 Inoltre, se l'applicazione usa gli alias di tabella, gestito da keyset dei cursori non è attivo. tipi di cursore forward-only o statici sono necessari. Il keyset utilizzando il tipo di cursore con gli alias di tabella causerà l'errore seguente: "[Microsoft] [driver ODBC per Oracle] non è possibile utilizzare cursore gestito da Keyset in join, tramite l'operatore union, intersect o meno o in sola lettura di set di risultati."  
  
> [!NOTE]  
>  Il modo in cui che il driver gestisce l'istruzione SQL che viene inviato al server Oracle, Oracle restituisce internamente il messaggio di errore seguente: "ORA 00964: tabella nome non in elenco."
