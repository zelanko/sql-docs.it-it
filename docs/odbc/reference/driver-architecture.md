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
ms.openlocfilehash: fd9bbb74d77a0b56b6b1f1aa5d8f1a6b5e97f5aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915469"
---
# <a name="driver-architecture"></a>Architettura dei driver
L'architettura del driver rientra in due categorie, a seconda del software che elabora istruzioni SQL:  
  
-   **Driver basati su file** Il driver accede direttamente ai dati fisici. In questo caso, il driver funge da driver e origine dati. ovvero elabora le chiamate ODBC e le istruzioni SQL. I driver dBASE, ad esempio, sono driver basati su file perché dBASE non fornisce un motore di database autonomo che può essere utilizzato dal driver. È importante notare che gli sviluppatori di driver basati su file devono scrivere i propri motori di database.  
  
-   **Driver basati su DBMS** Il driver accede ai dati fisici tramite un motore di database separato. In questo caso il driver elabora solo le chiamate ODBC; passa istruzioni SQL al motore di database per l'elaborazione. I driver Oracle, ad esempio, sono driver basati su DBMS perché Oracle dispone di un motore di database autonomo utilizzato dal driver. La posizione in cui risiede il motore di database è irrilevante. Può risiedere nello stesso computer del driver o di un altro computer nella rete; è anche possibile accedervi tramite un gateway.  
  
 L'architettura del driver è in genere interessante solo per i writer di driver; l'architettura dei driver, in genere, non fa alcuna differenza per l'applicazione. Tuttavia, l'architettura può influire sul fatto che un'applicazione possa usare SQL specifico di DBMS. Ad esempio, Microsoft Access fornisce un motore di database autonomo. Se un driver Microsoft Access è basato su DBMS, accede ai dati tramite questo motore. l'applicazione può passare le istruzioni Microsoft Access-SQL al motore per l'elaborazione.  
  
 Tuttavia, se il driver è basato su file, ovvero contiene un motore proprietario che accede direttamente al file con estensione mdb di Microsoft® Access, qualsiasi tentativo di passare istruzioni SQL specifiche di Microsoft Access al motore causa probabilmente errori di sintassi. Il motivo è che il motore proprietario può implementare solo ODBC SQL.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Driver basati su file](../../odbc/reference/file-based-drivers.md)  
  
-   [Driver basati su DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Esempio di rete](../../odbc/reference/network-example.md)  
  
-   [Altre architetture di driver](../../odbc/reference/other-driver-architectures.md)
