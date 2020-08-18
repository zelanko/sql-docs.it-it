---
description: SQLSetCursorName (driver di database desktop)
title: SQLSetCursorName (driver di database desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14fe15c6cdbdf50e6d28ca7e9a1168f54626e83b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411556"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (driver di database desktop)
Poiché il driver non supporta un'operazione di aggiornamento o eliminazione posizionata dalla sintassi WHERE CURRENT OF *CursorName* , **SQLSetCursorName** è supportato, ma non può essere usato per gli aggiornamenti posizionati. Può essere utilizzato solo quando la libreria di cursori è abilitata e l'applicazione utilizza **SQLExtendedFetch**.
