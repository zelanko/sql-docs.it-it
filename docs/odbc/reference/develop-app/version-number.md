---
description: Numero di versione
title: Numero di versione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- version number supported [ODBC]
- interoperability [ODBC], version number supported
ms.assetid: 6eccacdf-b837-4b66-bd48-ba31771acecb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86da481ef7854bb9878c2bac565ef2797b61f5ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421425"
---
# <a name="version-number"></a>Numero di versione
Sono disponibili diverse versioni di ODBC, ognuna con funzionalità diverse. Un'applicazione determina quale versione ODBC Gestione driver e un driver specifico supportano chiamando **SQLGetInfo** con le opzioni SQL_ODBC_VER e SQL_DRIVER_ODBC_VER.
