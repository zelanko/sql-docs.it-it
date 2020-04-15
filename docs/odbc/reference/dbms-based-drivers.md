---
title: Driver basati su DBMS Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e7b7b153d0b0cb0a3e6a3d738908b0039b95679
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306487"
---
# <a name="dbms-based-drivers"></a>Driver basati su DBMS
I driver basati su DBMS vengono utilizzati con origini dati come Oracle o SQL Server che forniscono un motore di database autonomo per il driver da utilizzare. Questi driver accedono ai dati fisici tramite il motore autonomo; ovvero inviano istruzioni SQL e recuperano i risultati dal motore.  
  
 Poiché i driver basati su DBMS utilizzano un motore di database esistente, in genere sono più semplici da scrivere rispetto ai driver basati su file. Anche se un driver basato su DBMS può essere facilmente implementato traducendo le chiamate ODBC in chiamate API native, ciò comporta un driver più lento. Un modo migliore per implementare un driver basato su DBMS consiste nell'utilizzare il protocollo del flusso di dati sottostante, che in genere è ciò che fa l'API nativa. Ad esempio, un driver di SQL Server deve utilizzare TDS (il protocollo del flusso di dati per SQL Server) anziché Libreria di database (l'API nativa per SQL Server). Un'eccezione a questa regola è quando ODBC è l'API nativa. Ad esempio, Watcom SQL è un motore autonomo che risiede sullo stesso computer dell'applicazione e viene caricato direttamente come driver.  
  
 I driver basati su DBMS fungono da client in una configurazione client/server in cui l'origine dati funge da server. Nella maggior parte dei casi, il client (driver) e il server (origine dati) risiedono su computer diversi, anche se entrambi potrebbero risiedere sullo stesso computer che esegue un sistema operativo multitasking. Una terza possibilità è un *gateway,* che si trova tra il driver e l'origine dati. Un gateway è un software che fa sì che un DBMS assomigli a un altro. Ad esempio, le applicazioni scritte per l'utilizzo di SQL Server possono accedere ai dati DB2 anche tramite il gateway Micro Decisionware DB2; questo prodotto fa sì che DB2 per assomigliare a SQL Server.  
  
 Nella figura seguente vengono illustrate tre diverse configurazioni di driver basati su DBMS. Nella prima configurazione, il driver e l'origine dati risiedono sullo stesso computer. Nel secondo, il driver e l'origine dati risiedono su computer diversi. Nel terzo, il driver e l'origine dati risiedono su computer diversi e un gateway si trova tra di essi, risiedendo su un altro computer.  
  
 ![Tre configurazioni per i driver basati su&#45;DBMS](../../odbc/reference/media/pr07.gif "pr07 (in questo modo)")
