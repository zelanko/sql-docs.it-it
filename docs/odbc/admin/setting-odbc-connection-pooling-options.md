---
title: Impostazione opzioni di pool di connessioni ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43d4fe1ab363326269daf40375e126b930d2548b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901639"
---
# <a name="setting-odbc-connection-pooling-options"></a>Impostazione di opzioni del pool di connessioni ODBC
Pool di connessioni consente a un'applicazione usare una connessione da un pool di connessioni che non è necessario ristabilirle per ogni utilizzo. È possibile usare la **pool di connessioni** scheda della finestra di **Amministrazione origine dati ODBC** finestra di dialogo per abilitare e disabilitare il monitoraggio delle prestazioni. Fare doppio clic su un nome di driver per impostare il periodo di timeout di connessione.  
  
 A livello di driver, il pool di connessioni è abilitato per il valore del Registro di sistema CPTimeout. Questa abilitazione selettiva per ogni driver consente a un amministratore di sistema abilitare il pool di connessioni per solo i driver che possono supportare tale condizione. Si è eseguito impostando il valore predefinito di CPTimeout durante il programma di installazione del driver. Fare doppio clic su un nome di driver per impostare il periodo di timeout di connessione.  
  
 Per altre informazioni sui pool di connessioni, vedere [pool di connessioni ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoraggio delle prestazioni  
 Monitoraggio delle prestazioni tiene traccia delle prestazioni di connessione mediante la registrazione di un'ampia gamma di statistiche. Queste statistiche possono essere personalizzate dallo sviluppatore per includere gli elementi seguenti:  
  
|Contatore|Definizione|  
|-------------|----------------|  
|Contatore di connessione disco rigido ODBC al secondo|Il numero di connessioni effettive al secondo che vengono apportate al server. La prima volta che l'ambiente esegue un carico pesante, questo contatore verrà incrementati molto rapidamente. Dopo alcuni secondi, eliminerà su zero. Questa è la situazione normale quando funziona nel pool di connessioni. Quando sono state stabilite le connessioni al server, verranno utilizzati e inseriti nel pool per il riutilizzo.|  
|ODBC rigido disconnettere contatore al secondo|Il numero di disco rigido disconnessioni al secondo inviata al server. Si tratta di connessioni effettive al server che vengono rilasciate dal pool di connessioni. Questo valore verrà aumentati da zero quando si arresta tutti i client nel sistema e le connessioni iniziano a raggiungere il timeout.|  
|Contatore di connessione temporanea ODBC al secondo|Il numero di connessioni soddisfatti dal pool per ogni secondo, in altre parole, le connessioni da quella del pool che sono stato presentato agli utenti. Questo contatore indica se il pool viene eseguito. A seconda del carico sul server, non è insolito per questa opzione per visualizzare le connessioni software 40 a 60 al secondo.|  
|Contatore di disconnessione temporanea ODBC al secondo|Il numero di disconnessioni al secondo emesso dalle applicazioni. Quando l'applicazione rilascia o si disconnette, la connessione viene inserita nuovamente nel pool.|  
|Contatore connessione attiva corrente di ODBC|Il numero di connessioni nel pool che sono attualmente in uso.|  
|Contatore di ODBC corrente di connessioni disponibili|Il numero corrente di connessioni gratuite disponibile nel pool. Si tratta di connessioni in tempo reale che sono disponibili per l'uso.|  
|Crea un pool attualmente attiva|Il numero di pool attualmente attivo. Questo contatore è stata aggiunta in Windows 8 per i driver che gestiscono le connessioni nel pool di connessioni. Per altre informazioni, vedere [Driver-Aware Connection Pooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Pool creati|Il numero di pool attivo, tra cui pool attivo ed è stato rimosso. Questo contatore è stata aggiunta in Windows 8 per i driver che gestiscono le connessioni nel pool di connessioni. Per altre informazioni, vedere [Driver-Aware Connection Pooling](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 È necessario specificare i propri parametri di monitoraggio. Esempi per il monitoraggio delle prestazioni sono stati inclusi in questa versione di ODBC.
