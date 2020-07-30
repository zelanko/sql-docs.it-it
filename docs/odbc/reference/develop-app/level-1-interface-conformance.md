---
title: Conformità dell'interfaccia di livello 1 | Microsoft Docs
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
ms.openlocfilehash: 29f59cf06eac1ce0f6589ad9c7cba8491e8383b5
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363425"
---
# <a name="level-1-interface-conformance"></a>Conformità di interfaccia di livello 1
Il livello di conformità dell'interfaccia di livello 1 include la funzionalità di base del livello di conformità dell'interfaccia, oltre a funzionalità aggiuntive, ad esempio le transazioni, che sono in genere disponibili in un DBMS relazionale OLTP. Un driver conforme all'interfaccia di livello 1 consente all'applicazione di eseguire le operazioni seguenti, oltre alle funzionalità del livello di conformità dell'interfaccia principale:  
  
|Numero di funzionalità|Descrizione|  
|-|-|  
|101|Specificare lo schema delle tabelle e delle viste di database (usando la denominazione in due parti). (Per altre informazioni, vedere la funzionalità di denominazione in tre parti 201 nella [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).|  
|102|Richiama la vera esecuzione asincrona delle funzioni ODBC, in cui le funzioni ODBC applicabili sono tutte sincrone o tutte asincrone in una determinata connessione.|  
|103|Utilizzare i cursori scorrevoli e quindi ottenere l'accesso a un set di risultati in metodi diversi da quelli di sola trasmissione, chiamando **SQLFetchScroll** con l'argomento *FetchOrientation* diverso da SQL_FETCH_NEXT. Il SQL_FETCH_BOOKMARK *FetchOrientation* è nella funzionalità 204 nella [conformità dell'interfaccia di livello 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).|  
|104|Ottenere le chiavi primarie delle tabelle chiamando **SQLPrimaryKeys**.|  
|105|Utilizzare stored procedure, tramite la sequenza di escape ODBC per le chiamate di procedure, ed eseguire una query sul dizionario dei dati relativo alle stored procedure, chiamando **SQLProcedureColumns** e **SQLProcedures**. Il processo mediante il quale le procedure vengono create e archiviate nell'origine dati esula dall'ambito di questo documento.|  
|106|Connettersi a un'origine dati esplorando in modo interattivo i server disponibili, chiamando **SQLBrowseConnect**.|  
|107|Utilizzare le funzioni ODBC anziché le istruzioni SQL per eseguire determinate operazioni di database: **SQLSetPos** con SQL_POSITION e SQL_REFRESH.|  
|108|Ottenere l'accesso al contenuto di più set di risultati generati da batch e stored procedure chiamando **SQLMoreResults**.|  
|109|Delimitare le transazioni che occupano diverse funzioni ODBC, con una reale atomicità e la possibilità di specificare SQL_ROLLBACK in **SQLEndTran**.|
