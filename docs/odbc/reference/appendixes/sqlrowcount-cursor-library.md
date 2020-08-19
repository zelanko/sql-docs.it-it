---
description: SQLRowCount (libreria di cursori)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02c972d4847ef0736e6f9e9ac91f8f617e1d9df0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424879"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLRowCount** nella libreria di cursori. Per informazioni generali su **SQLRowCount**, vedere [funzione SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Quando un'applicazione chiama **SQLRowCount** con l'istruzione associata al cursore, la libreria di cursori restituisce il numero di righe di dati recuperate dal driver.  
  
 Quando un'applicazione chiama **SQLRowCount** con l'istruzione associata a un'istruzione Update o DELETE posizionata, la libreria di cursori restituisce il numero di righe interessate dall'istruzione.  
  
 Quando un'applicazione chiama **SQLRowCount** dopo un'istruzione **SELECT** , la libreria di cursori restituisce-1.
