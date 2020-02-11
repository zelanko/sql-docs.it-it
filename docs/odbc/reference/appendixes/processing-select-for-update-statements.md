---
title: Elaborazione della selezione per le istruzioni UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ad9a20ab8abd40123ec4e4d7369373e68699205
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028372"
---
# <a name="processing-select-for-update-statements"></a>Elaborazione di istruzioni SELECT FOR UPDATE
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 Per garantire la massima interoperabilità, le applicazioni devono generare set di risultati che verranno aggiornati con un'istruzione UPDATE posizionata eseguendo un'istruzione **Select for Update** . Sebbene la libreria di cursori non lo richieda, è richiesta dalla maggior parte delle origini dati che supportano le istruzioni UPDATE posizionate.  
  
 La libreria di cursori ignora le colonne nella clausola **for Update** di un'istruzione **Select for Update** . Questa clausola viene rimossa prima di passare l'istruzione al driver. Nella libreria di cursori, l'attributo SQL_ATTR_CONCURRENCY Statement, insieme alle restrizioni indicate nella sezione precedente, determina se è possibile aggiornare le colonne di un set di risultati.
