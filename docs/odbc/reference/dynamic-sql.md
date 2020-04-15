---
title: 'Sql Dinamico : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56419723540114f122be2582f0de7c7e7d0c54f3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306689"
---
# <a name="dynamic-sql"></a>SQL dinamica
Sebbene SQL statico funzioni bene in molte situazioni, esiste una classe di applicazioni in cui non è possibile determinare in anticipo l'accesso ai dati. Si supponga, ad esempio, che un foglio di calcolo consenta a un utente di immettere una query, che il foglio di calcolo invia quindi al DBMS per recuperare i dati. Il contenuto di questa query ovviamente non può essere noto al programmatore quando viene scritto il programma foglio di calcolo.  
  
 Per risolvere questo problema, il foglio di calcolo utilizza una forma di SQL incorporato denominato SQL dinamico. A differenza delle istruzioni SQL statiche, che sono hardcoded nel programma, le istruzioni SQL dinamiche possono essere compilate in fase di esecuzione e inserite in una variabile host stringa. Vengono quindi inviati al DBMS per l'elaborazione. Poiché il DBMS deve generare un piano di accesso in fase di esecuzione per le istruzioni SQL dinamiche, SQL dinamico è in genere più lento di SQL statico. Quando viene compilato un programma contenente istruzioni SQL dinamiche, le istruzioni SQL dinamiche non vengono rimosse dal programma, come in SQL statico. Al contrario, vengono sostituiti da una chiamata di funzione che passa l'istruzione al DBMS; Le istruzioni SQL statiche nello stesso programma vengono trattate normalmente.  
  
 Il modo più semplice per eseguire un'istruzione SQL dinamica è con un'istruzione EXECUTE IMMEDIATE. Questa istruzione passa l'istruzione SQL al dbMS per la compilazione e l'esecuzione.  
  
 Uno svantaggio dell'istruzione EXECUTE IMMEDIATE è che il DBMS deve eseguire ognuno dei cinque passaggi dell'elaborazione di un'istruzione SQL ogni volta che viene eseguita l'istruzione. L'overhead coinvolto in questo processo può essere significativo se molte istruzioni vengono eseguite in modo dinamico ed è dispendioso se tali istruzioni sono simili. Per risolvere questa situazione, SQL dinamico offre una forma ottimizzata di esecuzione denominata esecuzione preparata, che utilizza i passaggi seguenti:  
  
1.  Il programma costruisce un'istruzione SQL in un buffer, come per l'istruzione EXECUTE IMMEDIATE. Anziché le variabili host, un punto interrogativo (?) può essere sostituito da una costante in qualsiasi punto del testo dell'istruzione per indicare che verrà fornito un valore per la costante in un secondo momento. Il punto interrogativo viene chiamato come marcatore di parametro.  
  
2.  Il programma passa l'istruzione SQL al DBMS con un'istruzione PREPARE, che richiede che DBMS analizzi, convalidi e ottimizzi l'istruzione e generi un piano di esecuzione per essa. Il programma utilizza quindi un'istruzione EXECUTE (non un'istruzione EXECUTE IMMEDIATE) per eseguire l'istruzione PREPARE in un secondo momento. Passa i valori dei parametri per l'istruzione tramite una struttura di dati speciale denominata area dati SQL o SQLDA.  
  
3.  Il programma può utilizzare ripetutamente l'istruzione EXECUTE, fornendo valori di parametro diversi ogni volta che viene eseguita l'istruzione dinamica.  
  
 L'esecuzione preparata non è ancora uguale a SQL statico. In SQL statico, i primi quattro passaggi dell'elaborazione di un'istruzione SQL vengono eseguiti in fase di compilazione. Nell'esecuzione preparata, questi passaggi vengono comunque eseguiti in fase di esecuzione, ma vengono eseguiti una sola volta. l'esecuzione del piano avviene solo quando viene chiamato EXECUTE. Ciò consente di eliminare alcuni degli svantaggi in termini di prestazioni inerenti all'architettura di SQL dinamico. Nella figura seguente vengono illustrate le differenze tra SQL statico, SQL dinamico con esecuzione immediata e SQL dinamico con esecuzione preparata.
