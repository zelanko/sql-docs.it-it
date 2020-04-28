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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304122"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (driver di database desktop)
Questa funzione può recuperare i dati da qualsiasi colonna, indipendentemente dal fatto che vi siano colonne associate e indipendentemente dall'ordine in cui le colonne vengono recuperate.  
  
> [!NOTE]  
>  \*pcbValue in **SQLGetData** può restituire il doppio dei caratteri effettivamente disponibili quando si esegue il binding ai dati ANSI con una lunghezza superiore a 510 caratteri in un database Jet 4,0. I valori di carattere di 510 o minori restituiranno il cbValue effettivo.
