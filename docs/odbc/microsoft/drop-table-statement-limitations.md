---
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
ms.openlocfilehash: c296108b9ab26a6361d12ad71a1f21b21d5bea1e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303402"
---
# <a name="drop-table-statement-limitations"></a>Limitazioni dell'istruzione DROP TABLE
Quando si utilizza il driver Microsoft Excel 5,0, 7,0 o 97, l'istruzione DROP TABLE Cancella il foglio di lavoro senza eliminare il nome del foglio di lavoro. Poiché il nome del foglio di lavoro esiste ancora nella cartella di lavoro, non è possibile creare un altro foglio di lavoro con lo stesso nome.
