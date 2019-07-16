---
title: Il popolamento automatico dell'IPD | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1591843667ef01c6c88f5dfafb734f044679b2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909835"
---
# <a name="automatic-population-of-the-ipd"></a>Popolamento automatico dell'IPD
Alcuni driver sono in grado di impostazione dei campi dell'IPD dopo aver preparata una query con parametri. I campi di descrizione vengono popolati automaticamente con informazioni sul parametro, inclusi il tipo di dati, precisione, scala e altre caratteristiche. Ciò equivale a supportare **SQLDescribeParam**. Queste informazioni possono essere particolarmente utile per un'applicazione quando non dispone di alcun altro modo per individuarlo, ad esempio quando viene eseguita una query ad hoc con parametri che l'applicazione non conosce.  
  
 Un'applicazione determina se il driver supporta il popolamento automatico chiamando **SQLGetConnectAttr** con un *attributo* di SQL_ATTR_AUTO_IPD. Se viene restituito SQL_TRUE, il driver supporta e l'applicazione può consentire impostando l'attributo di istruzione SQL_ATTR_ENABLE_AUTO_IPD su SQL_TRUE.  
  
 Quando il popolamento automatico è supportato e abilitato, il driver compila i campi dell'IPD dopo che è stata preparata un'istruzione SQL che contengono marcatori di parametro da una chiamata a **SQLPrepare**. Un'applicazione può recuperare queste informazioni chiamando **SQLGetDescField** oppure **SQLGetDescRec**, o **SQLDescribeParam**. L'applicazione può usare le informazioni da associare al buffer dell'applicazione più appropriato per un parametro o per specificare una conversione di dati per esso.  
  
 Il popolamento automatico dell'IPD produca una riduzione delle prestazioni. Un'applicazione possa disattivarla ripristinando l'attributo di istruzione SQL_ATTR_ENABLE_AUTO_IPD SQL_FALSE (valore predefinito).
