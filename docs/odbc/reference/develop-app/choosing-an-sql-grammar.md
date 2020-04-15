---
title: Scelta di una grammatica SQL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], SQL grammar
- SQL grammar [ODBC], selecting
ms.assetid: 4e0d189b-e407-47e0-92a9-f9982230dd0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299161"
---
# <a name="choosing-an-sql-grammar"></a>Scelta di una grammatica SQL
La prima decisione da prendere quando si costruiscono istruzioni SQL è la grammatica da utilizzare. Oltre alle grammatiche disponibili nei vari organismi di standard, come Open Group, ANSI e ISO, praticamente ogni fornitore DBMS definisce la propria grammatica, ognuno dei quali varia leggermente rispetto allo standard.  
  
 [Appendice C: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), descrive la grammatica SQL minima che tutti i driver ODBC devono supportare. Questa grammatica è un sottoinsieme del livello di ingresso di SQL-92. I driver possono supportare la grammatica aggiuntiva per conformarsi ai livelli di transizione Intermedio, Completo o FIPS 127-2 definito da SQL-92. Per altre informazioni, vedere Grammatica minima SQL nell'Appendice C: Grammatica SQL e SQL-92.For more information, see [SQL Minimum Grammar](../../../odbc/reference/appendixes/sql-minimum-grammar.md) in Appendix C: SQL Grammar, and SQL-92.  
  
 L'Appendice C definisce inoltre sequenze di *escape contenenti* la grammatica standard per le funzionalità del linguaggio comunemente disponibili, ad esempio outer join, che non sono coperte dalla grammatica SQL-92. Per ulteriori informazioni, vedere [Sequenze](../../../odbc/reference/appendixes/odbc-escape-sequences.md) di escape ODBC nell'Appendice C: Grammatica SQL e [Sequenze](../../../odbc/reference/develop-app/escape-sequences.md)di escape , più avanti in questa sezione.  
  
 La grammatica scelta influisce sul modo in cui il driver elabora l'istruzione. I driver devono modificare SQL SQL-92 E le sequenze di escape definite da ODBC in SQL specifico del DBMS. Poiché la maggior parte delle grammatiche SQL sono basate su uno o più dei vari standard, la maggior parte dei driver esegue poco o nessun lavoro per soddisfare questo requisito. Spesso consiste solo nella ricerca delle sequenze di escape definite da ODBC e nella loro sostituzione con la grammatica specifica del DBMS. Quando un driver rileva la grammatica che non riconosce, presuppone che la grammatica sia specifica del DBMS e passa l'istruzione SQL senza apportare modifiche all'origine dati per l'esecuzione.  
  
 Pertanto, esistono due opzioni di grammatica da utilizzare: la grammatica SQL-92 (e le sequenze di escape ODBC) e una grammatica specifica del DBMS. Dei due, solo la grammatica SQL-92 è interoperabile, pertanto tutte le applicazioni interoperabili devono utilizzarla. Le applicazioni che non sono interoperabili possono utilizzare la grammatica SQL-92 o una grammatica specifica di DBMS. Le grammatiche specifiche di DBMS presentano due vantaggi: possono sfruttare tutte le funzionalità non coperte da SQL-92 e sono marginalmente più veloci perché il driver non deve modificarle. Quest'ultima funzionalità può essere parzialmente applicata impostando l'attributo di istruzione SQL_ATTR_NOSCAN, che impedisce al driver di cercare e sostituire le sequenze di escape.  
  
 Se viene utilizzata la grammatica SQL-92, l'applicazione può scoprire come viene modificata dal driver chiamando **SQLNativeSql**. Ciò è spesso utile quando si esegue il debug di applicazioni. **SQLNativeSql** accetta un'istruzione SQL e la restituisce dopo che il driver l'ha modificata. Poiché questa funzione è nel livello di conformità dell'interfaccia Core, è supportata da tutti i driver.
