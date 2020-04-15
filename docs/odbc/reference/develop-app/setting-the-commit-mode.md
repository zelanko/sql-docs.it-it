---
title: Impostazione della modalità di commit Documenti Microsoft
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
ms.openlocfilehash: f05aaca2349a612cda7c5b6b257e7a1d5a5ea9c5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299821"
---
# <a name="setting-the-commit-mode"></a>Impostazione della modalità di commit
Le applicazioni specificano la modalità di transazione con l'attributo di connessione SQL_ATTR_AUTOCOMMIT. Per impostazione predefinita, le transazioni ODBC sono in modalità di commit automatico (a meno che **SQLSetConnectAttr** e **SQLSetConnectOption** non siano supportate, il che è improbabile). Il passaggio dalla modalità di commit manuale alla modalità di commit automatico esegue automaticamente il commit di qualsiasi transazione aperta sulla connessione.
