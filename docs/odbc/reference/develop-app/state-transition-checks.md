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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107278"
---
# <a name="state-transition-checks"></a>Controlli della transizione di stato
Gestione Driver controlla che lo stato dell'ambiente, la connessione o dell'istruzione è appropriato per la funzione chiamata. Ad esempio, una connessione deve essere allocato un stato quando **SQLConnect** viene chiamato; deve essere un'istruzione in una stato quando **SQLExecute** viene chiamato. Gestione Driver restituisce SQL_ERROR per gli errori di transizione di stato.
