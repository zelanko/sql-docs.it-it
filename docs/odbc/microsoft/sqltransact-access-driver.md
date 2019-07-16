---
title: SQLTransact (Driver Access) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4d4b3d8d417591bd72dde22240c81a91d80f990
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948976"
---
# <a name="sqltransact-access-driver"></a>SQLTransact (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Quando viene usato il driver Microsoft Access, SQL_COMMIT e SQL_ROLLBACK sono supportati per il *fType* argomento nella chiamata a **SQLTransact**.  
  
 Se si verifica un errore durante il processo di commit, i database interessato può essere corretti tramite l'opzione di Database di ripristino nell'installazione driver Microsoft Access, oppure tramite la parola chiave REPAIR_DB nel **SQLConfigDataSource** funzione.
