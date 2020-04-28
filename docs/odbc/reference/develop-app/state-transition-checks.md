---
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
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299706"
---
# <a name="state-transition-checks"></a>Controlli della transizione di stato
Gestione driver verifica che lo stato dell'ambiente, della connessione o dell'istruzione sia appropriato per la funzione chiamata. Una connessione, ad esempio, deve essere in uno stato allocato quando viene chiamato **SQLConnect** ; un'istruzione deve essere in uno stato preparato quando viene chiamato **SQLExecute** . Gestione driver restituisce SQL_ERROR per gli errori di transizione di stato.
