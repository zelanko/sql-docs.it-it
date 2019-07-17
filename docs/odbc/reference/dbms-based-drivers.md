---
title: Driver basati su DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fcd2221d9a0bb9cba42745901e5f00a6f8c8415e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111256"
---
# <a name="dbms-based-drivers"></a>Driver basati su DBMS
Driver basati su DBMS vengono utilizzati con origini dati, ad esempio Oracle o SQL Server che forniscono un motore di database autonomo per il driver da usare. Questi driver accedere ai dati fisici tramite il motore autonomo; vale a dire, che invia istruzioni SQL per e recuperare i risultati dal motore.  
  
 Poiché i driver basati su DBMS usano un motore di database esistente, sono in genere la scrittura di driver basati su file. Anche se un driver basati su DBMS può essere implementato facilmente traducendo chiamate ODBC alle chiamate API native, ciò comporta un driver più lento. Un modo migliore per implementare un driver basati su DBMS è usare il protocollo di flusso dei dati sottostante, che avviene in genere l'API nativa. Ad esempio, un driver di SQL Server deve usare TDS (i dati di protocollo del flusso per SQL Server) anziché DB Library (API nativo per SQL Server). Un'eccezione a questa regola è quando ODBC è l'API nativa. Ad esempio, Watcom SQL è un motore autonomo che risiede nello stesso computer dell'applicazione e viene caricato direttamente perché il driver.  
  
 Driver basati su DBMS fungere da client a una configurazione del client/server in cui l'origine dati funge da server. Nella maggior parte dei casi, il client (driver) e il server (origine dati) si trovano in computer diversi, anche se entrambi possono risiedere nello stesso computer che eseguono un sistema operativo multitasking. Una terza possibilità è una *gateway,* che risiede tra i driver e l'origine dati. Un gateway è un componente software che provoca un DBMS simile a un altro. Ad esempio, le applicazioni scritte per utilizzare SQL Server possono anche accedere dati DB2 attraverso il Gateway di DB2 Decisionware Micro; Questo prodotto provoca DB2 simile a SQL Server.  
  
 La figura seguente mostra tre diverse configurazioni di driver basati su DBMS. Nella configurazione del primo, il driver e l'origine dati si trovano nello stesso computer. Nella seconda, il driver e l'origine dati si trovano in computer diversi. Nel terzo, i driver e l'origine dati si trovano in computer diversi e un gateway si trova tra di essi, che si trovano in un altro computer.  
  
 ![Tre configurazioni di DBMS&#45;basato su driver](../../odbc/reference/media/pr07.gif "pr07")
