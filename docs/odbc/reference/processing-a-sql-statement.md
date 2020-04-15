---
title: Elaborazione di un'istruzione SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280521"
---
# <a name="processing-a-sql-statement"></a>Elaborazione di un'istruzione SQL
Prima di illustrare le tecniche per l'utilizzo di SQL a livello di codice, è necessario illustrare come viene elaborata un'istruzione SQL. I passaggi necessari sono comuni a tutte e tre le tecniche, anche se ogni tecnica le esegue in momenti diversi. Nella figura seguente vengono illustrati i passaggi necessari per l'elaborazione di un'istruzione SQL, illustrati nella parte restante di questa sezione.  
  
 ![Passaggi per l'elaborazione di un'istruzione SQL](../../odbc/reference/media/pr01.gif "pr01 (in questo modo)")  
  
 Per elaborare un'istruzione SQL, un DBMS esegue i cinque passaggi seguenti:To process an SQL statement, a DBMS performs the following five steps:  
  
1.  Il DBMS analizza innanzitutto l'istruzione SQL. Suddivide l'istruzione in singole parole, denominate token, assicura che l'istruzione abbia un verbo valido e clausole valide e così via. Gli errori di sintassi e gli errori di ortografia possono essere rilevati in questo passaggio.  
  
2.  Il DBMS convalida l'istruzione. Confronta l'istruzione rispetto al catalogo di sistema. Tutte le tabelle denominate nell'istruzione esistono nel database? Tutte le colonne esistono e i nomi delle colonne non sono ambigui? L'utente dispone dei privilegi necessari per eseguire l'istruzione? Alcuni errori semantici possono essere rilevati in questo passaggio.  
  
3.  Il DBMS genera un piano di accesso per l'istruzione. Il piano di accesso è una rappresentazione binaria dei passaggi necessari per eseguire l'istruzione; è l'equivalente DBMS del codice eseguibile.  
  
4.  Il DBMS ottimizza il piano di accesso. Esplora vari modi per realizzare il piano di accesso. È possibile utilizzare un indice per velocizzare una ricerca? Il DBMS deve prima applicare una condizione di ricerca alla tabella A e quindi unirla alla tabella B oppure iniziare con il join e utilizzare la condizione di ricerca in un secondo momento? È possibile evitare o ridurre una ricerca sequenziale in una tabella a un sottoinsieme della tabella? Dopo aver esplorato le alternative, il DBMS sceglie una di esse.  
  
5.  Il DBMS esegue l'istruzione eseguendo il piano di accesso.  
  
 I passaggi utilizzati per elaborare un'istruzione SQL variano in base alla quantità di accesso al database richiesta e alla quantità di tempo necessaria. L'analisi di un'istruzione SQL non richiede l'accesso al database e può essere eseguita molto rapidamente. L'ottimizzazione, d'altra parte, è un processo che richiede un utilizzo intensivo della CPU e richiede l'accesso al catalogo di sistema. Per una query complessa e multitabella, l'ottimizzatore può esplorare migliaia di modi diversi di eseguire la stessa query. Tuttavia, il costo dell'esecuzione della query in modo inefficiente è in genere così elevato che il tempo impiegato per l'ottimizzazione è più che riacquistato in una maggiore velocità di esecuzione della query. Ciò è ancora più significativo se lo stesso piano di accesso ottimizzato può essere utilizzato più e più volte per eseguire query ripetitive.
