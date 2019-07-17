---
title: Tipi di dati Visual FoxPro campo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087948"
---
# <a name="visual-foxpro-field-data-types"></a>Tipi di dati dei campi Visual FoxPro
Nella tabella seguente sono elencati i valori per il *FieldType* argomento nell'istruzione ALTER TABLE e CREATE TABLE indicando se *nFieldWidth* e *nPrecision* gli argomenti sono Obbligatorio.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descrizione|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|Double|  
|C|N|-|Campo di caratteri della larghezza *n*|  
|D|-|-|Date|  
|F|N|d|Mobile campo numerico della larghezza *n* con *1!d* posizioni decimali|  
|G|-|-|Generale|  
|I|-|-|Integer|  
|L|-|-|Logico|  
|M|-|-|Memo|  
|N|N|d|Campo numerico della larghezza *n* con *1!d* posizioni decimali|  
|T|-|-|DateTime|  
|Y|-|-|Currency|
