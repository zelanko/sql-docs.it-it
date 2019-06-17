---
title: Altre architetture di Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd051d018cb6f53b8c08110e26bc66910e3ca4c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045528"
---
# <a name="other-driver-architectures"></a>Altre architetture di driver
Alcuni driver ODBC non sono strettamente conformi per l'architettura descritta in precedenza. È possibile che i driver di eseguono attività diverse da quelle di un driver ODBC tradizionali o non sono driver nel senso normale.  
  
## <a name="driver-as-a-middle-component"></a>Driver come componente centrale  
 Il driver ODBC può trovarsi tra gestione Driver e uno o più driver ODBC. Quando il driver al centro è in grado di lavorare con più origini dati, agisce come un dispatcher di chiamate ODBC o tradotta in modo appropriato le chiamate da altri moduli che effettivamente accedere alle origini dati. In questa architettura, il driver nella parte centrale richiede alcuni del ruolo di una gestione Driver.  
  
 Un altro esempio di questo tipo di driver è un programma spy per ODBC, che intercetta e copia le funzioni ODBC inviate tra gestione Driver e il driver. Questo livello è utilizzabile per emulare un driver o un'applicazione. Per la gestione di Driver, il livello viene visualizzato sia il driver; al driver, il livello viene visualizzato da Gestione Driver.  
  
## <a name="heterogeneous-join-engines"></a>Motori di Join eterogeneo  
 Alcuni driver ODBC vengono compilate al momento di un motore di query per l'esecuzione di join eterogeneo. In un'architettura di un motore di join eterogeneo (vedere la figura seguente), il driver viene visualizzato per l'applicazione come un driver ma viene visualizzato a un'altra istanza di gestione Driver come un'applicazione. Questo driver elabora un join eterogeneo dall'applicazione chiamando nei driver in istruzioni SQL separate per ogni database unito in join.  
  
 ![Architettura di un motore di join eterogeneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Questa architettura offre un'interfaccia comune per l'applicazione accedere ai dati da database diversi. È possibile usare un modo comune per recuperare i metadati, ad esempio informazioni sulle colonne speciali (identificatori di riga), e può chiamare funzioni comuni di catalogo per recuperare informazioni del dizionario dei dati. Chiamando la funzione ODBC **SQLStatistics**, ad esempio, l'applicazione può recuperare informazioni sugli indici nelle tabelle di essere unito in join, anche se le tabelle si trovano in due distinti database. Query processor non dovrà preoccuparsi di come i database di archiviano i metadati.  
  
 L'applicazione ha anche accesso standard per i tipi di dati. ODBC definisce tipi di dati SQL comuni che i tipi di dati specifici del DBMS vengono eseguito il mapping a. Un'applicazione può chiamare **SQLGetTypeInfo** per recuperare informazioni sui tipi di dati in database diversi.  
  
 Quando l'applicazione genera un'istruzione di join eterogeneo, query processor in questa architettura analizza l'istruzione SQL e quindi genera istruzioni SQL separate per ogni database da unire. Grazie ai metadati di tutti i driver, query processor di determinare il join più efficace e intelligente. Ad esempio, se l'istruzione join due tabelle in un database con una tabella in un altro database, query processor può aggiungere le due tabelle in un database prima di aggiungere il risultato con la tabella di altro database.  
  
## <a name="odbc-on-the-server"></a>ODBC sul Server  
 Driver ODBC possono essere installati in un server in modo che possono essere usati dalle applicazioni in uno qualsiasi di una serie di computer client. In questa architettura (vedere la figura seguente), una gestione Driver e un singolo driver ODBC vengono installati in ogni client e un altro gestore di Driver e una serie di driver ODBC vengono installati nel server. In questo modo ogni accesso client a una varietà di driver utilizzate e gestite nel server.  
  
 ![Architettura del driver ODBC in un server](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Vantaggio di questa architettura consiste nella configurazione e manutenzione efficiente del software. I driver devono essere aggiornati solo in un'unica posizione: nel server. Origini dati con origini dati di sistema, è possibile definire nel server per l'utilizzo per tutti i client. Non è necessario definire le origini dati nel client. Pool di connessioni può essere utilizzato per semplificare il processo mediante il quale i client si connettono a origini dati.  
  
 Il driver del client è in genere un driver di dimensioni molto ridotto che trasferisce la chiamata di gestione Driver al server. Il footprint può essere significativamente inferiore ai driver ODBC perfettamente funzionanti sul server. In questa architettura, è possibile liberare risorse client se il server dispone di potenza di calcolo. Inoltre, l'efficienza e sicurezza dell'intero sistema possono essere migliorati con installazione di server di backup e l'esecuzione di bilanciamento del carico per ottimizzare l'uso di server.
