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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3604e9f3bd47a10ae1a6e5ec401b198675c2d3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149293"
---
# <a name="how-is-metadata-used"></a>Modalità di utilizzo dei metadati
Le applicazioni richiedono metadati per la maggior parte delle operazioni sui set di risultati. L'applicazione, ad esempio, utilizza il tipo di dati di una colonna per determinare il tipo di variabile da associare alla colonna. La lunghezza in byte di una colonna di tipo carattere utilizza per determinare la quantità di spazio che è necessario visualizzare dati di tale colonna. Il modo in cui un'applicazione determina i metadati per una colonna dipende dal tipo dell'applicazione.  
  
 Applicazioni verticali utilizzano le tabelle predefinite ed eseguono operazioni predefinite in tali tabelle. Poiché i metadati di set di risultati per tali applicazioni vengano definito prima che l'applicazione viene anche scritta e è controllata dallo sviluppatore dell'applicazione, può essere hardcoded nell'applicazione. Se, ad esempio, una colonna di ID ordine viene definita come valore integer a 4 byte nell'origine dati, l'applicazione può sempre associare un valore integer a 4 byte alla colonna. Quando i metadati vengono specificati a livello di codice nell'applicazione, una modifica apportata alle tabelle utilizzate dall'applicazione comporta in genere una modifica al codice dell'applicazione. Ciò è raramente è un problema, perché tali modifiche vengono apportate in genere come parte di una nuova versione dell'applicazione.  
  
 Come le applicazioni verticali, applicazioni personalizzate a livello generale con le tabelle predefinite ed eseguono operazioni predefinite in tali tabelle. Ad esempio, potrà scrivere un'applicazione per trasferire i dati tra tre origini dati diverse. i trasferimento dei dati sono noto in genere quando l'applicazione è scritta. Di conseguenza, le applicazioni personalizzate è anche tendono ad avere i metadati a livello di codice.  
  
 Applicazioni generiche, specialmente quelli che supportano query ad hoc, non conoscere quasi mai i metadati dei set di risultati creati. Pertanto, scoprono i metadati in fase di esecuzione usando le funzioni **SQLNumResultCols**, **SQLDescribeCol**, e **SQLColAttribute**, che sono descritte nel la sezione successiva [SQLDescribeCol e SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md).  
  
 Tutte le applicazioni, indipendentemente dal loro tipo, possono codificare i metadati per i set di risultati restituiti dalle funzioni di catalogo. Questi set di risultati sono definiti nella sezione riferimenti di questo manuale.
