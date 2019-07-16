---
title: Recupero di valori nei campi di descrizione | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020454"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recupero di valori nei campi del descrittore
Un'applicazione può chiamare **SQLGetDescField** per ottenere un singolo campo di un record del descrittore. **SQLGetDescField** offre l'accesso all'applicazione per tutti i campi di descrizione definiti in ODBC e anche i campi definiti dal driver.  
  
 **SQLGetDescRec** può essere chiamato per recuperare le impostazioni di più campi di descrizione che interessano il tipo di dati e archiviazione dei dati di colonna o parametro.
