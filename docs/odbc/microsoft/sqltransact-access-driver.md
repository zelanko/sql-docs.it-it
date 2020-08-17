---
description: SQLTransact (driver Access)
title: SQLTransact (driver di accesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLTransact
- SQLTransact function [ODBC], Access Driver
ms.assetid: 892b79c7-9e20-4d1f-bc60-d4b25694ca25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e9b00f8f5a12af2d3823171d22ad53106569352
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339684"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando si utilizza il driver Microsoft Access, SQL_COMMIT e SQL_ROLLBACK sono supportati per l'argomento *ftype* in una chiamata a **SQLTransact**.  
  
 Se si verifica un errore durante il processo di commit, è possibile ripristinare il database interessato utilizzando l'opzione Ripristina database nell'installazione del driver Microsoft Access o tramite l'utilizzo della parola chiave REPAIR_DB nella funzione **SQLConfigDataSource** .
