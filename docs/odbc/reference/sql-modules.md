---
title: Moduli SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b5cef56cec30e5ad09500135e05884bf55d5dde
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076222"
---
# <a name="sql-modules"></a>Moduli SQL
La seconda tecnica per l'invio di istruzioni SQL al sistema DBMS è tramite i moduli. In breve, un modulo è costituito da un gruppo di procedure, che vengono chiamate dal linguaggio di programmazione host. Ogni routine contiene una singola istruzione SQL e i dati vengono passati a e dalla procedura tramite parametri.  
  
 Un modulo può essere considerato come una libreria di oggetti collegata al codice dell'applicazione. Tuttavia, il modo in cui le procedure e il resto dell'applicazione sono collegati dipende dall'implementazione. Ad esempio, le procedure possono essere compilate nel codice dell'oggetto e collegate direttamente al codice dell'applicazione, che possono essere compilate e archiviate nel sistema DBMS e chiamate per accedere agli identificatori del piano inseriti nel codice dell'applicazione oppure possono essere interpretate in fase di esecuzione.  
  
 Il vantaggio principale dei moduli è la separazione di istruzioni SQL dal linguaggio di programmazione. In teoria, dovrebbe essere possibile modificarne uno senza modificare l'altro e ricollegarlo semplicemente.
