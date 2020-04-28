---
title: Origine dati predefinita | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305992"
---
# <a name="default-data-source"></a>Origine dati predefinita
Il driver può selezionare un'origine dati, denominata origine dati predefinita, in determinati casi in cui l'applicazione non ne specifichi esplicitamente uno:  
  
-   In una chiamata a **SQLConnect** dove l'argomento *ServerName* è una stringa di lunghezza zero, un puntatore null o un valore predefinito.  
  
-   In una chiamata a **SQLDriverConnect** in cui *InConnectionString* specifica **DSN**= default o specifica con la parola chiave **DSN** un'origine dati che non è contenuta nelle informazioni di sistema.  
  
 Viene definito dal driver come viene specificata l'origine dati predefinita. Questo può comportare un'azione amministrativa che può dipendere dall'utente.
