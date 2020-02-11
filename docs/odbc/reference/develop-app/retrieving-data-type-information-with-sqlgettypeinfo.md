---
title: Recupero delle informazioni sul tipo di dati con SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4f336a7ebfaf5e76ac464944900231c452809f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020553"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recupero di informazioni sul tipo di dati con SQLGetTypeInfo
Poiché i mapping dei tipi di dati SQL sottostanti agli identificatori di tipo ODBC sono approssimativi, ODBC fornisce una funzione (**SQLGetTypeInfo**) tramite la quale un driver può descrivere completamente ogni tipo di dati SQL nell'origine dati. Questa funzione restituisce un set di risultati, ogni riga che descrive le caratteristiche di un singolo tipo di dati, ad esempio il nome, l'identificatore del tipo, la precisione, la scala e il supporto di valori null.  
  
 Queste informazioni vengono in genere utilizzate da applicazioni generiche che consentono all'utente di creare e modificare le tabelle. Tali applicazioni chiamano **SQLGetTypeInfo** per recuperare le informazioni sul tipo di dati e quindi presentare alcune o tutte le informazioni all'utente. Tali applicazioni devono essere a conoscenza di due elementi:  
  
-   È possibile eseguire il mapping di più di un tipo di dati SQL a un singolo identificatore di tipo, che può rendere difficile determinare il tipo di dati da utilizzare. Per risolvere questo problema, il set di risultati viene ordinato per primo in base all'identificatore del tipo e secondo per chiusura alla definizione dell'identificatore di tipo. Inoltre, i tipi di dati definiti dall'origine dati hanno la precedenza sui tipi di dati definiti dall'utente. Si supponga, ad esempio, che un'origine dati definisca i tipi di dati INTEGER e COUNTER in modo che siano uguali, ad eccezione del fatto che il contatore viene incrementato automaticamente. Si supponga inoltre che il tipo definito dall'utente WHOLENUM sia un sinonimo di INTEGER. Ognuno di questi tipi viene mappato a SQL_INTEGER. Nel set di risultati **SQLGetTypeInfo** , Integer viene visualizzato per primo, seguito da WHOLENUM e quindi da Counter. WHOLENUM viene visualizzato dopo INTEGER perché è definito dall'utente, ma prima del contatore perché corrisponde maggiormente alla definizione dell'identificatore del tipo di SQL_INTEGER.  
  
-   ODBC non definisce i nomi dei tipi di dati da utilizzare nelle istruzioni **Create Table** e **ALTER TABLE** . Al contrario, l'applicazione deve utilizzare il nome restituito nella colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**. Il motivo è che anche se la maggior parte di SQL non varia molto tra DBMS, i nomi dei tipi di dati variano notevolmente. Anziché forzare i driver a analizzare le istruzioni SQL e a sostituire i nomi dei tipi di dati standard con i nomi dei tipi di dati specifici di DBMS, per ODBC è necessario che le applicazioni utilizzino i nomi specifici del sistema DBMS.  
  
 Si noti che **SQLGetTypeInfo** non descrive necessariamente tutti i tipi di dati che possono verificarsi in un'applicazione. In particolare, i set di risultati potrebbero contenere tipi di dati non supportati direttamente dall'origine dati. Ad esempio, i tipi di dati delle colonne nei set di risultati restituiti dalle funzioni di catalogo sono definiti da ODBC e tali tipi di dati potrebbero non essere supportati dall'origine dati. Per determinare le caratteristiche dei tipi di dati in un set di risultati, un'applicazione chiama **SQLColAttribute**.
