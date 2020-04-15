---
title: Architettura del driver ODBC - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712de6a7a3f80ce1cd3ca854a88765dbfa531356
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294559"
---
# <a name="odbc-driver-architecture"></a>Architettura dei driver ODBC
I writer di driver devono tenere presente che l'architettura del driver può influire sull'utilizzo di SQL specifico di DBMS.  
  
 ![Mostra l'architettura del driver ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Driver basati su file](../../../odbc/reference/file-based-drivers.md)  
  
 Quando il driver accede direttamente ai dati fisici, il driver funge sia da driver che da origine dati. Il driver deve elaborare sia le chiamate ODBC che le istruzioni SQL. Gli sviluppatori di driver basati su file devono scrivere i propri motori di database.  
  
 [Driver basati su DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Quando un motore di database separato viene utilizzato per accedere ai dati fisici, il driver elabora solo le chiamate ODBC. Passa istruzioni SQL al motore di database per l'elaborazione.  
  
 [Architettura di rete](../../../odbc/reference/network-example.md)  
  
 Le configurazioni ODBC di file e DBMS possono esistere in una singola rete.  
  
 [Altre architetture di driver](../../../odbc/reference/other-driver-architectures.md)  
  
 Quando un driver è necessario per lavorare con una varietà di origini dati, può essere utilizzato come middleware. L'architettura eterogenea del motore di join può far apparire il driver come gestore del driver. I driver possono anche essere installati su server, dove possono essere condivisi da una serie di client.  
  
 Per ulteriori informazioni sull'architettura dei driver, vedere [Gestione driver](../../../odbc/reference/the-driver-manager.md) e [architettura dei driver](../../../odbc/reference/driver-architecture.md) nella sezione sull'architettura [ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Ulteriori informazioni sui problemi dei driver sono disponibili nei percorsi descritti nella tabella seguente.  
  
|Problema|Argomento|Location|  
|-----------|-----------|--------------|  
|Problemi di compatibilità con applicazioni e driver|[Compatibilità applicazione/driver](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md), in ODBC Programmer's Reference (considerazioni sulla programmazione ODBC)|  
|Scrittura di driver ODBC|[Scrittura di driver ODBC 3.x](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md), in ODBC Programmer's Reference (considerazioni sulla programmazione ODBC)|  
|Linee guida per i driver per la compatibilità con le versioni precedenti|[Linee guida per la compatibilità con le versioni precedenti dei driver](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Appendice G: Linee guida per](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)i driver per la compatibilità con le versioni precedenti , in ODBC Programmer's Reference (Informazioni in base alle funzionalità java)|  
|Connessione a un driver|[Scelta di un'origine dati o driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Connessione a un'origine dati o](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)a un driver , in ODBC Programmer's Reference (informazioni in base al programmatore ODBC)|  
|Identificazione dei driver|[Visualizzazione dei driver](../../../odbc/admin/viewing-drivers.md)|[Visualizzazione dei driver](../../../odbc/admin/viewing-drivers.md), nella Guida in linea di Amministratore origine dati Microsoft ODBC|  
|Abilitazione del pool di connessioni|[Pool di connessioni ODBCODBC Connection Pooling](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Connessione a un'origine dati o](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)a un driver , in ODBC Programmer's Reference (informazioni in base al programmatore ODBC)|  
|Problemi di connessione e driver Unicode/ANSI|[Driver di Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md), in ODBC Programmer's Reference (considerazioni sulla programmazione ODBC)|  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
