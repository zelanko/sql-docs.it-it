---
description: Controlli della transizione di stato
title: Controlli della transizione di stato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 50a845f2b83ada7c9d4f03f252b6d2bc3d3eff3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476373"
---
# <a name="state-transition-checks"></a>Controlli della transizione di stato
Gestione driver verifica che lo stato dell'ambiente, della connessione o dell'istruzione sia appropriato per la funzione chiamata. Una connessione, ad esempio, deve essere in uno stato allocato quando viene chiamato **SQLConnect** ; un'istruzione deve essere in uno stato preparato quando viene chiamato **SQLExecute** . Gestione driver restituisce SQL_ERROR per gli errori di transizione di stato.
