---
title: Mapping di SQLFreeEnv | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f56bfeaee32e83ded6d8269873c9c4c33ed434e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302032"
---
# <a name="sqlfreeenv-mapping"></a>Mapping di SQLFreeEnv
Quando un'applicazione chiama **SQLFreeEnv** tramite un driver ODBC *3. x* , la chiamata a  
  
```  
SQLFreeEnv(henv)   
```  
  
 viene mappato a  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 con l'argomento *handle* impostato sul valore in *HENV*.
