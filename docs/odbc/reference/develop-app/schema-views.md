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
manager: craigg
ms.openlocfilehash: 782dec08b76a9e5a97719d6af39e2c30c0f92d19
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468618"
---
# <a name="schema-views"></a>Viste degli schemi
Un'applicazione può recuperare informazioni sui metadati dal sistema DBMS tramite la chiamata di funzioni di catalogo ODBC o le viste INFORMATION_SCHEMA. Le viste sono definite dallo standard ANSI SQL-92.  
  
 Se supportato dal sistema DBMS e il driver, le viste INFORMATION_SCHEMA forniscono un mezzo più potente e completo per il recupero dei metadati di forniscono le funzioni di catalogo ODBC. Un'applicazione possa eseguire personalizzati **seleziona** istruzione su una di queste visualizzazioni possono unire le viste o eseguire un'unione di viste. Offrendo maggiore utilità e una vasta gamma di metadati, le viste INFORMATION_SCHEMA non sono spesso supportate dal sistema DBMS. Ciò potrebbe cambiare come altre dei DBMS e i driver di realizzare la conformità con SQL-92.  
  
 Per determinare quali visualizzazioni sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_INFO_SCHEMA_VIEWS. Per recuperare metadati da una vista supportata, l'applicazione esegue una **seleziona** istruzione che specifica le informazioni dello schema necessarie.
