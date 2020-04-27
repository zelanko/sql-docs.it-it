---
title: DLL di traccia | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e1f9dc57415ad9865ca1b2ad02487b62a93f18f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "81298071"
---
# <a name="trace-dll"></a>DLL di traccia
La DLL che esegue la traccia è uno dei componenti di base di ODBC. La DLL di traccia è attualmente fornita come DLL di esempio nel componente ODBC del Windows SDK e in precedenza era incluso l'SDK di Microsoft Data Access Components (MDAC). Sono pertanto disponibili la voce del registro di sistema, l'interfaccia e il codice di esempio per la DLL di traccia. Questa DLL può essere sostituita da una DLL di traccia prodotta da un utente ODBC o da un fornitore di terze parti. A una DLL di traccia personalizzata deve essere assegnato un nome diverso da quello della DLL di traccia di esempio originale. È necessario installare le DLL di traccia nella directory di sistema. in caso contrario, il caricamento non verrà eseguito. Le stringhe di connessione non verranno passate alla DLL di traccia da Gestione driver.  
  
 La DLL di traccia traccia gli argomenti di input, gli argomenti di output, gli argomenti posticipati, i codici restituiti e i SQLSTATE. Quando la traccia è abilitata, gestione driver chiama la DLL di traccia in due punti: una volta alla voce della funzione (prima della convalida degli argomenti) e di nuovo immediatamente prima della restituzione della funzione.  
  
 Quando un'applicazione chiama una funzione, gestione driver chiama una funzione di traccia nella DLL di traccia prima di chiamare la funzione nel driver o di elaborare la chiamata stessa. Ogni funzione ODBC dispone di una funzione di traccia corrispondente (con prefisso *Trace*) identica alla funzione ODBC, ad eccezione del nome. Quando viene chiamata la funzione Trace, la DLL di traccia acquisisce gli argomenti di input e restituisce un codice restituito. Poiché la DLL di traccia viene chiamata prima che Gestione driver convalidi gli argomenti, vengono tracciate chiamate di funzione non valide, pertanto vengono registrati gli errori di transizione di stato e gli argomenti non validi.  
  
 Dopo aver chiamato la funzione Trace nella DLL di traccia, gestione driver chiama la funzione ODBC nel driver. Chiama quindi **TraceReturn** nella DLL di traccia. Questa funzione accetta due argomenti: il valore restituito dalla DLL di traccia per la funzione di traccia e il codice restituito restituito dal driver a gestione driver per la funzione ODBC (oppure il valore restituito da Gestione driver se ha elaborato la funzione). La funzione utilizza il valore restituito per la funzione Trace per modificare i valori degli argomenti di input acquisiti. Scrive il codice restituito per la funzione ODBC nel file di log (oppure lo Visualizza in modo dinamico, se abilitato). Dereferenzia i puntatori dell'argomento di output e registra i valori degli argomenti di output.
