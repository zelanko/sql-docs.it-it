---
title: Recupero dei valori nei campi del descrittore Documenti Microsoft
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
ms.openlocfilehash: 43467d19f3f2e576efa0402c4ba513e23da59390
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304322"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>Recupero di valori nei campi del descrittore
Un'applicazione può chiamare **SQLGetDescField** per ottenere un singolo campo di un record del descrittore. **SQLGetDescField** consente all'applicazione di accedere a tutti i campi del descrittore definiti in ODBC e anche ai campi definiti dal driver.  
  
 **SQLGetDescRec** può essere chiamato per recuperare le impostazioni di più campi descrittore che influiscono sul tipo di dati e sull'archiviazione dei dati di colonna o parametro.
