---
title: Moduli SQL - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280426"
---
# <a name="sql-modules"></a>Moduli SQL
La seconda tecnica per l'invio di istruzioni SQL al DBMS è tramite moduli. In breve, un modulo è costituito da un gruppo di procedure, che vengono chiamate dal linguaggio di programmazione host. Ogni procedura contiene una singola istruzione SQL e i dati vengono passati da e verso la procedura tramite i parametri.  
  
 Un modulo può essere considerato come una libreria di oggetti collegata al codice dell'applicazione. Tuttavia, il modo esatto in cui le procedure e il resto dell'applicazione sono collegati dipende dall'implementazione. Ad esempio, le procedure potrebbero essere compilate nel codice oggetto e collegate direttamente al codice dell'applicazione, potrebbero essere compilate e archiviate nel DBMS e chiamate per accedere agli identificatori del piano inseriti nel codice dell'applicazione oppure possono essere interpretate in fase di esecuzione.  
  
 Il vantaggio principale dei moduli è che separano in modo pulito le istruzioni SQL dal linguaggio di programmazione. In teoria, dovrebbe essere possibile cambiarne uno senza cambiare l'altro e semplicemente ricollegarli.
