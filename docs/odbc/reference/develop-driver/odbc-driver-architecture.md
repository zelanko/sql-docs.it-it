---
description: Architettura dei driver ODBC
title: Architettura del driver ODBC | Microsoft Docs
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
ms.openlocfilehash: 1789d5799ed9eb15ace7ea263d1a5804c8e86e74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476247"
---
# <a name="odbc-driver-architecture"></a>Architettura dei driver ODBC
I writer di driver devono tenere presente che l'architettura del driver può influire sul fatto che un'applicazione possa usare SQL specifico di DBMS.  
  
 ![Mostra l'architettura del driver ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Driver basati su file](../../../odbc/reference/file-based-drivers.md)  
  
 Quando il driver accede direttamente ai dati fisici, il driver funge da driver e origine dati. Il driver deve elaborare sia le chiamate ODBC sia le istruzioni SQL. Gli sviluppatori di driver basati su file devono scrivere i propri motori di database.  
  
 [Driver basati su DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Quando si utilizza un motore di database separato per accedere ai dati fisici, il driver elabora solo le chiamate ODBC. Passa istruzioni SQL al motore di database per l'elaborazione.  
  
 [Architettura di rete](../../../odbc/reference/network-example.md)  
  
 Le configurazioni ODBC di file e DBMS possono esistere in una singola rete.  
  
 [Altre architetture di driver](../../../odbc/reference/other-driver-architectures.md)  
  
 Quando è necessario un driver per lavorare con un'ampia gamma di origini dati, è possibile usarlo come middleware. L'architettura del motore di Join eterogenei può far apparire il driver come Gestione driver. I driver possono anche essere installati nei server, in cui possono essere condivisi da una serie di client.  
  
 Per ulteriori informazioni sull'architettura dei driver, vedere [Driver Manager](../../../odbc/reference/the-driver-manager.md) and driver [Architecture](../../../odbc/reference/driver-architecture.md) nella sezione relativa all'architettura [ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Ulteriori informazioni sui problemi relativi ai driver sono disponibili nei percorsi descritti nella tabella seguente.  
  
|Problema|Argomento|Location|  
|-----------|-----------|--------------|  
|Problemi di compatibilità con le applicazioni e i driver|[Compatibilità di applicazioni/driver](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md)in ODBC Programmer ' s Reference|  
|Scrittura di driver ODBC|[Scrittura di driver ODBC 3.x](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md)in ODBC Programmer ' s Reference|  
|Linee guida driver per compatibilità con le versioni precedenti|[Linee guida per la compatibilità con le versioni precedenti dei driver](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Appendice G: linee guida sui driver per la compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), in ODBC Programmer ' s Reference|  
|Connessione a un driver|[Scelta di un'origine dati o driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Connessione a un'origine dati o a un driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)in ODBC Programmer ' s Reference|  
|Identificazione dei driver|[Visualizzazione dei driver](../../../odbc/admin/viewing-drivers.md)|[Visualizzazione dei driver](../../../odbc/admin/viewing-drivers.md)nella Guida in linea di Amministrazione origine dati Microsoft ODBC|  
|Abilitazione del pool di connessioni|[Pool di connessioni ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Connessione a un'origine dati o a un driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)in ODBC Programmer ' s Reference|  
|Problemi di connessione e driver Unicode/ANSI|[Driver di Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Considerazioni sulla programmazione](../../../odbc/reference/develop-app/programming-considerations.md)in ODBC Programmer ' s Reference|  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
