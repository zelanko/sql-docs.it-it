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
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096538"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Creazione e apertura di tabelle (driver file di testo)
Quando viene usato il driver di testo, viene creata una nuova tabella utilizzando il formato specificato in Odbcinst. ini. Se non specificato, vengono create tabelle in formato CSVDELIMITED. Per impostazione predefinita, le colonne FLOAT per impostazione predefinita 22 caratteri e colonne di tipo INTEGER predefiniti a 11 caratteri. Le colonne data usano il formato AAAA-MM-GG. CHAR e le colonne LONGCHAR sono la larghezza specificata nell'istruzione CREATE.
