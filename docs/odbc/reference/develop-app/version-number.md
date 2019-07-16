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
ms.openlocfilehash: 331b60b31c49a203da5f25c4481a604132fbb0e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079556"
---
# <a name="version-number"></a>Numero di versione
Esistono diverse versioni di ODBC, ognuna con funzionalità diverse. Un'applicazione determina quale versione ODBC Driver Manager e un driver specifico supportano chiamando **SQLGetInfo** con le opzioni SQL_ODBC_VER e SQL_DRIVER_ODBC_VER.
