---
title: SQLGetData (Driver di database desktop) Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304122"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (driver di database desktop)
Questa funzione può recuperare i dati da qualsiasi colonna, indipendentemente dal fatto che siano presenti colonne associate dopo di essa e indipendentemente dall'ordine in cui vengono recuperate le colonne.  
  
> [!NOTE]  
>  \*pcbValue in **SQLGetData** può restituire il doppio dei caratteri effettivamente disponibili durante l'associazione a dati ANSI più lunghi di 510 caratteri in un database Jet 4.0. I valori di carattere pari o inferiori a 510 restituiranno il valore effettivo di cbValue.
