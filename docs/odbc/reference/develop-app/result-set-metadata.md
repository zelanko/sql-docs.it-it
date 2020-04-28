---
title: Metadati del set di risultati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 6d134515-e34d-4563-96d7-8ad7714818fd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b78cdeb4c8b3522f4677c0277401cd9395a36a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300081"
---
# <a name="result-set-metadata"></a>Metadati del set di risultati
I *metadati* sono dati che descrivono altri dati. I metadati del set di risultati, ad esempio, descrivono il set di risultati, ad esempio il numero di colonne nel set di risultati, i tipi di dati di tali colonne, i relativi nomi, la precisione, il supporto di valori null e così via.  
  
 Le applicazioni interoperative devono sempre controllare i metadati delle colonne del set di risultati. I metadati per una colonna in un set di risultati potrebbero essere diversi da quelli della colonna restituiti da una funzione di catalogo. Si supponga, ad esempio, che una colonna aggiornabile venga inclusa in un set di risultati creato mediante l'Unione di due tabelle. Mentre **SQLColumnPrivileges** potrebbe indicare che un utente può aggiornare la colonna, i metadati del set di risultati potrebbero non essere se la colonna si trova sul lato "molti" del join. molte origini dati possono aggiornare le colonne sul lato "uno" di un join, ma non sul lato "molti". Anche i tipi di dati non possono essere considerati uguali, perché l'origine dati potrebbe innalzare di livello il tipo di dati durante la creazione del set di risultati.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Modalità di utilizzo dei metadati](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
