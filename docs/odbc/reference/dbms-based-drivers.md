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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111256"
---
# <a name="dbms-based-drivers"></a>Driver basati su DBMS
I driver basati su DBMS vengono utilizzati con origini dati quali Oracle o SQL Server che forniscono un motore di database autonomo che il driver deve utilizzare. Questi driver accedono ai dati fisici tramite il motore autonomo; ovvero inviano istruzioni SQL e recuperano i risultati dal motore.  
  
 Poiché i driver basati su DBMS utilizzano un motore di database esistente, sono in genere più facili da scrivere rispetto ai driver basati su file. Sebbene un driver basato su DBMS possa essere implementato facilmente mediante la conversione di chiamate ODBC a chiamate API native, ciò comporta un driver più lento. Un modo migliore per implementare un driver basato su DBMS consiste nell'usare il protocollo del flusso di dati sottostante, che corrisponde in genere all'API nativa. Ad esempio, un driver di SQL Server deve usare TDS (il protocollo del flusso di dati per SQL Server) anziché la libreria DB (l'API nativa per SQL Server). Un'eccezione a questa regola è quando ODBC è l'API nativa. Ad esempio, Watcom SQL è un motore autonomo che risiede nello stesso computer dell'applicazione e viene caricato direttamente come driver.  
  
 I driver basati su DBMS fungono da client in una configurazione client/server in cui l'origine dati funge da server. Nella maggior parte dei casi, il client (driver) e il server (origine dati) risiedono in computer diversi, anche se entrambi potrebbero risiedere nello stesso computer che esegue un sistema operativo multitasking. Una terza possibilità è un *Gateway,* che risiede tra il driver e l'origine dati. Un gateway è un componente software che fa sì che un DBMS sia simile a un altro. Ad esempio, le applicazioni scritte per usare SQL Server possono anche accedere ai dati DB2 tramite il gateway DecisionWare DB2 micro. Questo prodotto causa l'aspetto di DB2 come SQL Server.  
  
 Nella figura seguente sono illustrate tre diverse configurazioni di driver basati su DBMS. Nella prima configurazione, il driver e l'origine dati si trovano nello stesso computer. Nel secondo, il driver e l'origine dati si trovano in computer diversi. Nel terzo, il driver e l'origine dati si trovano in computer diversi e un gateway si trova tra di essi, risiedendo in un altro computer.  
  
 ![Tre configurazioni per i driver basati su&#45;DBMS](../../odbc/reference/media/pr07.gif "pr07")
