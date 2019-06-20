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
manager: craigg
ms.openlocfilehash: ae95160a11a965e47845726748c2b9449a819e8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284956"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recupero di valori nei campi del descrittore
Un'applicazione può chiamare **SQLGetDescField** per ottenere un singolo campo di un record del descrittore. **SQLGetDescField** offre l'accesso all'applicazione per tutti i campi di descrizione definiti in ODBC e anche i campi definiti dal driver.  
  
 **SQLGetDescRec** può essere chiamato per recuperare le impostazioni di più campi di descrizione che interessano il tipo di dati e archiviazione dei dati di colonna o parametro.
