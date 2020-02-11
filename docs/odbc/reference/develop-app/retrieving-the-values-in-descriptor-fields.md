---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55d7017c659ca4d0b8094ed4a665d27c10b355f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020454"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recupero di valori nei campi del descrittore
Un'applicazione può chiamare **SQLGetDescField** per ottenere un singolo campo di un record di descrittore. **SQLGetDescField** consente all'applicazione di accedere a tutti i campi di descrizione definiti in ODBC e anche ai campi definiti dal driver.  
  
 È possibile chiamare **SQLGetDescRec** per recuperare le impostazioni di più campi di descrizione che influiscono sul tipo di dati e sull'archiviazione dei dati di colonna o di parametro.
