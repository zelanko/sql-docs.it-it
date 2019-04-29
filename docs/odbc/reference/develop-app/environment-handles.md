---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a73ec4a842e220a16189f1390df167fe12bbab8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942994"
---
# <a name="environment-handles"></a>Handle di ambiente
Un' *ambiente* è un contesto globale in cui si desidera accedere ai dati; associato a un ambiente è qualsiasi informazione che è globale in natura, ad esempio:  
  
-   Stato dell'ambiente  
  
-   La diagnostica a livello di ambiente corrente  
  
-   Gli handle di connessioni attualmente allocate nell'ambiente  
  
-   Le impostazioni correnti di ogni attributo di ambiente  
  
 All'interno di un frammento di codice che implementa ODBC (gestione Driver o un driver), un handle di ambiente identifica una struttura per contenere tali informazioni.  
  
 Handle di ambiente non vengono spesso usati nelle applicazioni ODBC. Vengono sempre usati nelle chiamate a **SQLDataSources** e **SQLDrivers** e a volte usati nelle chiamate a **SQLAllocHandle**, **SQLEndTran**, **SQLFreeHandle**, **SQLGetDiagField**, e **SQLGetDiagRec**.  
  
 Ogni frammento di codice che implementa ODBC (gestione Driver o un driver) contiene uno o più handle di ambiente. Ad esempio, gestione Driver mantiene un handle di ambiente separati per ogni applicazione che vi è connesso. Handle di ambiente vengono allocati con **SQLAllocHandle** e liberati con **SQLFreeHandle**.
