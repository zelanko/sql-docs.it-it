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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b36c02d772682088a799cfca66f5bbf3e169a67f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096538"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Creazione e apertura di tabelle (driver file di testo)
Quando si utilizza il driver di testo, viene creata una nuova tabella utilizzando il formato specificato in Odbcinst. ini. Se non specificato, le tabelle vengono create nel formato CSVDELIMITED. Per impostazione predefinita, le colonne di tipo INTEGER sono impostate su un valore predefinito di 11 caratteri e le colonne FLOAT vengono impostate su 22 Le colonne della data usano il formato AAAA-MM-GG. Le colonne CHAR e LONGCHAR sono la larghezza specificata nell'istruzione CREATE.
