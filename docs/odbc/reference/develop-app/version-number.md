---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03678023990fc15d03c73501f331ecc302f6b892
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208443"
---
# <a name="version-number"></a>Numero di versione
Esistono diverse versioni di ODBC, ognuna con funzionalità diverse. Un'applicazione determina quale versione ODBC Driver Manager e un driver specifico supportano chiamando **SQLGetInfo** con le opzioni SQL_ODBC_VER e SQL_DRIVER_ODBC_VER.
