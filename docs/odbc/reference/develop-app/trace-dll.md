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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7a99f6c2960600d62a789471f68c1f5da89ae8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148860"
---
# <a name="trace-dll"></a>DLL di traccia
La DLL che esegue la traccia è uno dei componenti principali di ODBC. La traccia DLL viene attualmente fornito come esempio DLL nel componente di ODBC di Windows SDK ed è stato incluso in precedenza Microsoft Data Access Components (MDAC) SDK. Pertanto, la voce del Registro di sistema, l'interfaccia e codice di esempio per la DLL di traccia sono disponibili. Questa DLL può essere sostituita da una traccia DLL prodotto da un utente ODBC o un fornitore di terze parti. Una traccia personalizzata DLL necessario assegnare un nome diverso da quello della traccia di esempio DLL originale. DLL di traccia deve essere installata nella directory di sistema, o non riuscirà a caricare. Le stringhe di connessione non verrà passate alla DLL di traccia da Gestione Driver.  
  
 La traccia DLL tiene traccia di argomenti di input, degli argomenti di output, argomenti posticipati, codici restituiti e SQLState. Quando la traccia è abilitata, gestione Driver chiama la DLL di traccia in due punti: una volta immesse funzioni (prima della convalida degli argomenti) e anche in questo caso appena prima che la funzione restituisce.  
  
 Quando un'applicazione chiama una funzione, gestione Driver chiama una funzione di traccia nella traccia DLL prima di chiamare la funzione nel driver o la chiamata di elaborazione. Ogni funzione ODBC dispone di una funzione di traccia corrispondente (con prefisso *traccia*) che è identico alla funzione ODBC fatta eccezione per il nome. Quando viene chiamata la funzione di traccia, traccia DLL acquisisce gli argomenti di input e restituisce un codice restituito. Poiché la DLL di traccia viene chiamata prima che Gestione Driver convalida gli argomenti, vengono tracciate le chiamate di funzione non è valido, in modo che gli errori di transizione di stato e gli argomenti non validi vengono registrati.  
  
 Dopo avere chiamato la funzione di traccia nella traccia DLL, gestione Driver chiama la funzione ODBC nel driver. Chiama poi **TraceReturn** nella traccia DLL. Questa funzione accetta due argomenti: il valore restituito dalla traccia DLL per la funzione di traccia e il codice restituito restituiti dal driver da Gestione Driver per la funzione ODBC (o il valore restituito da Gestione Driver stesso se la funzione elaborata). La funzione Usa il valore restituito per la funzione di traccia per modificare i valori di argomento di input acquisita. Scrive il codice restituito per la funzione ODBC al file di log (o viene visualizzata, in modo dinamico, se abilitato). Consente di dereferenziare i puntatori dell'argomento di output e registra i valori di argomento di output.
