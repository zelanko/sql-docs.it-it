---
description: Viste degli schemi
title: Viste dello schema | Microsoft Docs
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
ms.openlocfilehash: 34e1b52b5e96b5fedb964e53f14a7b554d12aa05
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429073"
---
# <a name="schema-views"></a>Viste degli schemi
Un'applicazione può recuperare informazioni sui metadati dal sistema DBMS chiamando le funzioni del catalogo ODBC o utilizzando INFORMATION_SCHEMA viste. Le visualizzazioni sono definite dallo standard ANSI SQL-92.  
  
 Se supportato dal sistema DBMS e dal driver, le visualizzazioni INFORMATION_SCHEMA forniscono un mezzo più potente e completo per il recupero dei metadati rispetto alle funzioni del catalogo ODBC. Un'applicazione può eseguire una propria istruzione **Select** personalizzata su una di queste visualizzazioni, può unire viste oppure può eseguire un'Unione sulle viste. Pur offrendo più utilità e una gamma più ampia di metadati, le visualizzazioni INFORMATION_SCHEMA non sono spesso supportate dal sistema DBMS. Questo può cambiare poiché più DBMS e driver raggiungono la conformità con SQL-92.  
  
 Per determinare quali visualizzazioni sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_INFO_SCHEMA_VIEWS. Per recuperare i metadati da una visualizzazione supportata, l'applicazione esegue un'istruzione **Select** che specifica le informazioni sullo schema necessarie.
