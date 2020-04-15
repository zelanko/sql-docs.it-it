---
title: Recupero delle informazioni sul tipo di dati con SQLGetTypeInfo . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec2bbba824eaf3d74133cf9754eca2593c9fb79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300061"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recupero di informazioni sul tipo di dati con SQLGetTypeInfo
Poiché i mapping dai tipi di dati SQL sottostanti agli identificatori di tipo ODBC sono approssimativi, ODBC fornisce una funzione (**SQLGetTypeInfo**) tramite la quale un driver può descrivere completamente ogni tipo di dati SQL nell'origine dati. Questa funzione restituisce un set di risultati, ogni riga che descrive le caratteristiche di un singolo tipo di dati, ad esempio nome, identificatore di tipo, precisione, scala e supporto di valori Null.This function returns a result set, each row of which describes the characteristics of a single data type, such as name, type identifier, precision, scale, and nullability.  
  
 Queste informazioni vengono in genere utilizzate da applicazioni generiche che consentono all'utente di creare e modificare tabelle. Tali applicazioni chiamano **SQLGetTypeInfo** per recuperare le informazioni sul tipo di dati e quindi presentarne alcune o tutte all'utente. Tali applicazioni devono essere consapevoli di due cose:  
  
-   È possibile eseguire il mapping di più tipi di dati SQL a un singolo identificatore di tipo, il che può rendere difficile determinare il tipo di dati da utilizzare. Per risolvere questo problema, il set di risultati viene ordinato prima in base all'identificatore di tipo e in secondo luogo in base alla vicinanza alla definizione dell'identificatore di tipo. Inoltre, i tipi di dati definiti dall'origine dati hanno la precedenza sui tipi di dati definiti dall'utente. Si supponga, ad esempio, che un'origine dati definisca i tipi di dati INTEGER e COUNTER in modo che siano uguali, ad eccezione del fatto che COUNTER viene incrementato automaticamente. Si supponga inoltre che il tipo definito dall'utente WHOLENUM sia un sinonimo di INTEGER. Ognuno di questi tipi esegue il mapping a SQL_INTEGER. Nel set di risultati **SQLGetTypeInfo,** INTEGER viene visualizzato per primo, seguito da WHOLENUM e quindi COUNTER. WHOLENUM viene visualizzato dopo INTEGER perché è definito dall'utente, ma prima di COUNTER perché corrisponde più strettamente alla definizione dell'identificatore di tipo SQL_INTEGER.  
  
-   ODBC non definisce i nomi dei tipi di dati da utilizzare nelle istruzioni **CREATE TABLE** e **ALTER TABLE.** Al contrario, l'applicazione deve utilizzare il nome restituito nella colonna TYPE_NAME del set di risultati restituito da **SQLGetTypeInfo**. La ragione di questo è che anche se la maggior parte di SQL non varia molto tra DBS, i nomi dei tipi di dati variano enormemente. Anziché forzare i driver per analizzare le istruzioni SQL e sostituire i nomi dei tipi di dati standard con nomi di tipi di dati specifici di DBMS, ODBC richiede alle applicazioni di utilizzare i nomi specifici di DBMS in primo luogo.  
  
 Si noti che **SQLGetTypeInfo** non descrive necessariamente tutti i tipi di dati che un'applicazione può incontrare. In particolare, i set di risultati potrebbero contenere tipi di dati non supportati direttamente dall'origine dati. Ad esempio, i tipi di dati delle colonne nei set di risultati restituiti dalle funzioni di catalogo sono definiti da ODBC e questi tipi di dati potrebbero non essere supportati dall'origine dati. Per determinare le caratteristiche dei tipi di dati in un set di risultati, un'applicazione chiama **SQLColAttribute**.
