---
description: Creazione e apertura di tabelle (driver file di testo)
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
ms.openlocfilehash: c64f74270e8c2bbf4645f72406113e88948d0da9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340967"
---
# <a name="creating-and-opening-tables-text-file-driver"></a>Creazione e apertura di tabelle (driver file di testo)
Quando si utilizza il driver di testo, viene creata una nuova tabella utilizzando il formato specificato in Odbcinst.ini. Se non specificato, le tabelle vengono create nel formato CSVDELIMITED. Per impostazione predefinita, le colonne di tipo INTEGER sono impostate su un valore predefinito di 11 caratteri e le colonne FLOAT vengono impostate su 22 Le colonne della data usano il formato AAAA-MM-GG. Le colonne CHAR e LONGCHAR sono la larghezza specificata nell'istruzione CREATE.
