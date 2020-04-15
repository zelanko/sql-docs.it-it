---
title: Maniglie dell'ambiente Documenti Microsoft
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
ms.openlocfilehash: b504995e99dfad032598485e370b4d5a6681ae81
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300441"
---
# <a name="environment-handles"></a>Handle di ambiente
Un *ambiente* è un contesto globale in cui accedere ai dati; associato a un ambiente è qualsiasi informazione di natura globale, ad esempio:  
  
-   Lo stato dell'ambiente  
  
-   La diagnostica a livello di ambiente corrente  
  
-   Gli handle delle connessioni attualmente allocate nell'ambiente  
  
-   Le impostazioni correnti di ogni attributo di ambiente  
  
 All'interno di una parte di codice che implementa ODBC (Gestione Driver o un driver), un handle di ambiente identifica una struttura per contenere queste informazioni.  
  
 Gli handle di ambiente non vengono utilizzati di frequente nelle applicazioni ODBC. Vengono sempre utilizzati nelle chiamate a **SQLDataSources** e **SQLDrivers** e talvolta utilizzati nelle chiamate a **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**e **SQLGetDiagRec**.  
  
 Ogni parte di codice che implementa ODBC (Gestione Driver o un driver) contiene uno o più handle di ambiente. Ad esempio, Gestione Driver gestisce un handle di ambiente separato per ogni applicazione che è connesso a esso. Gli handle di ambiente vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
