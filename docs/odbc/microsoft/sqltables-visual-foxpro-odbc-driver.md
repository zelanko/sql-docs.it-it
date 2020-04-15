---
title: SQLTables (Driver ODBC di Visual FoxPro) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5467fc8c1717d5ceb548b3950a0894fd2a1b4499
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299284"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello 1ODBC API Conformance: Level 1  
  
 Restituisce l'elenco dei nomi di tabella specificati dal parametro nell'istruzione **SQLTables.** Se non viene specificato alcun parametro, restituisce i nomi delle tabelle archiviati nell'origine dati corrente. Il driver restituisce le informazioni come set di risultati.  
  
 Le chiamate al tipo di enumerazione non riceveranno una voce del set di risultati per le visualizzazioni remote o le visualizzazioni con parametri locali. Tuttavia, una chiamata a **SQLTables** con un identificatore nome di tabella univoco troverà una corrispondenza per tale visualizzazione se presente con tale nome; in questo modo l'API può essere utilizzata per verificare la presenza di conflitti di nomi prima della creazione di una nuova tabella.  
  
> [!NOTE]  
>  Il driver ODBC di Visual FoxPro distingue tra tabelle di [database](../../odbc/microsoft/visual-foxpro-terminology.md) e [tabelle libere](../../odbc/microsoft/visual-foxpro-terminology.md), anche quando entrambi i tipi di tabelle sono archiviati nella stessa directory nel sistema. Se l'origine dati è una directory di tabelle libere, il driver ODBC di Visual FoxPro non cataloga né restituisce i nomi delle tabelle associate a un database.  
  
 Per ulteriori informazioni, vedere [SQLTables](../../odbc/reference/syntax/sqltables-function.md) in *ODBC Programmer's Reference*.
