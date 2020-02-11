---
title: Posizione Catalogo | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062685"
---
# <a name="catalog-position"></a>Posizione del catalogo
La posizione di un nome di catalogo in un identificatore e il modo in cui è separata dal resto dell'identificatore variano a seconda dell'origine dati. Ad esempio, in un'origine dati Xbase il nome del catalogo è una directory e, in Microsoft® Windows®, è separato dal nome della tabella, ovvero un nome di file, da una barra rovesciata (\\). Nella figura seguente viene illustrata questa condizione.  
  
 ![Posizione catalogo: Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 In un'origine dati SQL Server, il catalogo è un database ed è separato dai nomi dello schema e della tabella in base a un punto (.).  
  
 ![Posizione catalogo: SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 In un'origine dati Oracle, il catalogo è anche il database, ma segue il nome della tabella ed è separato dai nomi dello schema e della tabella da un simbolo di chiocciola (@).  
  
 ![Posizione catalogo: Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 Per determinare il separatore di catalogo e il percorso del nome del catalogo, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_NAME_SEPARATOR e SQL_CATALOG_LOCATION. Le applicazioni interoperative devono costruire gli identificatori in base a questi valori.  
  
 Quando si citano identificatori che contengono più di una parte, le applicazioni devono prestare attenzione a racchiudere separatamente ogni parte e non racchiudere il carattere che separa gli identificatori. Ad esempio, l'istruzione seguente per selezionare tutte le righe e le colonne di una tabella Xbase cita i nomi di catalogo (\XBASE\SALES\CORP) e Table (Parts. dbf), ma non il separatore di catalogo (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 L'istruzione seguente per selezionare tutte le righe e le colonne di una tabella Oracle include i nomi Catalog (Sales), schema (Corporate) e Table (Parts), ma non i separatori del catalogo (@) o dello schema (.):  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 Per informazioni sugli identificatori di virgolette, vedere la sezione successiva, [identificatori delimitati](../../../odbc/reference/develop-app/quoted-identifiers.md).
