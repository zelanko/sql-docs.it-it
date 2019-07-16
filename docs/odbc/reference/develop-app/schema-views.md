---
title: Viste degli schemi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e2dd512ab529f1fb5d216f4a2e459cd601d40e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943751"
---
# <a name="schema-views"></a>Viste degli schemi
Un'applicazione può recuperare informazioni sui metadati dal sistema DBMS tramite la chiamata di funzioni di catalogo ODBC o le viste INFORMATION_SCHEMA. Le viste sono definite dallo standard ANSI SQL-92.  
  
 Se supportato dal sistema DBMS e il driver, le viste INFORMATION_SCHEMA forniscono un mezzo più potente e completo per il recupero dei metadati di forniscono le funzioni di catalogo ODBC. Un'applicazione possa eseguire personalizzati **seleziona** istruzione su una di queste visualizzazioni possono unire le viste o eseguire un'unione di viste. Offrendo maggiore utilità e una vasta gamma di metadati, le viste INFORMATION_SCHEMA non sono spesso supportate dal sistema DBMS. Ciò potrebbe cambiare come altre dei DBMS e i driver di realizzare la conformità con SQL-92.  
  
 Per determinare quali visualizzazioni sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_INFO_SCHEMA_VIEWS. Per recuperare metadati da una vista supportata, l'applicazione esegue una **seleziona** istruzione che specifica le informazioni dello schema necessarie.
