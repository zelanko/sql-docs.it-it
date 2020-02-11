---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a43a78ad9453f65d9b12595851bd622f720b409a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094218"
---
# <a name="setting-the-commit-mode"></a>Impostazione della modalità di commit
Le applicazioni specificano la modalità di transazione con l'attributo di connessione SQL_ATTR_AUTOCOMMIT. Per impostazione predefinita, le transazioni ODBC sono in modalità autocommit, a meno che non siano supportati **SQLSetConnectAttr** e **SQLSetConnectOption** , che è improbabile. Il cambio dalla modalità con commit manuale alla modalità di commit automatico consente di eseguire automaticamente il commit di tutte le transazioni aperte sulla connessione.
