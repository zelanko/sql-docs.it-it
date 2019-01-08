---
title: Architettura del driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b593c3bd8619f0fbba47357f312479c2cd14063b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527177"
---
# <a name="driver-architecture"></a>Architettura dei driver
Architettura del driver rientra nelle due categorie, a seconda di quali processi software istruzioni SQL seguenti:  
  
-   **Driver basati su file** il driver accede direttamente i dati fisici. In questo caso, il driver è funge da origine dati; e del driver vale a dire, lo elabora chiamate ODBC e istruzioni SQL. Ad esempio, i driver dBASE sono driver basati su file perché dBASE non fornisce che un motore di database autonomo, il driver può utilizzare. È importante notare che gli sviluppatori di driver basati su file necessario scrivere i propri motori di database.  
  
-   **Driver basati su DBMS** il driver accede ai dati fisici tramite un motore di database separato. In questo caso il driver elabora solo le chiamate ODBC. passa istruzioni SQL per motore di database per l'elaborazione. Ad esempio, i driver di Oracle sono driver basati su DBMS perché Oracle dispone di un motore di database autonomo che viene utilizzato il driver. In cui risiede il motore di database non ha importanza. Può risiedere nella stessa macchina del driver o un altro computer della rete. è possibile anche accedervi tramite un gateway.  
  
 Architettura del driver è in genere interessante solo per gli sviluppatori di driver; vale a dire, architettura del driver in genere non è rilevante per l'applicazione. Tuttavia, l'architettura può influire sulle se un'applicazione può usare SQL specifici del DBMS. Ad esempio, Microsoft Access offre un motore di database autonomo. Se un driver Microsoft Access è basato su DBMS, accede ai dati tramite questo motore - l'applicazione può passare le istruzioni SQL di Microsoft Access al motore per l'elaborazione.  
  
 Tuttavia, se il driver è basata su file, vale a dire, contiene un motore proprietario che accede direttamente - il file con estensione mdb di Microsoft® Access qualsiasi tentativo di passare le istruzioni SQL specifiche di Microsoft Access al motore di probabile comportare errori di sintassi. Il motivo è che il motore proprietario è probabile che implementare solo ODBC SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Driver basati su file](../../odbc/reference/file-based-drivers.md)  
  
-   [Driver basati su DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Esempio di rete](../../odbc/reference/network-example.md)  
  
-   [Altre architetture di driver](../../odbc/reference/other-driver-architectures.md)
