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
ms.openlocfilehash: 086c5381f1801baf919508525c17faab93746ca0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003364"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (driver di database desktop)
Questa funzione può recuperare dati da qualsiasi colonna, se esistono colonne associate, dopo di esso e indipendentemente dall'ordine in cui vengono recuperate le colonne.  
  
> [!NOTE]  
>  \*in pcbValue **SQLGetData** possono restituire due volte come molti caratteri come effettivamente disponibili durante l'associazione a dati ANSI più di 510 caratteri in un database Jet 4.0. I valori di carattere di 510 o meno restituirà il cbValue effettivo.
