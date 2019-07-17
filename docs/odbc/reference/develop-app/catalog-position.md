---
title: Posizione catalogo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3d7c320521a9948c7968f4f7f5d42fd715f6c03d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062685"
---
# <a name="catalog-position"></a>Posizione del catalogo
La posizione di un nome di catalogo in un identificatore e modo in cui è separato dal resto dell'identificatore varia da origine dati all'origine dati. Ad esempio, in un'origine dati Xbase, il nome del catalogo è una directory e, in Microsoft® Windows®, sono separato dal nome della tabella (che è un nome di file) da una barra rovesciata (\\). La figura seguente illustra questa condizione.  
  
 ![Posizione catalogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 In un'origine dati di SQL Server, il catalogo è un database ed è separato dai nomi di tabella e dello schema da un punto (.).  
  
 ![Posizione catalogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 In un'origine dati Oracle, il catalogo è anche il database, ma segue il nome della tabella ed è separato dai nomi di tabella e dello schema da un simbolo di chiocciola (@).  
  
 ![Posizione catalogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Per determinare il separatore di catalogo e il percorso del nome di catalogo, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_NAME_SEPARATOR e SQL_CATALOG_LOCATION. Applicazioni interoperative necessario costruire identificatori in base a questi valori.  
  
 Quando deve essere racchiuso tra gli identificatori che contengono più di una parte, le applicazioni devono essere fare attenzione a offerta di ciascuna parte separatamente e non utilizzare le virgolette con il carattere che separa gli identificatori. Ad esempio, l'istruzione seguente per selezionare tutte le righe e colonne di una tabella di Xbase offerte del catalogo (\XBASE\SALES\CORP) e i nomi delle tabelle (Parts.dbf), ma non il separatore di catalogo (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 L'istruzione seguente per selezionare tutte le righe e colonne di una tabella Oracle delle offerte del catalogo (vendite), dello schema (aziendale) e i nomi delle tabelle (parti), ma non il catalogo (@) o i separatori di schema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Per informazioni su deve essere racchiuso tra gli identificatori, vedere la sezione successiva [identificatori racchiusi tra virgolette](../../../odbc/reference/develop-app/quoted-identifiers.md).
