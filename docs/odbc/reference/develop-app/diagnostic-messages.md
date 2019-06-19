---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 883cd29d8628f1e9270ae95a772c4d116b896710
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63034918"
---
# <a name="diagnostic-messages"></a>Messaggi di diagnostica
Viene restituito un messaggio di diagnostica con SQLSTATE ogni. Il valore SQLSTATE stesso spesso viene restituito con un numero di messaggi diversi. SQLSTATE 42000 (sintassi o violazione di accesso), ad esempio, viene restituito per la maggior parte degli errori nella sintassi SQL. Tuttavia, ogni errore di sintassi è probabile che essere descritti da un messaggio diverso.  
  
 Messaggi di diagnostica di esempio sono elencati nella colonna di errore nella tabella di SQLSTATE nell'appendice A e in ogni funzione. Anche se i driver possono restituire questi messaggi, sono più possibilità di restituire qualsiasi messaggio viene passato a essi per l'origine dati.  
  
 Le applicazioni in genere visualizzare messaggi di diagnostica all'utente, con il codice di errore nativo e SQLSTATE. Ciò consente all'utente e personale di supporto di determinano la causa di eventuali problemi. Le informazioni sul componente incorporati nel messaggio è particolarmente utile per eseguire questa operazione.  
  
 Messaggi di diagnostica provengono da origini dati e i componenti in una connessione ODBC, ad esempio, i gateway e la gestione di Driver. In genere, le origini dati non supportano direttamente ODBC. Di conseguenza, se un componente in una connessione ODBC riceve un messaggio da un'origine dati, è necessario identificare l'origine dati come origine del messaggio. Anche deve identificarsi come componente che riceve il messaggio.  
  
 Se l'origine dell'errore o avviso, è un componente stesso, il messaggio di diagnostica deve spiegare questo. Pertanto, il testo dei messaggi presenta due formati diversi. Per errori e avvisi che non sono presenti in un'origine dati, il messaggio di diagnostica debba usare questo formato:  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **]** *component-supplied-text*  
  
 Per errori e avvisi che si verificano in un'origine dati, il messaggio di diagnostica debba usare questo formato:  
  
 **[** *vendor-identifier* **][** *ODBC-component-identifier* **][** *data-source-identifier* **]** *data-source-supplied-text*  
  
 La tabella seguente illustra il significato di ogni elemento.  
  
|Elemento|Significato|  
|-------------|-------------|  
|*vendor-identifier*|Identifica il fornitore del componente in cui si è verificato l'errore o avviso o che hanno ricevuto l'errore o avviso direttamente dall'origine dati.|  
|*ODBC-component-identifier*|Identifica il componente in cui si è verificato l'errore o avviso o che hanno ricevuto l'errore o avviso direttamente dall'origine dati.|  
|*data-source-identifier*|Identifica l'origine dati. Per i driver basati su file, si tratta in genere un formato di file, ad esempio i driver basati su DBMS per Xbase [1], questo è il prodotto DBMS.|  
|*component-supplied-text*|Generato dal componente di ODBC.|  
|*data-source-supplied-text*|Generato dall'origine dati.|  
  
 [1] In questo caso, il driver viene utilizzato come il driver e l'origine dati.  
  
 Parentesi quadre ( **[]** ) deve essere incluso nel messaggio e non indicano elementi facoltativi.
