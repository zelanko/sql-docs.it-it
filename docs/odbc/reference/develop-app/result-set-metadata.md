---
title: Determinare i metadati del Set | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7dc88892fab2fd18dbcbec5ce54fa09c9c9b89e7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199384"
---
# <a name="result-set-metadata"></a>Metadati del set di risultati
*Metadati* sono dati che descrivono altri dati. Ad esempio, i metadati dei set di risultati descrive il set di risultati, ad esempio il numero di colonne nel set di risultati, i tipi di dati di tali colonne, i nomi, precisione, ammissione di valori null e così via.  
  
 Applicazioni interoperative consigliabile controllare sempre i metadati delle colonne del set di risultati. I metadati per una colonna in un set di risultati potrebbero essere diversi dai metadati per la colonna come restituiti da una funzione di catalogo. Ad esempio, si supponga che una colonna aggiornabile è incluso nel set di risultati creati unendo in join due tabelle. Sebbene **SQLColumnPrivileges** potrebbe indicare che un utente può aggiornare la colonna, i metadati di set di risultati potrebbero non se la colonna è sul lato "molti" del join; molte origini dati possono aggiornare le colonne sul lato "uno" di un join, ma non sulla " lato "molti". " Non è possibile presupporre anche i tipi di dati sia lo stesso, poiché l'origine dati può promuovere il tipo di dati durante la creazione di set di risultati.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Come vengono usati i metadati?](../../../odbc/reference/develop-app/how-is-metadata-used.md)  
  
-   [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)
