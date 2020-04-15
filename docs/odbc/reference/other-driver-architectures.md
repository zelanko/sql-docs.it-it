---
title: Altre architetture di driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae047fe8014b806d3bda8b0513521b4ddda072a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280531"
---
# <a name="other-driver-architectures"></a>Altre architetture di driver
Alcuni driver ODBC non sono strettamente conformi all'architettura descritta in precedenza. Ciò potrebbe essere dovuto al fatto che i driver eseguono compiti diversi da quelli di un driver ODBC tradizionale o non sono driver nel senso normale.  
  
## <a name="driver-as-a-middle-component"></a>Driver come componente intermedio  
 Il driver ODBC può risiedere tra Gestione Driver e uno o più altri driver ODBC. Quando il driver nel mezzo è in grado di lavorare con più origini dati, funge da dispatcher di chiamate ODBC (o chiamate tradotte in modo appropriato) ad altri moduli che accedono effettivamente alle origini dati. In questa architettura, il driver nel mezzo sta assumendo parte del ruolo di un Driver Manager.  
  
 Un altro esempio di questo tipo di driver è un programma spia per ODBC, che intercetta e copia le funzioni ODBC inviate tra Gestione Driver e il driver. Questo livello può essere utilizzato per emulare un driver o un'applicazione. Per Gestione Driver, il layer sembra essere il driver; al driver, il layer sembra essere Gestione Driver.  
  
## <a name="heterogeneous-join-engines"></a>Motori di giunzione eterogenei  
 Alcuni driver ODBC si basano su un motore di query per l'esecuzione di join eterogenei. In un'architettura di un motore di join eterogeneo (vedere la figura seguente), il driver viene visualizzato nell'applicazione come driver ma viene visualizzato in un'altra istanza di Gestione Driver come applicazione. Questo driver elabora un join eterogeneo dall'applicazione chiamando istruzioni SQL separate nei driver per ogni database unito.  
  
 ![Architettura di un motore di join eterogeneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Questa architettura fornisce un'interfaccia comune per l'applicazione per accedere ai dati da database diversi. Può usare un modo comune per recuperare i metadati, ad esempio informazioni sulle colonne speciali (identificatori di riga) e può chiamare funzioni comuni del catalogo per recuperare le informazioni sul dizionario dei dati. Chiamando la funzione ODBC **SQLStatistics**, ad esempio, l'applicazione può recuperare informazioni sugli indici nelle tabelle da unire in join, anche se le tabelle si trovano in due database separati. Query Processor non deve preoccuparsi del modo in cui i database archiviano i metadati.  
  
 L'applicazione ha anche accesso standard ai tipi di dati. ODBC definisce i tipi di dati SQL comuni a cui vengono mappati i tipi di dati specifici di DBMS. Un'applicazione può chiamare **SQLGetTypeInfo** per recuperare informazioni sui tipi di dati in database diversi.  
  
 Quando l'applicazione genera un'istruzione join eterogenea, Query Processor in questa architettura analizza l'istruzione SQL e quindi genera istruzioni SQL separate per ogni database da unire. Utilizzando i metadati relativi a ogni driver, Query Processor è in grado di determinare il join intelligente più efficiente. Ad esempio, se l'istruzione unisce due tabelle in un database con una tabella in un altro database, Query Processor può unire le due tabelle in un database prima di unire il risultato con la tabella dell'altro database.  
  
## <a name="odbc-on-the-server"></a>ODBC sul server  
 I driver ODBC possono essere installati in un server in modo che possano essere utilizzati dalle applicazioni in una serie di computer client. In questa architettura (vedere la figura seguente), un Driver Manager e un singolo driver ODBC vengono installati in ogni client e un altro Driver Manager e una serie di driver ODBC vengono installati sul server. Ciò consente a ogni client di accedere a una varietà di driver utilizzati e mantenuti sul server.  
  
 ![Architettura di driver ODBC in un server](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Uno dei vantaggi di questa architettura è l'efficiente manutenzione e configurazione del software. I driver devono essere aggiornati in un'unica posizione: sul server. Utilizzando le origini dati di sistema, le origini dati possono essere definite nel server per l'utilizzo da parte di tutti i client. Le origini dati non devono essere definite nel client. Il pool di connessioni può essere utilizzato per semplificare il processo mediante il quale i client si connettono alle origini dati.  
  
 Il driver sul client è in genere un driver molto piccolo che trasferisce la chiamata di Gestione Driver al server. Il footprint può essere significativamente inferiore rispetto ai driver ODBC completamente funzionali sul server. In questa architettura, le risorse client possono essere liberate se il server dispone di più potenza di calcolo. Inoltre, l'efficienza e la sicurezza dell'intero sistema possono essere migliorate installando server di backup ed eseguendo il bilanciamento del carico per ottimizzare l'utilizzo dei server.
