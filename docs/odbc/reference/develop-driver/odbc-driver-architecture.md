---
title: Architettura del Driver ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260767c88fdf980466a21d4cc9658b259b91c854
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690645"
---
# <a name="odbc-driver-architecture"></a>Architettura dei driver ODBC
Gli sviluppatori di driver necessario tenere presente che l'architettura del driver possa interessare un'applicazione può usare SQL specifici del DBMS.  
  
 ![Mostra l'architettura del driver ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Driver basati su file](../../../odbc/reference/file-based-drivers.md)  
  
 Quando il driver accede direttamente i dati fisici, il driver funge da origine dati e del driver. Il driver deve elaborare chiamate ODBC sia istruzioni SQL. Gli sviluppatori di driver basati su file è necessario scrivere i propri motori di database.  
  
 [Driver basati su DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Quando un motore di database separato viene utilizzato per accedere ai dati fisici, il driver elabora solo le chiamate ODBC. Passa istruzioni SQL per motore di database per l'elaborazione.  
  
 [Architettura di rete](../../../odbc/reference/network-example.md)  
  
 Le configurazioni di file e DBMS ODBC possono esistere in una singola rete.  
  
 [Altre architetture di driver](../../../odbc/reference/other-driver-architectures.md)  
  
 Quando è necessario un driver per funzionare con un'ampia gamma di origini dati, può essere utilizzato come middleware. Architettura del motore di join eterogeneo possa visualizzare i driver come strumento di Gestione driver. I driver possono anche essere installati nei server in cui può essere condiviso da una serie di client.  
  
 Per altre informazioni sull'architettura di driver, vedere [gestione Driver](../../../odbc/reference/the-driver-manager.md) e [architettura Driver](../../../odbc/reference/driver-architecture.md) nella sezione [architettura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Altre informazioni sui problemi di driver sono reperibile nei percorsi descritti nella tabella seguente.  
  
|Problema|Argomento|Location|  
|-----------|-----------|--------------|  
|Problemi di compatibilità con le applicazioni e driver|[Compatibilità dell'applicazione/Driver](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md), di riferimento per programmatori ODBC|  
|Driver ODBC di scrittura|[Scrittura di driver ODBC 3.x](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md), di riferimento per programmatori ODBC|  
|Linee guida di driver per la compatibilità con le versioni precedenti|[Linee guida di driver per la compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Appendice g: Linee guida di driver per la compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), di riferimento per programmatori ODBC|  
|La connessione a un driver|[Scelta di un'origine dati o driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[La connessione a una Data sorgente o il Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), di riferimento per programmatori ODBC|  
|Identificare i driver|[Visualizzazione dei driver](../../../odbc/admin/viewing-drivers.md)|[Visualizzazione dei driver](../../../odbc/admin/viewing-drivers.md), nella Guida in linea Amministrazione origine dati ODBC di Microsoft|  
|Abilitazione del pool di connessioni|[Pool di connessioni ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[La connessione a una Data sorgente o il Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), di riferimento per programmatori ODBC|  
|Problemi di connessione e driver di Unicode/ANSI|[Driver di Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md), di riferimento per programmatori ODBC|  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
