---
title: 'Origine dati predefinita : Documenti Microsoft'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305992"
---
# <a name="default-data-source"></a>Origine dati predefinita
Il driver può selezionare un'origine dati, denominata origine dati predefinita, in alcuni casi in cui l'applicazione non ne specifica esplicitamente una:  
  
-   In una chiamata a **SQLConnect** in cui il *ServerName* argomento è una stringa di lunghezza zero, un puntatore null o DEFAULT.  
  
-   In una chiamata a **SQLDriverConnect,** dove *InConnectionString* specifica **DSN**: DEFAULT o specifica con la parola chiave **DSN** un'origine dati che non è contenuta nelle informazioni di sistema.  
  
 È definito dal driver come viene specificata l'origine dati predefinita. Ciò può comportare un'azione amministrativa e può dipendere dall'utente.
