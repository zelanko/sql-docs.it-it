---
title: Elaborazione delle istruzioni SELECT FOR UPDATE Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 904028cd7b3798fcac8f9e5afa6186fae3e9fa29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308012"
---
# <a name="processing-select-for-update-statements"></a>Elaborazione di istruzioni SELECT FOR UPDATE
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 Per garantire la massima interoperabilità, le applicazioni devono generare set di risultati che verranno aggiornati con un'istruzione di aggiornamento posizionato eseguendo un'istruzione **SELECT FOR UPDATE.** Anche se la libreria di cursori non lo richiede, è richiesta dalla maggior parte delle origini dati che supportano istruzioni di aggiornamento posizionate.  
  
 La libreria di cursori ignora le colonne nella clausola **FOR UPDATE** di un'istruzione SELECT **FOR UPDATE.** rimuove questa clausola prima di passare l'istruzione al driver. Nella libreria di cursori, l'attributo di istruzione SQL_ATTR_CONCURRENCY, insieme alle restrizioni indicate nella sezione precedente, controlla se le colonne in un set di risultati possono essere aggiornate.
