---
title: Mapping di SQLFreeConnect | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b9a35275d95207fd8ceef296ecda4664a1c4e7f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793596"
---
# <a name="sqlfreeconnect-mapping"></a>Mapping di SQLFreeConnect
Quando un'applicazione chiama **SQLFreeConnect** tramite un database ODBC *3.x* driver, la chiamata a  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 viene eseguito il mapping a  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 con il *gestiscono* impostata sul valore nell'argomento *hdbc*.
