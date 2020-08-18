---
description: Limitazioni dell'istruzione DROP TABLE
title: Limitazioni dell'istruzione DROP TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d56e53d8a17c15736e9423e5920c81f864e2973
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412557"
---
# <a name="drop-table-statement-limitations"></a>Limitazioni dell'istruzione DROP TABLE
Quando si utilizza il driver Microsoft Excel 5,0, 7,0 o 97, l'istruzione DROP TABLE Cancella il foglio di lavoro senza eliminare il nome del foglio di lavoro. Poiché il nome del foglio di lavoro esiste ancora nella cartella di lavoro, non è possibile creare un altro foglio di lavoro con lo stesso nome.
