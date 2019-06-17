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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 909f9b3e7c8087add8eb66ca2f5c15253026304c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267648"
---
# <a name="default-data-source"></a>Origine dati predefinita
Il driver può selezionare un'origine dati, l'origine dati predefinita, in alcuni casi in cui l'applicazione non specificano esplicitamente una chiamata:  
  
-   In una chiamata a **SQLConnect** in cui le *ServerName* argomento è una stringa di lunghezza zero, un puntatore null o DEFAULT.  
  
-   In una chiamata a **SQLDriverConnect** in cui *InConnectionString* una specifica **DSN**= DEFAULT o specifica con la **DSN** parola chiave un origine dati che non è contenuta nelle informazioni di sistema.  
  
 È definito dal driver come viene specificata l'origine dati predefinita. Questa operazione potrebbe comportare un'azione amministrativa e può dipendere l'utente.
