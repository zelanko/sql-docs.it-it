---
title: Accesso al database di rete - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2237c725d6fe3696d1f28d80c09f22183f718de8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295584"
---
# <a name="network-database-access"></a>Accesso di rete ai database
L'accesso a un database attraverso una rete richiede un numero di componenti, ognuno dei quali è indipendente e risiede sotto l'interfaccia di programmazione. Questi componenti sono illustrati nella figura seguente.  
  
 ![Componenti per l'accesso a un database in rete](../../odbc/reference/media/pr04.gif "pr04 (in questo constatato rem")  
  
 Di seguito è fornita un'ulteriore descrizione di ciascun componente:  
  
-   **Interfaccia di programmazione** Come descritto in precedenza in questa sezione, l'interfaccia di programmazione contiene le chiamate effettuate dall'applicazione. Queste interfacce (SQL incorporato, moduli SQL e interfacce a livello di chiamata) sono in genere specifiche per ogni DBMS, anche se sono in genere basate su uno standard ANSI o ISO.  
  
-   **Protocollo flusso di dati** Il protocollo del flusso di dati descrive il flusso di dati trasferiti tra il DBMS e il relativo client. Ad esempio, il protocollo potrebbe richiedere il primo byte per descrivere il contenuto del resto del flusso: un'istruzione SQL da eseguire, un valore di errore restituito o dati restituiti. Il formato del resto dei dati nel flusso dipenderebbe quindi da questo flag. Ad esempio, un flusso di errore potrebbe contenere il flag, un codice di errore integer a 2 byte, una lunghezza del messaggio di errore Integer a 2 byte e un messaggio di errore.  
  
     Il protocollo del flusso di dati è un protocollo logico ed è indipendente dai protocolli utilizzati dalla rete sottostante. Pertanto, un singolo protocollo di flusso di dati può in genere essere utilizzato su un numero di reti diverse. I protocolli del flusso di dati sono in genere proprietari e sono stati ottimizzati per funzionare con un particolare DBMS.  
  
-   **Meccanismo di comunicazione interprocesso** Il meccanismo di comunicazione interprocesso (IPC) è il processo mediante il quale un processo comunica con un altro. Gli esempi includono named pipe, socket TCP/IP e socket DECnet. La scelta del meccanismo IPC è vincolata dal sistema operativo e dalla rete in uso.  
  
-   **Protocollo di rete** Il protocollo di rete viene utilizzato per trasportare il flusso di dati su una rete. Può essere considerato l'impianto idraulico che supporta i meccanismi IPC utilizzati per implementare il protocollo del flusso di dati, oltre a supportare le operazioni di rete di base come i trasferimenti di file e la condivisione di stampa. I protocolli di rete includono NetBEUI, TCP/IP, DECnet e SPX/IPX e sono specifici per ogni rete.
