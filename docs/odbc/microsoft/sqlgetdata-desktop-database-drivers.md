---
title: SQLGetData (driver di Database Desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f362d725f8b734ab9ecdbdc79c268af08a495b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313134"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (driver di database desktop)
Questa funzione può recuperare dati da qualsiasi colonna, se esistono colonne associate, dopo di esso e indipendentemente dall'ordine in cui vengono recuperate le colonne.  
  
> [!NOTE]  
>  \*in pcbValue **SQLGetData** possono restituire due volte come molti caratteri come effettivamente disponibili durante l'associazione a dati ANSI più di 510 caratteri in un database Jet 4.0. I valori di carattere di 510 o meno restituirà il cbValue effettivo.
