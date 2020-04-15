---
title: Modalità di utilizzo dei metadati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fbbba96fa2e99a2ccc0618f31e3b29e7d479f703
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300171"
---
# <a name="how-is-metadata-used"></a>Modalità di utilizzo dei metadati
Le applicazioni richiedono metadati per la maggior parte delle operazioni sui set di risultati. L'applicazione, ad esempio, utilizza il tipo di dati di una colonna per determinare il tipo di variabile da associare alla colonna. Utilizza la lunghezza in byte di una colonna di caratteri per determinare la quantità di spazio necessario per visualizzare i dati da tale colonna. Il modo in cui un'applicazione determina i metadati per una colonna dipende dal tipo dell'applicazione.  
  
 Le applicazioni verticali funzionano con tabelle predefinite ed eseguono operazioni predefinite su tali tabelle. Poiché i metadati del set di risultati per tali applicazioni vengono definiti prima che l'applicazione venga scritta e controllata dallo sviluppatore dell'applicazione, possono essere hardcoded nell'applicazione. Se, ad esempio, una colonna di ID ordine viene definita come valore integer a 4 byte nell'origine dati, l'applicazione può sempre associare un valore integer a 4 byte alla colonna. Quando i metadati vengono specificati a livello di codice nell'applicazione, una modifica apportata alle tabelle utilizzate dall'applicazione comporta in genere una modifica al codice dell'applicazione. Questo è raramente un problema, perché tali modifiche vengono in genere apportate come parte di una nuova versione dell'applicazione.  
  
 Analogamente alle applicazioni verticali, le applicazioni personalizzate in genere funzionano con tabelle predefinite ed eseguono operazioni predefinite su tali tabelle. Ad esempio, un'applicazione potrebbe essere scritta per trasferire dati tra tre origini dati diverse; i dati da trasferire sono in genere noti quando viene scritta l'applicazione. Di conseguenza, anche le applicazioni personalizzate tendono ad avere metadati hardcoded.  
  
 Le applicazioni generiche, in particolare quelle che supportano query ad hoc, non conoscono quasi mai i metadati dei set di risultati che creano. Pertanto, devono individuare i metadati in fase di esecuzione utilizzando le funzioni **SQLNumResultCols**, **SQLDescribeCol**e **SQLColAttribute**, descritte nella sezione successiva, [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Tutte le applicazioni, indipendentemente dal tipo, possono impostare come hardcoded i metadati per i set di risultati restituiti dalle funzioni di catalogo. Questi set di risultati sono definiti nella sezione di riferimento di questo manuale.
