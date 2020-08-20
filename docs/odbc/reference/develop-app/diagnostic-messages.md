---
description: Messaggi di diagnostica
title: Messaggi di diagnostica | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic messages messages
- error messages [ODBC], diagnostic messages
- diagnostic messages [ODBC]
ms.assetid: 98027871-9901-476e-a722-ee58b7723c1f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d788a8bb23b7b63ae65a6fcf8c119110b5e6557
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461513"
---
# <a name="diagnostic-messages"></a>Messaggi di diagnostica
Viene restituito un messaggio di diagnostica con ogni SQLSTATE. Lo stesso SQLSTATE viene spesso restituito con una serie di messaggi diversi. Per la maggior parte degli errori nella sintassi SQL, ad esempio, viene restituito SQLSTATE 42000 (errore di sintassi o violazione di accesso). Tuttavia, ogni errore di sintassi è probabilmente descritto da un messaggio diverso.  
  
 I messaggi di diagnostica di esempio sono elencati nella colonna Error della tabella di sqlstates nell'Appendice A e in ogni funzione. Sebbene i driver possano restituire questi messaggi, è più probabile che vengano restituiti tutti i messaggi che vengono passati dall'origine dati.  
  
 Le applicazioni in genere visualizzano i messaggi di diagnostica per l'utente, insieme al codice di errore SQLSTATE e nativo. Questo consente all'utente e al personale del supporto di determinare la cause di eventuali problemi. Le informazioni sui componenti incorporate nel messaggio sono particolarmente utili per questa operazione.  
  
 I messaggi di diagnostica provengono da origini dati e componenti in una connessione ODBC, ad esempio driver, gateway e gestione driver. In genere, le origini dati non supportano direttamente ODBC. Di conseguenza, se un componente in una connessione ODBC riceve un messaggio da un'origine dati, deve identificare l'origine dati come origine del messaggio. Deve inoltre identificarsi come componente che ha ricevuto il messaggio.  
  
 Se l'origine di un errore o di un avviso è un componente, il messaggio di diagnostica deve spiegarlo. Il testo dei messaggi, pertanto, presenta due formati diversi. Per gli errori e gli avvisi che non si verificano in un'origine dati, il messaggio di diagnostica deve utilizzare il formato seguente:  
  
 **[** *identificatore-fornitore* **] [** *ODBC-Component-Identifier* **]** *fornito dal componente-testo*  
  
 Per gli errori e gli avvisi che si verificano in un'origine dati, il messaggio di diagnostica deve utilizzare il formato seguente:  
  
 **[** *Vendor-Identifier* **] [** *ODBC-Component-Identifier* **] [** *Data-Source-Identifier* **]** *Data-Source-fornito-text*  
  
 La tabella seguente illustra il significato di ogni elemento.  
  
|Elemento|Significato|  
|-------------|-------------|  
|*identificatore fornitore*|Identifica il fornitore del componente in cui si è verificato l'errore o l'avviso o che ha ricevuto l'errore o l'avviso direttamente dall'origine dati.|  
|*ODBC-Component-Identifier*|Identifica il componente in cui si è verificato l'errore o l'avviso o che ha ricevuto l'errore o l'avviso direttamente dall'origine dati.|  
|*ID origine dati*|Identifica l'origine dati. Per i driver basati su file, si tratta in genere di un formato di file, ad esempio Xbase [1] per i driver basati su DBMS, questo è il prodotto DBMS.|  
|*testo fornito dal componente*|Generato dal componente ODBC.|  
|*Data Source-fornito-testo*|Generato dall'origine dati.|  
  
 [1] in questo caso, il driver funge sia dal driver che dall'origine dati.  
  
 Le parentesi quadre (**[]**) devono essere incluse nel messaggio e non indicano elementi facoltativi.
