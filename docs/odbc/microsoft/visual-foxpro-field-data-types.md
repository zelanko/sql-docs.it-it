---
description: Tipi di dati dei campi Visual FoxPro
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65410f16367af8764e8572c58e53831f3f7b9cda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449053"
---
# <a name="visual-foxpro-field-data-types"></a>Tipi di dati dei campi Visual FoxPro
Nella tabella seguente sono elencati i valori per l'argomento *FieldType* in alter table e create table e viene indicato se sono necessari gli argomenti *nFieldWidth* e *nPrecision* .  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descrizione|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|Double|  
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
