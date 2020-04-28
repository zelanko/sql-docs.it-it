---
title: Popolamento automatico del dispositivo dpi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1998ea1992ee7f14d87d01e348d955b017166088
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285071"
---
# <a name="automatic-population-of-the-ipd"></a>Popolamento automatico dell'IPD
Alcuni driver sono in grado di impostare i campi del dip dopo che è stata preparata una query con parametri. I campi del descrittore vengono popolati automaticamente con informazioni sul parametro, inclusi il tipo di dati, la precisione, la scala e altre caratteristiche. Questa operazione equivale a supportare **SQLDescribeParam**. Queste informazioni possono essere particolarmente utili per un'applicazione quando non sono disponibili altri modi per individuarle, ad esempio quando viene eseguita una query ad hoc con i parametri di cui l'applicazione non è a conoscenza.  
  
 Un'applicazione determina se il driver supporta il popolamento automatico chiamando **SQLGetConnectAttr** con un *attributo* di SQL_ATTR_AUTO_IPD. Se viene restituito SQL_TRUE, il driver lo supporta e l'applicazione può abilitarla impostando l'attributo dell'istruzione SQL_ATTR_ENABLE_AUTO_IPD su SQL_TRUE.  
  
 Quando il popolamento automatico è supportato e abilitato, il driver compila i campi del valore dpi dopo che un'istruzione SQL contenente i marcatori di parametro è stata preparata da una chiamata a **SQLPrepare**. Un'applicazione può recuperare queste informazioni chiamando **SQLGetDescField** o **SQLGetDescRec**o **SQLDescribeParam**. L'applicazione può utilizzare le informazioni per associare il buffer dell'applicazione più appropriato per un parametro o per specificare una conversione dei dati.  
  
 Il popolamento automatico del dpi potrebbe produrre una riduzione delle prestazioni. Un'applicazione può disattivarla reimpostando l'attributo dell'istruzione SQL_ATTR_ENABLE_AUTO_IPD su SQL_FALSE (valore predefinito).
