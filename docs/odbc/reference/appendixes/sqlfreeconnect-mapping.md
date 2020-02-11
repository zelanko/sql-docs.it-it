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
ms.openlocfilehash: 062894547aca57ca01ca105f4060f2dcd39e942f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086445"
---
# <a name="sqlfreeconnect-mapping"></a>Mapping di SQLFreeConnect
Quando un'applicazione chiama **SQLFreeConnect** tramite un driver ODBC *3. x* , la chiamata a  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 viene mappato a  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 con l'argomento *handle* impostato sul valore in *HDBC*.
