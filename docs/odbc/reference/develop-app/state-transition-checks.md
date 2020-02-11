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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107278"
---
# <a name="state-transition-checks"></a>Controlli della transizione di stato
Gestione driver verifica che lo stato dell'ambiente, della connessione o dell'istruzione sia appropriato per la funzione chiamata. Una connessione, ad esempio, deve essere in uno stato allocato quando viene chiamato **SQLConnect** ; un'istruzione deve essere in uno stato preparato quando viene chiamato **SQLExecute** . Gestione driver restituisce SQL_ERROR per gli errori di transizione di stato.
