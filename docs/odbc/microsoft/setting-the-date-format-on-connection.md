---
description: Impostazione del formato data per la connessione
title: Impostazione del formato della data nella connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date formats [ODBC]
- ODBC driver for Oracle [ODBC], date formats
ms.assetid: ba0d5123-db52-448b-8e19-b7647ce4b361
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3137fa2a8433b7b5174910926fd91e846fd462b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412407"
---
# <a name="setting-the-date-format-on-connection"></a>Impostazione del formato data per la connessione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 La nuova versione di Microsoft ODBC driver for Oracle non imposta automaticamente il formato della data per i campi data Oracle. In precedenza, quando il driver si connette, usava `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'` .  
  
 Per impostare il formato della data, chiamare ALTER SESSION SET, quindi eseguire l'istruzione INSERT. Ad esempio:  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```
