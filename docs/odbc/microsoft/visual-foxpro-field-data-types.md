---
title: Tipi di dati dei campi di Visual FoxPro | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087948"
---
# <a name="visual-foxpro-field-data-types"></a>Tipi di dati dei campi Visual FoxPro
Nella tabella seguente sono elencati i valori per l'argomento *FieldType* in alter table e create table e viene indicato se sono necessari gli argomenti *nFieldWidth* e *nPrecision* .  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descrizione|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|DOUBLE|  
|C|N|-|Campo carattere della larghezza *n*|  
|D|-|-|Data|  
|F|N|d|Campo numerico a virgola mobile con larghezza *n* con *d* posizioni decimali|  
|G|-|-|Generale|  
|I|-|-|Integer|  
|L|-|-|Logico|  
|M|-|-|Memo|  
|N|N|d|Campo numerico della larghezza *n* con *d* posizioni decimali|  
|T|-|-|Datetime|  
|S|-|-|Valuta|
