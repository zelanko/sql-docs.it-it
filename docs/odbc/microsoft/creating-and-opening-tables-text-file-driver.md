---
title: Creazione e apertura di tabelle (Driver File di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], creating and opening tables
ms.assetid: e6a07dda-a665-4f5b-a8d6-9ff479700513
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ce901e6a8639c8a2caea6e55cbaa18fedb56f4a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63132733"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Creazione e apertura di tabelle (driver file di testo)
Quando viene usato il driver di testo, viene creata una nuova tabella utilizzando il formato specificato in Odbcinst. ini. Se non specificato, vengono create tabelle in formato CSVDELIMITED. Per impostazione predefinita, le colonne FLOAT per impostazione predefinita 22 caratteri e colonne di tipo INTEGER predefiniti a 11 caratteri. Le colonne data usano il formato AAAA-MM-GG. CHAR e le colonne LONGCHAR sono la larghezza specificata nell'istruzione CREATE.
