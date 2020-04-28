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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306532"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilazione di un programma Embedded SQL
Poiché un programma SQL incorporato contiene una combinazione di istruzioni SQL e del linguaggio host, non può essere inviato direttamente a un compilatore per la lingua host. Viene invece compilato tramite un processo a più passaggi. Sebbene questo processo sia diverso da prodotto a prodotto, la procedura è approssimativamente la stessa per tutti i prodotti.  
  
 Questa illustrazione mostra i passaggi necessari per compilare un programma SQL incorporato.  
  
 ![Passaggi per la compilazione di un programma SQL incorporato](../../odbc/reference/media/pr02.gif "PR02")  
  
 Per la compilazione di un programma SQL incorporato sono necessari cinque passaggi:  
  
1.  Il programma SQL incorporato viene inviato al precompilatore SQL, uno strumento di programmazione. Il precompilatore analizza il programma, trova le istruzioni SQL incorporate e le elabora. È necessario un precompilatore diverso per ogni linguaggio di programmazione supportato dal sistema DBMS. I prodotti DBMS offrono in genere compilatori per uno o più linguaggi, tra cui C, Pascal, COBOL, FORTRAN, Ada, pl/I e vari linguaggi di assembly.  
  
2.  Il precompilatore produce due file di output. Il primo file è il file di origine, rimosso dalle istruzioni SQL incorporate. Al suo posto, il preprocessore sostituisce le chiamate alle routine DBMS proprietarie che forniscono il collegamento di run-time tra il programma e il sistema DBMS. In genere, i nomi e le sequenze di chiamata di queste routine sono noti solo per il preprocessore e il sistema DBMS; non sono un'interfaccia pubblica per il sistema DBMS. Il secondo file è una copia di tutte le istruzioni SQL incorporate utilizzate nel programma. Questo file viene talvolta definito modulo di richiesta di database o DBRM.  
  
3.  L'output del file di origine del precompilatore viene inviato al compilatore standard per il linguaggio di programmazione host, ad esempio un compilatore C o COBOL. Il compilatore elabora il codice sorgente e genera il codice oggetto come output. Si noti che questo passaggio non ha nulla a che fare con il sistema DBMS o con SQL.  
  
4.  Il linker accetta i moduli oggetto generati dal compilatore, li collega a diverse routine di libreria e genera un programma eseguibile. Le routine della libreria collegate al programma eseguibile includono le routine DBMS proprietarie descritte nel passaggio 2.  
  
5.  Il modulo di richiesta di database generato dal precompilatore viene inviato a un'utilità di associazione speciale. Questa utilità esamina le istruzioni SQL, le analizza, le convalida e le ottimizza, quindi produce un piano di accesso per ogni istruzione. Il risultato è un piano di accesso combinato per l'intero programma, che rappresenta una versione eseguibile delle istruzioni SQL incorporate. L'utilità di associazione archivia il piano nel database, assegnando in genere il nome del programma applicativo che lo utilizzerà. Il fatto che questo passaggio avvenga in fase di compilazione o di esecuzione dipende dal sistema DBMS.  
  
 Si noti che i passaggi utilizzati per compilare un programma SQL incorporato sono strettamente correlati alla procedura descritta in precedenza nell' [elaborazione di un'istruzione SQL](../../odbc/reference/processing-a-sql-statement.md). In particolare, si noti che il precompilatore separa le istruzioni SQL dal codice della lingua host e l'utilità di associazione analizza e convalida le istruzioni SQL e crea i piani di accesso. Nei sistemi DBMS in cui il passaggio 5 avviene in fase di compilazione, i primi quattro passaggi di elaborazione di un'istruzione SQL avvengono in fase di compilazione, mentre l'ultimo passaggio (esecuzione) avviene in fase di esecuzione. Questo ha l'effetto di rendere molto veloce l'esecuzione delle query in tali DBMS.
