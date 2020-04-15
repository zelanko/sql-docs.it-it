---
title: 'DLL di traccia: Documenti Microsoft'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298071"
---
# <a name="trace-dll"></a>DLL di traccia
La DLL che esegue l'analisi è uno dei componenti principali di ODBC. La DLL di traccia è attualmente fornita come DLL di esempio nel componente ODBC di Windows SDK ed è stata precedentemente inclusa nell'SDK di Microsoft Data Access Components (MDAC). Di conseguenza, sono disponibili la voce del Registro di sistema, l'interfaccia e il codice di esempio per la DLL di traccia. Questa DLL può essere sostituita da una DLL di traccia prodotta da un utente ODBC o da un fornitore di terze parti. A una DLL di traccia personalizzata deve essere assegnato un nome diverso da quello della DLL di traccia di esempio originale. Le DLL di traccia devono essere installate nella directory di sistema, altrimenti non verranno caricate. Le stringhe di connessione non verranno passate alla DLL di traccia da Gestione Driver.  
  
 La DLL di traccia tiene traccia degli argomenti di input, degli argomenti di output, degli argomenti posticipati, dei codici restituiti e delle SQLSTATE. Quando la traccia è abilitata, Gestione Driver chiama la DLL di traccia in due punti: una volta all'immissione della funzione (prima della convalida dell'argomento) e di nuovo appena prima che la funzione restituisce.  
  
 Quando un'applicazione chiama una funzione, Gestione Driver chiama una funzione di traccia nella DLL di traccia prima di chiamare la funzione nel driver o l'elaborazione della chiamata stessa. Ogni funzione ODBC dispone di una funzione di traccia corrispondente (con prefisso *Trace*) identica alla funzione ODBC, con l'eccezione del nome. Quando viene chiamata la funzione di traccia, la DLL di traccia acquisisce gli argomenti di input e restituisce un codice restituito. Poiché la DLL di traccia viene chiamata prima che Gestione Driver convalida gli argomenti, vengono tracciate le chiamate di funzione non valide, pertanto vengono registrati gli errori di transizione dello stato e gli argomenti non validi.  
  
 Dopo aver chiamato la funzione di traccia nella DLL di traccia, Gestione Driver chiama la funzione ODBC nel driver. Chiama quindi **TraceReturn** nella DLL di traccia. Questa funzione accetta due argomenti: il valore restituito dalla DLL di traccia per la funzione di traccia e il codice restituito dal driver a Gestione Driver per la funzione ODBC (o il valore restituito da Gestione Driver stesso se ha elaborato la funzione). La funzione utilizza il valore restituito per la funzione di traccia per modificare i valori degli argomenti di input acquisiti. Scrive il codice restituito per la funzione ODBC nel file di registro (o lo visualizza in modo dinamico, se abilitato). Dereferenzia i puntatori agli argomenti di output e registra i valori degli argomenti di output.
