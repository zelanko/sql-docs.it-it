---
title: L'elaborazione di istruzioni SELECT FOR UPDATE | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028372"
---
# <a name="processing-select-for-update-statements"></a>Elaborazione di istruzioni SELECT FOR UPDATE
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Per garantire la massima interoperabilità, le applicazioni devono generare set di risultati che verranno aggiornate con un'istruzione di aggiornamento posizionato tramite l'esecuzione di un **selezionare per aggiornare** istruzione. Anche se la libreria di cursori non è richiesto, è necessaria per la maggior parte delle origini dati che supportano le istruzioni per gli aggiornamenti posizionati.  
  
 La libreria di cursori vengono ignorate le colonne nel **FOR UPDATE** clausola di un **SELECT FOR UPDATE** istruzione; prima di passare l'istruzione per il driver rimuove questa clausola. Nella libreria di cursori, l'attributo di istruzione SQL_ATTR_CONCURRENCY, con le restrizioni indicate nella sezione precedente, i controlli se impostare le colonne in un risultato possono essere aggiornati.
