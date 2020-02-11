---
title: SQLGetData (driver di database desktop) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003364"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (driver di database desktop)
Questa funzione può recuperare i dati da qualsiasi colonna, indipendentemente dal fatto che vi siano colonne associate e indipendentemente dall'ordine in cui le colonne vengono recuperate.  
  
> [!NOTE]  
>  \*pcbValue in **SQLGetData** può restituire il doppio dei caratteri effettivamente disponibili quando si esegue il binding ai dati ANSI con una lunghezza superiore a 510 caratteri in un database Jet 4,0. I valori di carattere di 510 o minori restituiranno il cbValue effettivo.
