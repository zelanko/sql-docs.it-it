---
title: Creazione e apertura di tabelle (driver file di testo) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae13312299f131d1957557db28bbe4db0bf7b4c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280921"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Creazione e apertura di tabelle (driver file di testo)
Quando si utilizza il driver di testo, viene creata una nuova tabella utilizzando il formato specificato in Odbcinst. ini. Se non specificato, le tabelle vengono create nel formato CSVDELIMITED. Per impostazione predefinita, le colonne di tipo INTEGER sono impostate su un valore predefinito di 11 caratteri e le colonne FLOAT vengono impostate su 22 Le colonne della data usano il formato AAAA-MM-GG. Le colonne CHAR e LONGCHAR sono la larghezza specificata nell'istruzione CREATE.
