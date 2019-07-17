---
title: SQLRowCount (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be902866cfcf98a10af2c3741926de8b7541bb79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125604"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLRowCount** funzione nella libreria di cursori. Per informazioni generali sul **SQLRowCount**, vedere [funzione SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Quando un'applicazione chiama **SQLRowCount** con l'istruzione associato al cursore, la libreria di cursori restituisce il numero di righe di dati che sono recuperati dal driver.  
  
 Quando un'applicazione chiama **SQLRowCount** con l'istruzione associata a un'istruzione delete o un aggiornamento posizionato, la libreria di cursori restituisce il numero di righe interessate dall'istruzione.  
  
 Quando un'applicazione chiama **SQLRowCount** dopo un **seleziona** istruzione, la libreria di cursori restituisce -1.
