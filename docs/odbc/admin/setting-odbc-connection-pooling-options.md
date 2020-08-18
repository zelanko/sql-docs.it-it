---
description: Impostazione di opzioni del pool di connessioni ODBC
title: Impostazione delle opzioni per il pool di connessioni ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d6f741654f9765e909a8a2e33bce5e7e596f8b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386597"
---
# <a name="setting-odbc-connection-pooling-options"></a>Impostazione di opzioni del pool di connessioni ODBC
Il pool di connessioni consente a un'applicazione di usare una connessione da un pool di connessioni che non devono essere ristabilite per ogni uso. È possibile utilizzare la scheda **pool di connessioni** della finestra di dialogo **Amministrazione origine dati ODBC** per abilitare e disabilitare il monitoraggio delle prestazioni. Fare doppio clic sul nome di un driver per impostare il periodo di timeout della connessione.  
  
 A livello di driver, il pool di connessioni è abilitato dal valore del registro di sistema CPTimeout. Questa abilitazione selettiva per driver consente a un amministratore di sistema di abilitare il pool di connessioni solo per i driver in grado di supportarlo. Questa operazione viene eseguita impostando il valore predefinito di CPTimeout durante il programma di installazione del driver. Fare doppio clic sul nome di un driver per impostare il periodo di timeout della connessione.  
  
 Per ulteriori informazioni sul pool di connessioni, vedere la pagina relativa al [pool di connessioni ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoraggio delle prestazioni  
 Il monitoraggio delle prestazioni tiene traccia delle prestazioni della connessione registrando un'ampia gamma di statistiche. Queste statistiche possono essere personalizzate dallo sviluppatore per includere elementi come i seguenti:  
  
|Contatore|Definizione|  
|-------------|----------------|  
|Contatore connessioni rigide ODBC al secondo|Numero di connessioni effettive al secondo effettuate al server. La prima volta che l'ambiente comporta un carico elevato, questo contatore risale molto rapidamente. Dopo alcuni secondi, verrà rilasciata a zero. Si tratta della situazione normale quando il pool di connessioni funziona. Quando le connessioni al server sono state stabilite, verranno usate e inserite nel pool per il riutilizzo.|  
|Contatore di disconnessione hardware ODBC al secondo|Numero di disconnessioni rigide al secondo emesse al server. Si tratta di connessioni effettive al server rilasciate dal pool di connessioni. Questo valore aumenterà da zero quando si arrestano tutti i client nel sistema e si verifica il timeout delle connessioni.|  
|Contatore connessione flessibile ODBC al secondo|Il numero di connessioni soddisfatte dal pool al secondo, ovvero le connessioni da tale pool passate agli utenti. Questo contatore indica se il pool è funzionante. A seconda del carico sul server, non è insolito che mostri 40-60 connessioni soft al secondo.|  
|Contatore di disconnessione software ODBC al secondo|Numero di disconnessioni al secondo emesse dalle applicazioni. Quando l'applicazione rilascia o si disconnette, la connessione viene riposizionata nel pool.|  
|Contatore connessione attiva ODBC corrente|Numero di connessioni nel pool attualmente in uso.|  
|Contatore connessione libera corrente ODBC|Numero corrente di connessioni gratuite disponibili nel pool. Si tratta di connessioni in tempo reale disponibili per l'utilizzo.|  
|Pool attualmente attivi|Il numero di pool attualmente attivi. Questo contatore è stato aggiunto in Windows 8 per i driver che gestiscono le connessioni nel pool di connessioni. Per ulteriori informazioni, vedere [pool di connessioni compatibile](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)con i driver.|  
|Pool creati|Il numero di pool attivi, inclusi i pool attivi e rimossi. Questo contatore è stato aggiunto in Windows 8 per i driver che gestiscono le connessioni nel pool di connessioni. Per ulteriori informazioni, vedere [pool di connessioni compatibile](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)con i driver.|  
  
 È necessario specificare i propri parametri di monitoraggio. Con questa versione di ODBC sono stati inclusi esempi per il monitoraggio delle prestazioni.
