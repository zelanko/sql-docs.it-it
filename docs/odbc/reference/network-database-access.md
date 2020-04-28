---
title: Accesso al database di rete | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81295584"
---
# <a name="network-database-access"></a>Accesso di rete ai database
Per accedere a un database in una rete sono necessari diversi componenti, ognuno dei quali è indipendente da e risiede sotto, l'interfaccia di programmazione. Questi componenti sono illustrati nella figura seguente.  
  
 ![Componenti per l'accesso a un database in rete](../../odbc/reference/media/pr04.gif "Pr04")  
  
 Di seguito viene riportata una descrizione di ciascun componente:  
  
-   **Interfaccia di programmazione** Come descritto in precedenza in questa sezione, l'interfaccia di programmazione contiene le chiamate effettuate dall'applicazione. Queste interfacce (SQL incorporato, moduli SQL e interfacce a livello di chiamata) sono in genere specifiche per ogni DBMS, sebbene siano in genere basate su uno standard ANSI o ISO.  
  
-   **Protocollo flusso di dati** Il protocollo del flusso di dati descrive il flusso di dati trasferiti tra il sistema DBMS e il client. Ad esempio, il protocollo potrebbe richiedere il primo byte per descrivere il resto del flusso contenente: un'istruzione SQL da eseguire, un valore di errore restituito o dati restituiti. Il formato del resto dei dati nel flusso dipenderà quindi da questo flag. Un flusso di errore può ad esempio contenere il flag, un codice di errore intero a 2 byte, una lunghezza del messaggio di errore integer a 2 byte e un messaggio di errore.  
  
     Il protocollo del flusso di dati è un protocollo logico ed è indipendente dai protocolli utilizzati dalla rete sottostante. In questo modo, in genere è possibile utilizzare un singolo protocollo di flusso di dati su diverse reti. I protocolli di flusso di dati sono in genere proprietari e sono stati ottimizzati per funzionare con un sistema DBMS specifico.  
  
-   **Meccanismo di comunicazione interprocesso** Il meccanismo di comunicazione interprocesso (IPC) è il processo mediante il quale un processo comunica con un altro. Alcuni esempi sono Named Pipes, TCP/IP Sockets e DECnet Sockets. La scelta del meccanismo IPC è vincolata dal sistema operativo e dalla rete in uso.  
  
-   **Protocollo di rete** Il protocollo di rete viene usato per trasportare il flusso di dati in una rete. Può essere considerato il plumbing che supporta i meccanismi IPC usati per implementare il protocollo del flusso di dati, nonché il supporto di operazioni di rete di base, ad esempio i trasferimenti di file e la condivisione di stampa. I protocolli di rete includono NetBEUI, TCP/IP, DECnet e SPX/IPX e sono specifici per ogni rete.
