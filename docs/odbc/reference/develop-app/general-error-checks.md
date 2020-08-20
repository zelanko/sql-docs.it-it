---
description: Controlli degli errori generali
title: Controlli generali sugli errori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 014959769eb9b419595f122d099efbdc8fa7c1fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465773"
---
# <a name="general-error-checks"></a>Controlli degli errori generali
Gestione driver verifica un errore generale. Restituisce sempre SQL_ERROR quando viene rilevato l'errore seguente: la funzione deve essere supportata dal driver.
