---
title: Uso delle applicazioni a 16 bit e a 32 bit con driver a 32 Bit | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8540983b84d4d39fe5a02b92a1e3a3606350d36d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209991"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 16 e 32 bit con driver a 32 bit
> [!IMPORTANT]  
>  supporto di applicazioni a 16 bit verrà rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa possibile sviluppare applicazioni a 32 o 64 bit.  
  
 Con il componente di accesso ai dati ODBC, è possibile usare le applicazioni a 16 bit e a 32 bit con driver a 32 bit. Sistemi operativi Microsoft® Windows® 95 o 98 e 2000 di Microsoft Windows/Windows supportano le combinazioni seguenti di applicazioni e driver:  
  
-   applicazioni a 16 bit con driver a 32 bit  
  
-   applicazioni a 32 bit con driver a 32 bit  
  
 Usando un'applicazione a 32 bit con driver a 16 bit non è supportato.  
  
> [!NOTE]  
>  Iniziare con la versione di ODBC versione 3.0, Windows NT 4.0 è supportata.  
  
 ODBC include i componenti ODBC necessari per supportare le configurazioni sopra "thunk" librerie a collegamento dinamico (DLL) per convertire gli indirizzi di 16 bit in indirizzi a 32 bit e viceversa. Il programma di installazione determina quale sistema operativo si utilizza e installa i componenti ODBC richiesti da tale sistema. È anche possibile scegliere di installare i componenti ODBC utilizzati da tutti i sistemi.  
  
 Nella maggior parte dei casi, il porting di un'applicazione o driver da 16 bit a 32 bit prevede cinque tipi di modifiche:  
  
-   Modifiche al codice di gestione dei messaggi  
  
-   Modifica perché sono numeri interi e gli handle a 32 bit  
  
-   Modifiche nelle chiamate a application programming interface (API) Windows  
  
-   Modifiche per rendere il driver thread-safe  
  
-   Modifiche ai componenti ODBC  
  
 Da un'applicazione o il driver programmazione punto di vista, la differenza principale tra i componenti ODBC 16 bit e a 32 bit sia che abbiano nomi di file diverso. Dal punto di vista di sistema, l'architettura di ogni connessione dell'applicazione o il driver è diversa e gli strumenti utilizzati per gestire le origini dati sono diversi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Uso delle applicazioni a 16 bit con driver a 32 bit](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso delle applicazioni a 32 bit con driver a 32 bit](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
