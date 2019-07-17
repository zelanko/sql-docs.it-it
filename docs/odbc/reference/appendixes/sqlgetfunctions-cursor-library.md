---
title: SQLGetFunctions (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1497a7d2ec5951feedb36831ab541413e57152f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073930"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLGetFunctions** funzione nella libreria di cursori. Per informazioni generali sul **SQLGetFunctions**, vedere [funzione SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Quando si chiama **SQLGetFunctions**, la libreria di cursori restituisce che supporta **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**, e **SQLSetScrollOptions**, oltre alle funzioni supportate dal driver.
