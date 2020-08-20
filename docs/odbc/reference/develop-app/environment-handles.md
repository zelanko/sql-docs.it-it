---
description: Handle di ambiente
title: Handle di ambiente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment handles [ODBC]
- handles [ODBC], environment
ms.assetid: 917f1b0c-272b-4e37-a1f5-87cd24b9fa21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1aa22a89288f4dd5a8400484078f57b60fc135fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461503"
---
# <a name="environment-handles"></a>Handle di ambiente
Un *ambiente* è un contesto globale in cui accedere ai dati; associato a un ambiente è qualsiasi informazione globale di natura, ad esempio:  
  
-   Stato dell'ambiente  
  
-   Diagnostica a livello di ambiente corrente  
  
-   Handle delle connessioni attualmente allocate nell'ambiente  
  
-   Impostazioni correnti di ogni attributo dell'ambiente  
  
 All'interno di un frammento di codice che implementa ODBC (Gestione driver o driver), un handle di ambiente identifica una struttura per contenere tali informazioni.  
  
 Gli handle di ambiente non vengono spesso utilizzati nelle applicazioni ODBC. Vengono sempre utilizzate nelle chiamate a **SQLDataSources** e **SQLDrivers** e talvolta utilizzate nelle chiamate a **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**e **SQLGetDiagRec**.  
  
 Ogni parte di codice che implementa ODBC (Gestione driver o driver) contiene uno o più handle di ambiente. Gestione driver, ad esempio, gestisce un handle di ambiente separato per ogni applicazione connessa. Gli handle di ambiente vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
