---
title: Compilazione di un programma SQL incorporato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc8133241ad0b76579e87164350a5c6fe2a39f2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186338"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilazione di un programma Embedded SQL
Poiché un programma SQL incorporato contiene una combinazione delle istruzioni del linguaggio SQL e host, non possono essere inviata direttamente a un compilatore per il linguaggio host. Al contrario, viene compilato tramite un processo in più passaggi. Anche se questo processo è diverso da prodotto a prodotto, i passaggi sono all'incirca lo stesso per tutti i prodotti.  
  
 Questa illustrazione mostra i passaggi necessari per compilare un programma SQL incorporato.  
  
 ![Passaggi per la compilazione di un programma SQL incorporato](../../odbc/reference/media/pr02.gif "pr02")  
  
 Cinque passaggi coinvolti nella compilazione di un programma SQL incorporato:  
  
1.  Il programma SQL incorporato viene inviato a precompilatore il SQL, uno strumento di programmazione. Il precompilatore analizza il programma, individua le istruzioni SQL incorporate e li elabora. Un precompilatore diverso è necessario per ogni linguaggio di programmazione supportato dal sistema DBMS. Prodotti DBMS offrono in genere precompilers per uno o più lingue, tra cui C, Pascal, COBOL, Fortran, Ada, PL / I e vari linguaggi assembly.  
  
2.  Il precompilatore produce due file di output. Il primo file è il file di origine, privato di relative istruzioni SQL incorporate. Al loro posto i precompilatore sostituisce con chiamate alle routine DBMS proprietari che forniscono il collegamento in fase di esecuzione tra il programma e il sistema DBMS. In genere, i nomi e le sequenze di queste routine chiamate sono note solo al precompilatore e del sistema DBMS; non sono un'interfaccia pubblica per il sistema DBMS. Il secondo file è una copia di tutte le istruzioni di SQL incorporate nel programma. Questo file viene chiamato talvolta un modulo di richiesta di database o nome DBRM.  
  
3.  L'output del file di origine dal precompilatore viene inviato al compilatore standard per l'host di linguaggio (ad esempio un compilatore C o COBOL) di programmazione. Il compilatore elabora il codice sorgente e produce codice dell'oggetto come output. Si noti che questo passaggio non ha nulla a che fare con il sistema DBMS o SQL.  
  
4.  Il linker accetta i moduli di oggetto generati dal compilatore, li collega con diverse routine di libreria e produce un programma eseguibile. Le routine della libreria collegate nel programma eseguibile includono le routine DBMS proprietarie descritte nel passaggio 2.  
  
5.  Il modulo di richiesta database generato dallo strumento di precompilazione viene inviato a un'utilità di binding speciali. Questa utilità esamina le istruzioni SQL, analizza, convalida e ottimizzarli e produce quindi un piano di accesso per ogni istruzione. Il risultato è un piano di accesso combinato per l'intero programma, che rappresenta una versione eseguibile delle istruzioni SQL incorporate. L'utilità di associazione archivia il piano nel database, in genere assegnarle il nome dell'applicazione che verrà usato. Indica se questo passaggio viene eseguita in fase di compilazione o fase di esecuzione varia a seconda del sistema DBMS.  
  
 Si noti che i passaggi necessari per compilare un programma SQL incorporato correlare strettamente con i passaggi descritti nella sezione precedente [elaborazione di un'istruzione SQL](../../odbc/reference/processing-a-sql-statement.md). In particolare, si noti che il precompilatore separa le istruzioni SQL dal codice del linguaggio host e l'utilità di associazione consente di analizzare e convalida le istruzioni SQL e crea i piani di accesso. In DBMS in cui il passaggio 5 viene eseguita in fase di compilazione, i primi quattro passaggi dell'elaborazione di un'istruzione SQL avvengono in fase di compilazione, mentre l'ultimo passaggio (esecuzione) viene eseguita in fase di esecuzione. Ciò ha lo scopo di rendere l'esecuzione di query in questo tipo DBMS molto veloce.
