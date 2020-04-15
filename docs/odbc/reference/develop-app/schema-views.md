---
title: Visualizzazioni dello schema Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1a9e421c4835d35e3c4f3c644e69b8c7601e8e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304252"
---
# <a name="schema-views"></a>Viste degli schemi
Un'applicazione può recuperare le informazioni sui metadati dal DBMS chiamando le funzioni di catalogo ODBC o utilizzando INFORMATION_SCHEMA visualizzazioni. Le viste sono definite dallo standard ANSI SQL-92.  
  
 Se supportato dal DBMS e il driver, le visualizzazioni INFORMATION_SCHEMA forniscono un mezzo più potente e completo per recuperare i metadati rispetto alle funzioni di catalogo ODBC. Un'applicazione può eseguire la propria istruzione **SELECT** personalizzata su una di queste visualizzazioni, può unire le visualizzazioni o eseguire un'unione sulle visualizzazioni. Pur offrendo una maggiore utilità e una più ampia gamma di metadati, le visualizzazioni INFORMATION_SCHEMA non sono spesso supportate dal DBMS. Questo potrebbe cambiare man mano che un numero maggiore di DBS e driver raggiunge la conformità con SQL-92.  
  
 Per determinare quali visualizzazioni sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_INFO_SCHEMA_VIEWS. Per recuperare i metadati da una visualizzazione supportata, l'applicazione esegue un'istruzione **SELECT** che specifica le informazioni sullo schema necessarie.
