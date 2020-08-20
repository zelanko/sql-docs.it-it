---
description: Impostazione della modalità di commit
title: Impostazione della modalità commit | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
ms.assetid: b60d0d74-0655-4013-8d5a-bc1866eaa166
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a71d6f97f4683f9177c940be7d6ca1cc4a27c01
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494625"
---
# <a name="setting-the-commit-mode"></a>Impostazione della modalità di commit
Le applicazioni specificano la modalità di transazione con l'attributo di connessione SQL_ATTR_AUTOCOMMIT. Per impostazione predefinita, le transazioni ODBC sono in modalità autocommit, a meno che non siano supportati **SQLSetConnectAttr** e **SQLSetConnectOption** , che è improbabile. Il cambio dalla modalità con commit manuale alla modalità di commit automatico consente di eseguire automaticamente il commit di tutte le transazioni aperte sulla connessione.
