---
title: Istruzioni SQL dinamiche | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbecd1d6db1d5ed77082253f6a6a57a96ceec4d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62628697"
---
# <a name="dynamic-sql"></a>SQL dinamica
Sebbene SQL statica funziona bene in molte situazioni, c'è una classe di applicazioni in cui l'accesso ai dati non è possibile determinare in anticipo. Si supponga, ad esempio, che un foglio di calcolo consente agli utenti di immettere una query, che il foglio di calcolo invia al sistema DBMS per recuperare i dati. Il contenuto di questa query ovviamente non può essere noto al programmatore quando viene scritto il programma di foglio di calcolo.  
  
 Per risolvere questo problema, il foglio di calcolo adotta un formato di embedded SQL denominato SQL dinamico. A differenza delle istruzioni SQL statiche, che sono impostate come hardcoded nel programma, le istruzioni SQL dinamiche possono essere compilate in fase di esecuzione e inserite in una variabile di stringa di host. Sono quindi inviati per il sistema DBMS per l'elaborazione. Poiché il sistema DBMS deve generare un piano di accesso in fase di esecuzione per le istruzioni SQL dinamiche, istruzioni SQL dinamiche è in genere più lento rispetto alle soluzioni SQL statico. Quando viene compilato un programma che contiene le istruzioni SQL dinamiche, le istruzioni SQL dinamiche non vengono rimossi dal programma, come in SQL statico. Al contrario, vengono sostituiti con una chiamata di funzione che passa l'istruzione per il sistema DBMS; istruzioni SQL statiche del programma stesso vengono gestite normalmente.  
  
 Il modo più semplice per eseguire un'istruzione SQL dinamica è con un'istruzione EXECUTE IMMEDIATE. Questa istruzione passa l'istruzione SQL per il sistema DBMS per la compilazione e l'esecuzione.  
  
 Uno svantaggio dell'istruzione EXECUTE immediata è che il sistema DBMS deve passare attraverso ognuno dei cinque passaggi di un'istruzione SQL ogni volta che viene eseguita l'istruzione di elaborazione. L'overhead necessario per questo processo può essere significativo se numerose istruzioni vengono eseguite in modo dinamico ed è dispendioso se tali istruzioni sono simili. Per risolvere questa situazione, SQL dinamico offre una forma ottimizzata di esecuzione denominata esecuzione preparata, che usa la procedura seguente:  
  
1.  Il programma genera un'istruzione SQL in un buffer, come avviene per l'istruzione EXECUTE IMMEDIATE. Invece di variabili host, un punto interrogativo (?) può essere sostituito per una costante in un punto qualsiasi nel testo dell'istruzione per indicare che un valore per la costante verrà fornito in un secondo momento. Il punto interrogativo viene chiamato come un marcatore di parametro.  
  
2.  Il programma passa l'istruzione SQL per il sistema DBMS con un'istruzione PREPARE, le richieste che il sistema DBMS analizza, eseguire la convalida e ottimizza l'istruzione e genera un'esecuzione piano. Il programma utilizza quindi un'istruzione EXECUTE (non un'istruzione EXECUTE IMMEDIATE) per eseguire l'istruzione PREPARE in un secondo momento. Passa i valori dei parametri per l'istruzione tramite una struttura di dati speciale denominata di SQL Data Area o SQLDA.  
  
3.  Il programma è possibile usare l'istruzione EXECUTE più volte, specificando i valori dei parametri diversi ogni volta che viene eseguita l'istruzione dinamica.  
  
 Esecuzione preparata è ancora non lo stesso come istruzione SQL statica. In SQL statico, i primi quattro passaggi dell'elaborazione di un'istruzione SQL è avvengono in fase di compilazione. In esecuzione preparata, questi passaggi vengono comunque eseguiti in fase di esecuzione, ma vengono eseguiti solo una volta. esecuzione del piano di viene eseguita solo quando viene chiamato EXECUTE. Ciò consente di eliminare alcuni degli svantaggi delle prestazioni inerenti nell'architettura di istruzioni SQL dinamiche. La figura seguente mostra le differenze tra SQL statico, istruzioni SQL dinamiche con esecuzione immediata e istruzioni SQL dinamiche con l'esecuzione preparata.
