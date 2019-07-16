---
title: Del tipo di dati durante il recupero delle informazioni con SQLGetTypeInfo | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020553"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recupero di informazioni sul tipo di dati con SQLGetTypeInfo
Poiché il mapping tra tipi di dati SQL sottostanti e gli identificatori di tipo ODBC sono approssimativi, ODBC offre una funzione (**SQLGetTypeInfo**) tramite cui un driver può completamente descrivere ciascun tipo di dati SQL nell'origine dati. Questa funzione restituisce un set di risultati, ogni riga di cui vengono descritte le caratteristiche di un tipo di dati singolo, ad esempio nome, identificatore del tipo, precisione, scala e supporto di valori null.  
  
 In genere, queste informazioni vengono utilizzate dalle applicazioni generiche che consentono di creare e modificare le tabelle. Tali le applicazioni chiamano **SQLGetTypeInfo** per recuperare le informazioni sul tipo di dati e quindi presentano alcuni o tutti, all'utente. Queste applicazioni devono essere a conoscenza delle seguenti operazioni:  
  
-   Più di un tipo di dati SQL può eseguire il mapping a un identificatore unico tipo, che può renderlo difficile determinare quali dati di tipo da usare. Per risolvere questo problema, il set di risultati è ordinato prima di tutto dall'identificatore di tipo e la seconda da vicinanza alla definizione dell'identificatore del tipo. Inoltre, i tipi di dati definito dall'origine dati hanno la precedenza su tipi di dati definito dall'utente. Ad esempio, si supponga che un'origine dati definisce i tipi di dati INTEGER e il contatore per lo stesso ad eccezione del fatto che, CONTATORI è a incremento automatico. Si supponga inoltre che il tipo definito dall'utente WHOLENUM è un sinonimo dell'intero. Ognuno di questi tipi viene mappato a SQL_INTEGER. Nel **SQLGetTypeInfo** set di risultati, numero intero viene visualizzata per prima, seguita da WHOLENUM e quindi del contatore. WHOLENUM viene visualizzata dopo il numero intero perché è definito dall'utente, ma prima del contatore quanto più da vicino corrisponde la definizione di SQL_INTEGER l'identificatore di tipo.  
  
-   ODBC non definisce nomi di tipi di dati per l'utilizzo in **CREATE TABLE** e **ALTER TABLE** istruzioni. Al contrario, l'applicazione deve utilizzare il nome restituito nella colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**. Il motivo è che sebbene la maggior parte di SQL non presenti variazioni significative in DBMS, nomi dei tipi di dati variare notevolmente. Anziché richiedere driver per analizzare le istruzioni SQL e sostituire i nomi dei tipi di dati standard con nomi di tipi di dati specifici del DBMS, ODBC richiede alle applicazioni di utilizzare i nomi specifici del DBMS in primo luogo.  
  
 Si noti che **SQLGetTypeInfo** non necessariamente descrive tutti i tipi di dati può verificarsi un'applicazione. In particolare, i set di risultati potrebbero contenere tipi di dati non supportati direttamente dall'origine dati. Ad esempio, i tipi di dati delle colonne nel set di risultati restituiti dalle funzioni di catalogo vengono definiti da ODBC e questi tipi di dati potrebbero non essere supportati dall'origine dati. Per determinare le caratteristiche dei tipi di dati in un set di risultati, un'applicazione chiama **SQLColAttribute**.
