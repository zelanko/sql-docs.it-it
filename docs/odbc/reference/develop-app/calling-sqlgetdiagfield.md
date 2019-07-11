---
title: Chiamata di SQLGetDiagField | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42d24de7e5e94a3301653eb3082140e260a1e745
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793897"
---
# <a name="calling-sqlgetdiagfield"></a>Chiamata di SQLGetDiagField
Quando un'applicazione ODBC *3.x* applicazione chiama **SQLGetDiagField** in un database ODBC *2.x* driver, il driver restituisce SQL_SUCCESS e le informazioni appropriate nella  *\*DiagInfoPtr* se il *DiagIdentifier* argomento è SQL_DIAG_CLASS_ORIGIN, SQL_DIAG_CLASS_SUBCLASS_ORIGIN, SQL_DIAG_CONNECTION_NAME, SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_ NATIVE, SQL_DIAG_NUMBER, SQL_DIAG_RETURNCODE, SQL_DIAG_SERVER_NAME o SQL_DIAG_SQLSTATE. Tutti gli altri campi di diagnostica restituirà SQL_ERROR.
