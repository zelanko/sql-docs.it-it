---
description: Recupero di valori nei campi del descrittore
title: Recupero dei valori nei campi del descrittore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2118efe58b076287dd75192de679bdb74299435
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494649"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recupero di valori nei campi del descrittore
Un'applicazione può chiamare **SQLGetDescField** per ottenere un singolo campo di un record di descrittore. **SQLGetDescField** consente all'applicazione di accedere a tutti i campi di descrizione definiti in ODBC e anche ai campi definiti dal driver.  
  
 È possibile chiamare **SQLGetDescRec** per recuperare le impostazioni di più campi di descrizione che influiscono sul tipo di dati e sull'archiviazione dei dati di colonna o di parametro.
