---
title: Posizione del catalogo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0305d978dc4ecd21892a0be3916fa5072b7be95a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303382"
---
# <a name="catalog-position"></a>Posizione del catalogo
La posizione di un nome di catalogo in un identificatore e il modo in cui viene separato dal resto dell'identificatore varia da origine dati a origine dati. In un'origine dati Xbase, ad esempio, il nome del catalogo è una directory e, in Microsoft® Windows®,\\è separato dal nome della tabella (che è un nome di file) da una barra rovesciata ( ). Nella figura seguente viene illustrata questa condizione.  
  
 ![Posizione catalogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 In un'origine dati SQL ServerSQL Server , il catalogo è un database ed è separato dai nomi di tabella e schema da un punto (.).  
  
 ![Posizione catalogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 In un'origine dati Oracle, il catalogo è anche il database, ma segue il nome della tabella ed è separato dai nomi dello schema e della tabella da un simbolo di chiocciola (-).  
  
 ![Posizione catalogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Per determinare il separatore del catalogo e il percorso del nome del catalogo, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_NAME_SEPARATOR e SQL_CATALOG_LOCATION. Le applicazioni interoperabili devono costruire identificatori in base a questi valori.  
  
 Quando si citano identificatori che contengono più di una parte, le applicazioni devono fare attenzione a citare ogni parte separatamente e non citare il carattere che separa gli identificatori. Ad esempio, l'istruzione seguente per selezionare tutte le righe e le colonne di una tabella Xbase cita i nomi del catalogo ,\\XBASE SALES , CORP , ma non il separatore di catalogo ( ):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 L'istruzione seguente per selezionare tutte le righe e le colonne di una tabella Oracle indica i nomi del catalogo (Sales), dello schema (Corporate) e della tabella (Parti), ma non i separatori di catalogo o di schema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Per informazioni sugli identificatori di citazione, vedere la sezione [successiva, Identificatori tra virgolette](../../../odbc/reference/develop-app/quoted-identifiers.md).
