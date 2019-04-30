---
title: Costruzione di istruzioni SQL interoperative | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], constructing statements
ms.assetid: dee6f7e2-bcc4-4c74-8c7c-12aeda8a90eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc8072a6d7291a546f0f12256aa4b336da037a83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281084"
---
# <a name="constructing-interoperable-sql-statements"></a>Creazione di istruzioni SQL interoperative
Come indicato nelle sezioni precedenti, le applicazioni interoperative devono usare la grammatica SQL ODBC. Oltre usando i tohoto odkazu, tuttavia, un numero di altri problemi riscontrato dalle applicazioni interoperative. Ad esempio, che cosa fa un'applicazione? se desidera utilizzare una funzionalità, ad esempio gli outer join, che non è supportata da tutte le origini dati  
  
 A questo punto, il writer dell'applicazione deve prendere alcune decisioni sulle funzionalità del linguaggio sono necessari e facoltativi. Nella maggior parte dei casi, se un particolare dei driver non supporta una funzionalità richiesta dall'applicazione, l'applicazione Rifiuta semplicemente per l'esecuzione con tale driver. Tuttavia, se la funzionalità è facoltativa, l'applicazione può risolvere la funzionalità. Ad esempio, potrebbe disabilitare le parti dell'interfaccia che consentono all'utente di usare la funzionalità.  
  
 Per determinare quali funzionalità sono supportate, applicazioni vengono avviate chiamando **SQLGetInfo** con l'opzione SQL_SQL_CONFORMANCE. Il livello di conformità SQL fornisce all'applicazione una visione più ampia di cui è supportato SQL. Per perfezionare questa visualizzazione, l'applicazione chiama **SQLGetInfo** con una qualsiasi delle numerose altre opzioni. Per un elenco completo di queste opzioni, vedere la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione. Infine **SQLGetTypeInfo** restituisce informazioni sui tipi di dati supportati dall'origine dati. Le sezioni seguenti riportano un numero di fattori che è opportuno considerare attentamente le applicazioni gli durante la costruzione di istruzioni SQL interoperative.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Utilizzo del catalogo e dello schema](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posizione catalogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificatori delimitati](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Maiuscole/minuscole identificatore](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Sequenza di escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Valore letterale prefissi e suffissi](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcatori di parametro nelle chiamate di procedura](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Istruzioni DDL](../../../odbc/reference/develop-app/ddl-statements.md)
