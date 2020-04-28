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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ca9911d3c88f2f540ff1332d77a2e1ebc6a4942
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299161"
---
# <a name="choosing-an-sql-grammar"></a>Scelta di una grammatica SQL
La prima decisione da prendere quando si costruiscono istruzioni SQL è la grammatica da usare. Oltre alle grammatiche disponibili nei vari corpi degli standard, ad esempio Open Group, ANSI e ISO, virtualmente ogni fornitore del sistema DBMS definisce la propria grammatica, ognuno dei quali è leggermente diverso da quello standard.  
  
 [Appendice C: grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md), che descrive la grammatica SQL minima che tutti i driver ODBC devono supportare. Questa grammatica è un subset del livello di ingresso di SQL-92. I driver possono supportare una grammatica aggiuntiva per conformarsi ai livelli di transizione intermedio, completo o FIPS 127-2 definiti da SQL-92. Per ulteriori informazioni, vedere la pagina relativa alla [grammatica minima SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) nell'Appendice C: grammatica SQL e sql-92.  
  
 L'Appendice C definisce anche le *sequenze di escape* che contengono la grammatica standard per le funzionalità del linguaggio comunemente disponibili, ad esempio outer join, che non sono coperte dalla grammatica SQL-92. Per ulteriori informazioni, vedere [sequenze di escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) nell'Appendice C: grammatica SQL e [sequenze di escape](../../../odbc/reference/develop-app/escape-sequences.md), più avanti in questa sezione.  
  
 La grammatica scelta influiscono sulla modalità di elaborazione dell'istruzione da parte del driver. I driver devono modificare SQL-92 SQL e le sequenze di escape definite da ODBC in SQL specifico di DBMS. Poiché la maggior parte delle grammatiche SQL si basa su uno o più standard diversi, la maggior parte dei driver non è sufficiente per soddisfare questo requisito. Spesso è costituito solo dalla ricerca di sequenze di escape definite da ODBC e dalla relativa sostituzione con la grammatica specifica di DBMS. Quando un driver rileva la grammatica, non riconosce, presuppone che la grammatica sia specifica per DBMS e passa l'istruzione SQL senza apportare modifiche all'origine dati per l'esecuzione.  
  
 Sono pertanto disponibili due opzioni di grammatica da utilizzare: la grammatica SQL-92 (e le sequenze di escape ODBC) e una grammatica specifica del sistema DBMS. Tra le due, solo la grammatica SQL-92 è interoperativa, pertanto tutte le applicazioni interoperative devono utilizzarlo. Le applicazioni non interoperative possono utilizzare la grammatica SQL-92 o una grammatica specifica del sistema DBMS. Le grammatiche specifiche di DBMS hanno due vantaggi: possono sfruttare le funzionalità non incluse in SQL-92 e sono leggermente più veloci perché il driver non è necessario modificarle. La seconda funzionalità può essere applicata parzialmente impostando l'attributo dell'istruzione SQL_ATTR_NOSCAN, che interrompe la ricerca e la sostituzione delle sequenze di escape da parte del driver.  
  
 Se viene utilizzata la grammatica SQL-92, l'applicazione può individuare il modo in cui viene modificata dal driver chiamando **SQLNativeSql**. Questa operazione è spesso utile quando si esegue il debug delle applicazioni. **SQLNativeSql** accetta un'istruzione SQL e la restituisce dopo che è stata modificata dal driver. Poiché questa funzione è nel livello di conformità dell'interfaccia principale, è supportata da tutti i driver.
