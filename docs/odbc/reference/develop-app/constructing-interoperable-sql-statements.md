---
title: Costruzione di istruzioni SQL interoperabili Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1eccdef63b7d06a456a07f5f1a9ccad987d2de29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282517"
---
# <a name="constructing-interoperable-sql-statements"></a>Creazione di istruzioni SQL interoperative
Come accennato nelle sezioni precedenti, le applicazioni interoperabili devono utilizzare la grammatica SQL ODBC. Oltre all'utilizzo di questa grammatica, tuttavia, una serie di problemi aggiuntivi sono affrontati da applicazioni interoperabili. Ad esempio, cosa fa un'applicazione se si desidera utilizzare una funzionalità, ad esempio outer join, che non è supportata da tutte le origini dati?  
  
 A questo punto, il writer dell'applicazione deve prendere alcune decisioni sulle funzionalità del linguaggio richieste e facoltative. Nella maggior parte dei casi, se un particolare driver non supporta una funzionalità richiesta dall'applicazione, l'applicazione si rifiuta semplicemente di eseguire con tale driver. Tuttavia, se la funzionalità è facoltativa, l'applicazione può aggirare la funzionalità. Ad esempio, potrebbe disabilitare quelle parti dell'interfaccia che consentono all'utente di utilizzare la funzionalità.  
  
 Per determinare le funzionalità supportate, le applicazioni vengono avviate chiamando **SQLGetInfo** con l'opzione SQL_SQL_CONFORMANCE. Il livello di conformità SQL offre all'applicazione un'ampia visualizzazione del supporto di SQL. Per perfezionare questa visualizzazione, l'applicazione chiama **SQLGetInfo** con una serie di altre opzioni. Per un elenco completo di queste opzioni, vedere il [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione. Infine, **SQLGetTypeInfo** restituisce informazioni sui tipi di dati supportati dall'origine dati. Nelle sezioni seguenti sono elencati alcuni possibili fattori che le applicazioni devono controllare durante la costruzione di istruzioni SQL interoperabili.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Utilizzo del catalogo e dello schema](../../../odbc/reference/develop-app/catalog-and-schema-usage.md)  
  
-   [Posizione del catalogo](../../../odbc/reference/develop-app/catalog-position.md)  
  
-   [Identificatori delimitati](../../../odbc/reference/develop-app/quoted-identifiers.md)  
  
-   [Maiuscole/minuscole per gli identificatori](../../../odbc/reference/develop-app/identifier-case.md)  
  
-   [Sequenza di escape](../../../odbc/reference/develop-app/escape-sequences.md)  
  
-   [Prefissi e suffissi per valori letterali](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)  
  
-   [Marcatori di parametro nelle chiamate di procedura](../../../odbc/reference/develop-app/parameter-markers-in-procedure-calls.md)  
  
-   [Istruzioni DDL](../../../odbc/reference/develop-app/ddl-statements.md)
