---
title: Uso di applicazioni a 16 bit e a 32 bit con driver a 32 bit | Microsoft Docs
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
ms.openlocfilehash: 941c821d7622b2364ec1cd417dd9b50302540b95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088169"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso delle applicazioni a 16 e 32 bit con driver a 32 bit
> [!IMPORTANT]  
>  il supporto per le applicazioni a 16 bit verrà rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Sviluppare invece applicazioni a 32 bit o a 64 bit.  
  
 Con il componente di accesso ai dati ODBC è possibile utilizzare applicazioni a 16 bit e a 32 bit con driver a 32 bit. I sistemi operativi Microsoft® Windows® 95/98 e Microsoft Windows NT®/Windows 2000 supportano le seguenti combinazioni di applicazioni e driver:  
  
-   applicazioni a 16 bit con driver a 32 bit  
  
-   applicazioni a 32 bit con driver a 32 bit  
  
 L'uso di un'applicazione a 32 bit con un driver a 16 bit non è supportato.  
  
> [!NOTE]  
>  A partire dal rilascio di ODBC versione 3,0, Windows NT 4,0 è supportato.  
  
 ODBC include i componenti ODBC necessari per supportare le configurazioni precedenti tramite il "thunk" di librerie a collegamento dinamico (dll) per convertire gli indirizzi a 16 bit in indirizzi a 32 bit e viceversa. Il programma di installazione determina il sistema operativo in uso e installa i componenti ODBC richiesti dal sistema. È inoltre possibile scegliere di installare i componenti ODBC utilizzati da tutti i sistemi.  
  
 Nella maggior parte dei casi, il porting di un'applicazione o di un driver da 16 bit a 32 bit prevede cinque tipi di modifiche:  
  
-   Modifiche al codice di gestione dei messaggi  
  
-   Modifiche perché i numeri interi e gli handle sono di 32 bit  
  
-   Modifiche alle chiamate alle API (Application Programming Interface) di Windows  
  
-   Modifiche per rendere il driver thread-safe  
  
-   Modifiche ai componenti ODBC  
  
 Dal punto di vista della programmazione di un'applicazione o di un driver, la differenza principale tra i componenti ODBC a 16 bit e a 32 bit è che hanno nomi file diversi. Dal punto di vista del sistema, l'architettura di ogni connessione di applicazione o driver è diversa e gli strumenti utilizzati per gestire le origini dati sono diversi.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Uso delle applicazioni a 16 bit con driver a 32 bit](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso delle applicazioni a 32 bit con driver a 32 bit](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
