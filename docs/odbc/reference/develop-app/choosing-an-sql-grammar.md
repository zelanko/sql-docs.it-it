---
title: Scelta di una grammatica SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 670ed0adbbd5ad993af0942d492ee19f75fa9628
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026580"
---
# <a name="choosing-an-sql-grammar"></a>Scelta di una grammatica SQL
La prima decisione da prendere durante la costruzione di istruzioni SQL è che sintassi da utilizzare. Oltre alle grammatiche disponibile dai corpi dei vari standard, come Open Group, ANSI e ISO, praticamente ogni fornitore DBMS definisce il proprio grammatica, ognuno dei quali varia leggermente dallo standard.  
  
 [Appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), viene descritta la grammatica SQL minima che devono supportare tutti i driver ODBC. L'espressione è un subset del livello minimo di SQL-92. I driver possono supportare ulteriore grammatica in modo da essere conformi alla FIPS 127-2 transitori livelli definiti da SQL-92, Full o intermedio. Per altre informazioni, vedere [grammatica SQL minima](../../../odbc/reference/appendixes/sql-minimum-grammar.md) nell'appendice c: Grammatica SQL e SQL-92.  
  
 Appendice C definisce inoltre *sequenze di escape* contenente grammatica standard per funzionalità del linguaggio comunemente disponibili, ad esempio gli outer join, che non sono coperti dalla grammatica SQL-92. Per altre informazioni, vedere [sequenze di Escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) nell'appendice c: Grammatica SQL, e [sequenze di Escape](../../../odbc/reference/develop-app/escape-sequences.md), più avanti in questa sezione.  
  
 La grammatica scelto influisce sul modo in cui il driver elabora l'istruzione. I driver necessario modificare le sequenze di escape definite da ODBC a specifici del DBMS SQL e SQL-92 SQL. Poiché la maggior parte delle grammatiche SQL si basano su uno o più dei vari standard, i driver la maggior parte delle operazioni vengono eseguite senza alcuna per soddisfare questo requisito. Spesso costituita solo da una ricerca per le sequenze di escape definite da ODBC e sostituirli con grammatica specifici del DBMS. Quando un driver rileva grammatica che non riconosce, si presuppone la grammatica è specifico del sistema DBMS e passa l'istruzione SQL senza alcuna modifica all'origine dati per l'esecuzione.  
  
 Pertanto, sono disponibili due opzioni di grammatica da utilizzare: la grammatica SQL-92 (e le sequenze di escape ODBC) e una grammatica di specifici del DBMS. Dei due, solo la grammatica SQL-92 è interoperativa, in modo che tutte le applicazioni interoperative devono usarlo. Applicazioni che non sono interoperative possono usare la grammatica SQL-92 o una grammatica di specifici del DBMS. Grammatiche specifici del DBMS sono due vantaggi: È possibile sfruttare le funzionalità non coperti da SQL-92 e sono leggermente più veloce perché il driver non è necessario modificarle. La funzionalità di quest'ultima può essere applicata parzialmente impostando l'attributo di istruzione SQL_ATTR_NOSCAN, interrompendo il driver dalla ricerca e sostituzione di sequenze di escape.  
  
 Se viene utilizzata la grammatica SQL-92, l'applicazione può individuare come viene modificato dal driver chiamando **SQLNativeSql**. Ciò è spesso utile durante il debug di applicazioni. **SQLNativeSql** accetta un'istruzione SQL e lo restituisce dopo che il driver è stato modificato. Poiché questa funzione si trova al livello di conformità di interfaccia Core, è supportata da tutti i driver.
