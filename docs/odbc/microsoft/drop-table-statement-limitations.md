---
title: Limitazioni dell'istruzione DROP tabella | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a24a22a5e666421136780f3614db4df2233bc82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128012"
---
# <a name="drop-table-statement-limitations"></a>Limitazioni dell'istruzione DROP TABLE
Quando viene usato il driver di Microsoft Excel 97, versione 7.0 o 5.0, l'istruzione DROP TABLE consente di cancellare il foglio di lavoro ma non elimina il nome del foglio di lavoro. Poiché il nome del foglio di lavoro è ancora presente nella cartella di lavoro, un altro foglio di lavoro non è possibile creare con lo stesso nome.
