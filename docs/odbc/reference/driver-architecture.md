---
title: Architettura dei driver - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ffe2023f028357468700b9bd995d22129ba06817
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294221"
---
# <a name="driver-architecture"></a>Architettura dei driver
L'architettura del driver rientra in due categorie, a seconda del software che elabora le istruzioni SQL:  
  
-   **Driver basati su file** Il driver accede direttamente ai dati fisici. In questo caso, il driver funge sia da driver che da origine dati; ovvero elabora le chiamate ODBC e le istruzioni SQL. Ad esempio, i driver dBASE sono driver basati su file perché dBASE non fornisce un motore di database autonomo che il driver può utilizzare. È importante notare che gli sviluppatori di driver basati su file devono scrivere i propri motori di database.  
  
-   **Driver basati su DBMS** Il driver accede ai dati fisici tramite un motore di database separato. In questo caso il driver elabora solo le chiamate ODBC; passa istruzioni SQL al motore di database per l'elaborazione. Ad esempio, i driver Oracle sono driver basati su DBMS perché Oracle dispone di un motore di database autonomo utilizzato dal driver. La posizione in cui risiede il motore di database non è rilevante. Può risiedere sulla stessa macchina del driver o di un altro computer sulla rete; potrebbe anche essere accessibile tramite un gateway.  
  
 L'architettura dei driver è in genere interessante solo per i driver writer; vale a dire, l'architettura dei driver in genere non fa alcuna differenza per l'applicazione. Tuttavia, l'architettura può influire se un'applicazione può utilizzare SQL specifico di DBMS. Ad esempio, Microsoft Access fornisce un motore di database autonomo. Se un driver di Microsoft Access è basato su DBMS, ovvero accede ai dati tramite questo motore, l'applicazione può passare le istruzioni Microsoft Access-SQL al motore per l'elaborazione.  
  
 Tuttavia, se il driver è basato su file, ovvero contiene un motore proprietario che accede direttamente al file con estensione mdb di Microsoft® Access, è probabile che qualsiasi tentativo di passare istruzioni SQL specifiche di Microsoft Access al motore comporterà errori di sintassi. Il motivo è che è probabile che il motore proprietario implementi solo ODBC SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Driver basati su file](../../odbc/reference/file-based-drivers.md)  
  
-   [Driver basati su DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Esempio di rete](../../odbc/reference/network-example.md)  
  
-   [Altre architetture di driver](../../odbc/reference/other-driver-architectures.md)
