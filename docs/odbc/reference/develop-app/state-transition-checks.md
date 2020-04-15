---
title: Controlli di transizione dello stato Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299706"
---
# <a name="state-transition-checks"></a>Controlli della transizione di stato
Gestione Driver verifica che lo stato dell'ambiente, connessione o istruzione sia appropriato per la funzione chiamata. Ad esempio, una connessione deve essere in uno stato allocato quando **SQLConnect** viene chiamato; un'istruzione deve essere in uno stato preparato quando **SQLExecute** viene chiamato. Gestione Driver restituisce SQL_ERROR per gli errori di transizione di stato.
