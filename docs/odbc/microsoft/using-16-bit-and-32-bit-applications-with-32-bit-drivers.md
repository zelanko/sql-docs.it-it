---
title: Utilizzo di applicazioni a 16 e 32 bit con driver a 32 bit Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce996a7c4816d4d14491e226f891904b6cf8c02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307612"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 16 e 32 bit con driver a 32 bit
> [!IMPORTANT]  
>  Il supporto delle applicazioni a 16 bit verrà rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Sviluppare invece applicazioni a 32 bit o a 64 bit.  
  
 Con il componente di accesso ai dati ODBC, è possibile utilizzare applicazioni a 16 e 32 bit con driver a 32 bit. I sistemi operativi Microsoft® Windows® 95/98 e Microsoft Windows NT®/Windows 2000 supportano le seguenti combinazioni di applicazioni e driver:  
  
-   Applicazioni a 16 bit con driver a 32 bit  
  
-   Applicazioni a 32 bit con driver a 32 bit  
  
 L'utilizzo di un'applicazione a 32 bit con un driver a 16 bit non è supportato.  
  
> [!NOTE]  
>  A partire dal rilascio di ODBC versione 3.0, è stato supportato Windows NT 4.0.  
  
 ODBC include i componenti ODBC necessari per supportare le configurazioni precedenti mediante "thunking" librerie a collegamento dinamico (DLL) per convertire gli indirizzi a 16 bit in indirizzi a 32 bit e viceversa. Il programma di installazione determina il sistema operativo in uso e installa i componenti ODBC richiesti da tale sistema. È inoltre possibile scegliere di installare i componenti ODBC utilizzati da tutti i sistemi.  
  
 Nella maggior parte dei casi, il porting di un'applicazione o di un driver da 16 bit a 32 bit comporta cinque tipi di modifiche:  
  
-   Modifiche al codice di gestione dei messaggiChanges to message-handling code  
  
-   Modifiche perché i numeri interi e le maniglie sono 32 bitChanges because integers and handles are 32 bits  
  
-   Modifiche nelle chiamate alle API (Application Programming Interface) di WindowsChanges in calls to Windows Application programming interfaces (APIs)  
  
-   Modifiche per rendere il driver thread-safe  
  
-   Modifiche ai componenti ODBC  
  
 Dal punto di vista della programmazione di un'applicazione o di un driver, la differenza principale tra i componenti ODBC a 16 bit e a 32 bit consiste nel fatto che hanno nomi di file diversi. Dal punto di vista del sistema, l'architettura di ogni connessione di applicazioni o driver è diversa e gli strumenti utilizzati per gestire le origini dati sono diversi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Uso delle applicazioni a 16 bit con driver a 32 bit](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso delle applicazioni a 32 bit con driver a 32 bit](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
