---
title: Impostazione delle opzioni di pool di connessioni ODBC Documenti Microsoft
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
ms.openlocfilehash: 1d8e66c506518b77320347ce9120254aa1cae287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307197"
---
# <a name="setting-odbc-connection-pooling-options"></a>Impostazione di opzioni del pool di connessioni ODBC
Il pool di connessioni consente a un'applicazione di utilizzare una connessione da un pool di connessioni che non è necessario ristabilire per ogni utilizzo. È possibile utilizzare la scheda **Pool di** connessioni della finestra di dialogo Amministratore origine **dati ODBC** per abilitare e disabilitare il monitoraggio delle prestazioni. Fare doppio clic sul nome di un driver per impostare il periodo di timeout della connessione.  
  
 A livello di driver, il pool di connessioni è abilitato dal valore del Registro di sistema CPTimeout. Questa abilitazione selettiva per driver consente a un amministratore di sistema di abilitare il pool di connessioni solo per i driver che possono supportarlo. Questa operazione viene eseguita impostando il valore predefinito di CPTimeout durante il programma di installazione del driver. Fare doppio clic sul nome di un driver per impostare il periodo di timeout della connessione.  
  
 Per ulteriori informazioni sul pool di connessioni, vedere [Pool di connessioni ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoraggio delle prestazioni  
 Il monitoraggio delle prestazioni tiene traccia delle prestazioni della connessione registrando una varietà di statistiche. Queste statistiche possono essere personalizzate dallo sviluppatore per includere elementi come i seguenti:  
  
|Contatore|Definizione|  
|-------------|----------------|  
|Contatore connessioni rigide ODBC al secondo|Numero di connessioni effettive al secondo effettuate al server. La prima volta che l'ambiente trasporta un carico pesante, questo contatore salirà molto rapidamente. Dopo alcuni secondi, scenderà a zero. Questa è la situazione normale quando il pool di connessioni funziona. Una volta stabilite le connessioni al server, queste verranno utilizzate e inserite nel pool per il riutilizzo.|  
|ODBC Hard Disconnect Counter per Second|Numero di disconnessioni rigide al secondo emesse al server. Si tratta di connessioni effettive al server che vengono rilasciate dal pool di connessioni. Questo valore aumenterà da zero quando si arrestano tutti i client nel sistema e le connessioni iniziano a sfinire.|  
|Contatore connessioni software ODBC al secondo|Il numero di connessioni soddisfatte dal pool al secondo, ovvero le connessioni da tale pool che sono state passate agli utenti. Questo contatore indica se il pooling funziona. A seconda del carico sul server, non è raro che questo mostri 40-60 connessioni soft al secondo.|  
|Contatore di disconnessione software ODBC al secondo|Numero di disconnessioni al secondo emesse dalle applicazioni. Quando l'applicazione viene rireleases o disconnessa, la connessione viene inserita nuovamente nel pool.|  
|Contatore connessione attiva corrente ODBC|Numero di connessioni nel pool attualmente in uso.|  
|Contatore connessione libera corrente ODBCODBC Current Free Connection Counter|Il numero corrente di connessioni libere disponibili nel pool. Si tratta di connessioni attive disponibili per l'uso.|  
|Pool attualmente attivi|Il numero di pool attualmente attivi. Questo contatore è stato aggiunto in Windows 8, per i driver che gestiscono le connessioni nel pool di connessioni. Per ulteriori informazioni, vedere [Pool di connessioni in base](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)al driver .|  
|Pool creati|Il numero di pool attivi, inclusi i pool attivi e rimossi. Questo contatore è stato aggiunto in Windows 8, per i driver che gestiscono le connessioni nel pool di connessioni. Per ulteriori informazioni, vedere [Pool di connessioni in base](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)al driver .|  
  
 È necessario specificare i propri parametri di monitoraggio. Esempi per il monitoraggio delle prestazioni sono stati inclusi in questa versione di ODBC.
