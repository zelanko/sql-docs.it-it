---
description: Altre architetture di driver
title: Altre architetture di driver | Microsoft Docs
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
ms.openlocfilehash: 44a09eb786abc9f43e25ea105e25e8fdefcdff86
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499664"
---
# <a name="other-driver-architectures"></a>Altre architetture di driver
Alcuni driver ODBC non sono strettamente conformi all'architettura descritta in precedenza. Questo potrebbe essere dovuto al fatto che i driver eseguono compiti diversi da quelli di un driver ODBC tradizionale o non sono driver in senso normale.  
  
## <a name="driver-as-a-middle-component"></a>Driver come componente centrale  
 Il driver ODBC può risiedere tra Gestione driver e uno o più driver ODBC. Quando il driver al centro è in grado di lavorare con più origini dati, funge da dispatcher di chiamate ODBC (o chiamate tradotte in modo appropriato) ad altri moduli che accedono effettivamente alle origini dati. In questa architettura, il driver in mezzo assume parte del ruolo di gestione driver.  
  
 Un altro esempio di questo tipo di driver è un programma di spionaggio per ODBC, che intercetta e copia le funzioni ODBC inviate tra Gestione driver e il driver. Questo livello può essere usato per emulare un driver o un'applicazione. Per Gestione driver, il livello sembra essere il driver; al driver, il livello sembra essere gestione driver.  
  
## <a name="heterogeneous-join-engines"></a>Motori Join eterogenei  
 Alcuni driver ODBC sono basati su un motore di query per l'esecuzione di Join eterogenei. In un'architettura di un motore di join eterogeneo (vedere la figura seguente), il driver viene visualizzato nell'applicazione come driver, ma viene visualizzato in un'altra istanza di gestione driver come applicazione. Questo driver elabora un join eterogeneo dall'applicazione chiamando istruzioni SQL separate nei driver per ogni database Unito in join.  
  
 ![Architettura di un motore di join eterogeneo](../../odbc/reference/media/fig3-4.gif "Fig3-4")  
  
 Questa architettura fornisce un'interfaccia comune per l'applicazione per accedere ai dati da database diversi. Può utilizzare un modo comune per recuperare i metadati, ad esempio le informazioni sulle colonne speciali (identificatori di riga), ed è possibile chiamare funzioni comuni del catalogo per recuperare informazioni sul dizionario dei dati. Chiamando la funzione ODBC **SQLStatistics**, ad esempio, l'applicazione può recuperare informazioni sugli indici nelle tabelle da unire in join, anche se le tabelle si trovano in due database distinti. Query Processor non deve preoccuparsi del modo in cui i metadati vengono archiviati nei database.  
  
 L'applicazione dispone inoltre dell'accesso standard ai tipi di dati di. ODBC definisce i tipi di dati SQL comuni a cui viene eseguito il mapping dei tipi di dati specifici di DBMS. Un'applicazione può chiamare **SQLGetTypeInfo** per recuperare informazioni sui tipi di dati in database diversi.  
  
 Quando l'applicazione genera un'istruzione join eterogenea, query processor in questa architettura analizza l'istruzione SQL e quindi genera istruzioni SQL separate per ogni database da unire in join. Utilizzando i metadati relativi a ogni driver, query processor può determinare il join più efficiente e intelligente. Se, ad esempio, l'istruzione crea un join tra due tabelle in un database con una tabella in un altro database, query processor può unire le due tabelle in un database prima di unire il risultato con la tabella dell'altro database.  
  
## <a name="odbc-on-the-server"></a>ODBC nel server  
 I driver ODBC possono essere installati in un server in modo che possano essere utilizzati dalle applicazioni su una serie di computer client. In questa architettura (vedere la figura seguente), una gestione driver e un singolo driver ODBC sono installati in ogni client e nel server sono installati un'altra gestione driver e una serie di driver ODBC. Questo consente a ogni client di accedere a un'ampia gamma di driver usati e gestiti nel server.  
  
 ![Architettura di driver ODBC in un server](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Un vantaggio di questa architettura è la manutenzione e la configurazione efficienti del software. I driver devono essere aggiornati solo in un'unica posizione: sul server. Utilizzando origini dati di sistema, è possibile definire le origini dati nel server per l'utilizzo da parte di tutti i client. Non è necessario definire le origini dati nel client. Il pool di connessioni può essere usato per semplificare il processo mediante il quale i client si connettono alle origini dati.  
  
 Il driver del client è in genere un driver molto piccolo che trasferisce la chiamata di gestione driver al server. Il footprint può essere significativamente inferiore rispetto ai driver ODBC completamente funzionali nel server. In questa architettura, le risorse client possono essere liberate se il server ha una maggiore potenza di calcolo. Inoltre, l'efficienza e la sicurezza dell'intero sistema possono essere migliorate installando i server di backup ed eseguendo il bilanciamento del carico per ottimizzare l'uso del server.
