---
title: L'accesso al Database di rete | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- network database access [ODBC]
- standardizing database access [ODBC], network
ms.assetid: f31dd938-e992-436b-b613-145c23973064
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ff13d2e46377b0d29c9bbc8e8ad1705dedc048b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63272878"
---
# <a name="network-database-access"></a>Accesso di rete ai database
L'accesso a un database attraverso una rete richiede un numero di componenti, ognuno dei quali è indipendente da e si trova di sotto, l'interfaccia di programmazione. Questi componenti sono illustrati nella figura seguente.  
  
 ![I componenti per accedere a un database attraverso una rete](../../odbc/reference/media/pr04.gif "pr04")  
  
 Di seguito una descrizione più dettagliata di ogni componente:  
  
-   **Interfaccia di programmazione** come descritto in precedenza in questa sezione, l'interfaccia di programmazione contiene le chiamate effettuate dall'applicazione. Queste interfacce (embedded SQL, SQL, moduli e interfacce a livello di chiamata) sono in genere specifici per ogni sistema DBMS, anche se sono in genere basate su uno standard ANSI o ISO.  
  
-   **Protocollo di Stream data** il protocollo di flusso di dati descrive il flusso di dati trasferiti tra il sistema DBMS e il relativo client. Ad esempio, il protocollo potrebbe richiedere il primo byte per descrivere ciò che contiene il resto del flusso: un'istruzione SQL eseguita, un valore di errore restituito, o i dati restituiti. Il formato del resto dei dati nel flusso dipenderanno quindi questo flag. Ad esempio, un flusso di errore potrebbe contenere il flag, un codice di errore di interi a 2 byte, una lunghezza del messaggio di errore di interi a 2 byte e un messaggio di errore.  
  
     Il protocollo di flusso di dati è un protocollo logico ed è indipendente dai protocolli usati dalla rete sottostante. Di conseguenza, un protocollo di flusso di dati single in genere sono utilizzabili in un numero di reti diverse. Protocolli di flusso di dati sono in genere proprietari e sono stati ottimizzati per lavorare con un DBMS particolare.  
  
-   **Meccanismo di comunicazione interprocesso** il meccanismo di comunicazione interprocesso (IPC) è il processo mediante il quale un processo comunica con un altro. Sono esempi DECnet socket, socket TCP/IP e named pipe. La scelta del meccanismo IPC è limitata dal sistema operativo e la rete in uso.  
  
-   **Protocollo di rete** per trasportare il flusso di dati in una rete viene utilizzato il protocollo di rete. Può essere considerato il plumbing che supporta i meccanismi IPC usati per implementare i dati di streaming protocol, nonché il supporto di operazioni di rete di base, ad esempio i trasferimenti di file e stampanti. Protocolli di rete includono i quali NetBEUI, TCP/IP, DECnet e SPX/IPX e sono specifici per ogni rete.
