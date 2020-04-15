---
title: Messaggi di diagnostica Documenti Microsoft
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
ms.openlocfilehash: be63e9d78960e40ac5e9ee016d2cfd868d99a922
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305832"
---
# <a name="diagnostic-messages"></a>Messaggi di diagnostica
Viene restituito un messaggio di diagnostica con ogni SQLSTATE. Lo stesso SQLSTATE viene spesso restituito con un numero di messaggi diversi. Ad esempio, SQLSTATE 42000 (errore di sintassi o violazione di accesso) viene restituito per la maggior parte degli errori nella sintassi SQL. Tuttavia, è probabile che ogni errore di sintassi venga descritto da un messaggio diverso.  
  
 I messaggi di diagnostica di esempio sono elencati nella colonna Errore nella tabella di SQLSTATEs nell'Appendice A e in ogni funzione. Anche se i driver possono restituire questi messaggi, è più probabile che restituiscano qualsiasi messaggio venga loro passato dall'origine dati.  
  
 Le applicazioni in genere visualizzano messaggi di diagnostica per l'utente, insieme al SQLSTATE e codice di errore nativo. Ciò consente all'utente e al personale di supporto di determinare la causa di eventuali problemi. Le informazioni sul componente incorporate nel messaggio sono particolarmente utili per eseguire questa operazione.  
  
 I messaggi di diagnostica provengono da origini dati e componenti in una connessione ODBC, ad esempio driver, gateway e Gestione Driver. In genere, le origini dati non supportano direttamente ODBC. Di conseguenza, se un componente in una connessione ODBC riceve un messaggio da un'origine dati, deve identificare l'origine dati come origine del messaggio. Deve inoltre identificarsi come componente che ha ricevuto il messaggio.  
  
 Se l'origine di un errore o avviso è un componente stesso, il messaggio di diagnostica deve spiegare questo. Pertanto, il testo dei messaggi ha due formati diversi. Per gli errori e gli avvisi che non si verificano in un'origine dati, il messaggio di diagnostica deve utilizzare questo formato:For errors and warnings that do not occur in a data source, the diagnostic message must use this format:  
  
 **[** *identificatore-fornitore* **][** *ODBC-component-identifier* **]** testo del componente *fornito*  
  
 Per gli errori e gli avvisi che si verificano in un'origine dati, il messaggio di diagnostica deve utilizzare questo formato:For errors and warnings that occur in a data source, the diagnostic message must use this format:  
  
 **[** *identificatore-fornitore* **][** *Identificatore-componente-ODBC* **][** *identificatore-origine dati* **]** *testo-origine dati*  
  
 Nella tabella seguente viene illustrato il significato di ogni elemento.  
  
|Elemento|Significato|  
|-------------|-------------|  
|*identificatore del fornitore*|Identifica il fornitore del componente in cui si è verificato l'errore o l'avviso o che ha ricevuto l'errore o l'avviso direttamente dall'origine dati.|  
|*Identificatore del componente ODBC*|Identifica il componente in cui si è verificato l'errore o l'avviso o che ha ricevuto l'errore o l'avviso direttamente dall'origine dati.|  
|*identificatore dell'origine dati*|Identifica l'origine dati. Per i driver basati su file, si tratta in genere di un formato di file, ad esempio Xbase[1] Per i driver basati su DBMS, si tratta del prodotto DBMS.|  
|*testo fornito dal componente*|Generato dal componente ODBC.|  
|*testo fornito dall'origine dati*|Generato dall'origine dati.|  
  
 [1] In questo caso, il driver agisce sia come driver che come origine dati.  
  
 Le parentesi quadre (**[ ]**) devono essere incluse nel messaggio e non indicano elementi facoltativi.
