---
title: Maniglie del descrittore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed0595c97f3f4ad92d976c89327a01e25cb5b753
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305912"
---
# <a name="descriptor-handles"></a>Handle del descrittore
Un *descrittore* è un insieme di metadati che descrive i parametri di un'istruzione SQL o le colonne di un set di risultati, come illustrato dall'applicazione o dal driver (noto anche come *implementazione*). Pertanto, un descrittore può ricoprire uno qualsiasi dei quattro ruoli seguenti:So, a descriptor can fill any of four roles:  
  
-   **descrittore di parametri dell'applicazione (APD).** Contiene informazioni sui buffer dell'applicazione associati ai parametri in un'istruzione SQL, ad esempio i relativi indirizzi, lunghezze e tipi di dati C.  
  
-   **Descrittore del parametro di implementazione (IPD).** Contiene informazioni sui parametri in un'istruzione SQL, ad esempio i tipi di dati SQL, le lunghezze e il supporto di valori Null.  
  
-   **Descrittore di riga dell'applicazione (ARD).** Contiene informazioni sui buffer dell'applicazione associati alle colonne in un set di risultati, ad esempio i relativi indirizzi, lunghezze e tipi di dati C.  
  
-   **Descrittore di riga di implementazione (IRD).** Contiene informazioni sulle colonne in un set di risultati, ad esempio i tipi di dati SQL, le lunghezze e il supporto di valori Null.Contains information about the columns in a result set, such as their SQL data types, lengths, and nullability.  
  
 Quattro descrittori (uno che riempie ogni ruolo) vengono allocati automaticamente quando viene allocata un'istruzione. Questi sono *noti come descrittori allocati automaticamente* e sono sempre associati a tale istruzione. Le applicazioni possono inoltre allocare descrittori con **SQLAllocHandle**. Questi sono *noti come descrittori allocati in modo esplicito*. Vengono allocati in una connessione e possono essere associati a una o più istruzioni su tale connessione per adempiere al ruolo di un APD o ARD in tali dichiarazioni.  
  
 La maggior parte delle operazioni in ODBC può essere eseguita senza l'utilizzo esplicito dei descrittori da parte dell'applicazione. Tuttavia, i descrittori forniscono una comoda scelta rapida per alcune operazioni. Si supponga, ad esempio, che un'applicazione desideri inserire dati da due set diversi di buffer. Per utilizzare il primo set di buffer, è necessario chiamare ripetutamente **SQLBindParameter** per associarli ai parametri in un'istruzione **INSERT** e quindi eseguire l'istruzione. Per utilizzare il secondo set di buffer, ripetere questo processo. In alternativa, è possibile impostare associazioni al primo set di buffer in un descrittore e al secondo set di buffer in un altro descrittore. Per passare da un set di associazioni all'altro, l'applicazione chiamerebbe semplicemente **SQLSetStmtAttr** e associa il descrittore corretto all'istruzione come APD.  
  
 Per ulteriori informazioni sui descrittori, vedere [Tipi di descrittori](../../../odbc/reference/develop-app/types-of-descriptors.md).
