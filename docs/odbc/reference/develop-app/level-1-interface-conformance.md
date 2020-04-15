---
title: Conformità dell'interfaccia di livello 1 Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d31d5fe8aea1df4e7937104580efb820ba6f031
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306182"
---
# <a name="level-1-interface-conformance"></a>Conformità di interfaccia di livello 1
Il livello di conformità dell'interfaccia di livello 1 include la funzionalità del livello di conformità dell'interfaccia di base e funzionalità aggiuntive, ad esempio le transazioni, che in genere sono disponibili in un DBMS relazionale OLTP. Un driver conforme all'interfaccia di livello 1 consente all'applicazione di eseguire le operazioni seguenti, oltre alle funzionalità del livello di conformità dell'interfaccia di base:A Level 1 interface-conformant driver lets the application do the following, in addition to the features in the Core interface conformance level:  
  
|||  
|-|-|  
|101|Specificare lo schema delle tabelle e delle viste di database (utilizzando la denominazione in due parti). Per ulteriori informazioni, vedere la funzionalità di denominazione in tre parti 201 nella [conformità dell'interfaccia](../../../odbc/reference/develop-app/level-2-interface-conformance.md)di livello 2.|  
|102|Richiamare l'esecuzione asincrona vera delle funzioni ODBC, in cui le funzioni ODBC applicabili sono tutte sincrone o tutte asincrone in una determinata connessione.|  
|103|Utilizzare cursori scorrevoli e quindi ottenere l'accesso a un set di risultati in metodi diversi da forward-only, chiamando **SQLFetchScroll** con il *FetchOrientation* argomento diverso da SQL_FETCH_NEXT. (La SQL_FETCH_BOOKMARK *FetchOrientation* è nella funzionalità 204 in [Conformità dell'interfaccia](../../../odbc/reference/develop-app/level-2-interface-conformance.md)di livello 2 .|  
|104|Ottenere le chiavi primarie delle tabelle chiamando **SQLPrimaryKeys**.|  
|105|Utilizzare stored procedure tramite la sequenza di escape ODBC per le chiamate di routine ed eseguire una query nel dizionario dei dati relativo alle stored procedure, chiamando **SQLProcedureColumns** e **SQLProcedures**. Il processo mediante il quale le procedure vengono create e archiviate nell'origine dati non rientra nell'ambito di questo documento.|  
|106|Connettersi a un'origine dati esplorando in modo interattivo i server disponibili, chiamando **SQLBrowseConnect**.|  
|107|Utilizzare le funzioni ODBC anziché le istruzioni SQL per eseguire determinate operazioni di database: **SQLSetPos** con SQL_POSITION e SQL_REFRESH.|  
|108|Ottenere l'accesso al contenuto di più set di risultati generati da batch e stored procedure, chiamando **SQLMoreResults**.|  
|109|Delimitare le transazioni che si estendono su diverse funzioni ODBC, con true atomicity e la possibilità di specificare SQL_ROLLBACK in **SQLEndTran**.|
