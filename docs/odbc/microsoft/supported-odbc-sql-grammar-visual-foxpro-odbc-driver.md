---
description: Grammatica SQL ODBC supportata (driver ODBC Visual FoxPro)
title: Grammatica SQL ODBC supportata (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- native Visual FoxPro language syntax [ODBC]
- FoxPro ODBC driver [ODBC], SQL grammar
- SQL grammar [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], SQL grammar
- grammar support in Visual FoxPro ODBC driver [ODBC]
- Visual FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
- FoxPro ODBC driver [ODBC], native Visual FoxPro language syntax
ms.assetid: f41a38c2-e22e-4c65-a32e-9a6777435160
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3057520e5aca5277a68971513ef28427f27208ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471503"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Grammatica SQL ODBC supportata (driver ODBC Visual FoxPro)
Il driver ODBC di Microsoft Visual FoxPro supporta gli elementi seguenti:  
  
-   Tutte le istruzioni e le clausole SQL nella grammatica SQL minima ODBC  
  
-   Un'istruzione SQL aggiuntiva dalla grammatica SQL di ODBC Core  
  
 Nella tabella seguente sono elencati gli elementi supportati dal driver, dal livello di grammatica SQL ODBC.  
  
|Level|Elementi|Item|  
|-----------|--------------|----------|  
|Minima|Data Definition Language (DDL)|CREATE TABLE e DROP TABLE|  
||Data Manipulation Language (DML)|SELECT, INSERT, UPDATE e DELETE|  
||Espressioni|Semplice (ad esempio un>B + C)|  
||Tipi di dati|CHAR, VARCHAR o LONG VARCHAR|  
  
 Oltre alla grammatica SQL ODBC supportata, il driver ODBC Visual FoxPro supporta la sintassi nativa completa del linguaggio Visual FoxPro per i comandi Visual FoxPro seguenti:  
  
 [ALTER TABLE](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md)  
  
 [DELETE](../../odbc/microsoft/delete-sql-command.md)  
  
 [ELIMINA TAG](../../odbc/microsoft/delete-tag-command.md)  
  
 [DROP TABLE](../../odbc/microsoft/drop-table-command.md)  
  
 [Indice](../../odbc/microsoft/index-command.md)  
  
 [INSERT](../../odbc/microsoft/insert-sql-command.md)  
  
 [SELECT](../../odbc/microsoft/select-sql-command.md)  
  
 [UPDATE](../../odbc/microsoft/update-sql-command.md)
