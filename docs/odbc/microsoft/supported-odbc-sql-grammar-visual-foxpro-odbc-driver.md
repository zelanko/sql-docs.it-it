---
title: Grammatica SQL ODBC supportata (driver ODBC di Visual FoxPro) . Documenti Microsoft
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
ms.openlocfilehash: f72548d0708a63f887f7d6da4d4f5988500f0eef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304084"
---
# <a name="supported-odbc-sql-grammar-visual-foxpro-odbc-driver"></a>Grammatica SQL ODBC supportata (driver ODBC Visual FoxPro)
Il driver ODBC di Microsoft Visual FoxPro supporta quanto segue:  
  
-   Tutte le istruzioni e le clausole SQL nella grammatica SQL minima ODBC  
  
-   Un'istruzione SQL aggiuntiva dalla grammatica SQL di base di ODBCAn additional SQL statement from the ODBC core SQL grammar  
  
 Nella tabella seguente sono elencati gli elementi supportati dal driver, dal livello di grammatica SQL ODBC.  
  
|Level|Elementi|Elemento|  
|-----------|--------------|----------|  
|Minima|Data Definition Language (DDL)|CREATE TABLE e DROP TABLE|  
||Data Manipulation Language (DML)|SELECT, INSERT, UPDATE e DELETE|  
||Espressioni|Semplice (ad esempio A>B|  
||Tipi di dati|CHAR, VARCHAR o LONG VARCHAR|  
  
 Oltre alla grammatica SQL ODBC supportata, il driver ODBC di Visual FoxPro supporta la sintassi completa del linguaggio Visual FoxPro nativo per i seguenti comandi di Visual FoxPro:  
  
 [ALTER A TABELLA](../../odbc/microsoft/alter-table-sql-command.md)  
  
 [CREA TABELLA](../../odbc/microsoft/create-table-sql-command.md)  
  
 [Elimina](../../odbc/microsoft/delete-sql-command.md)  
  
 [ELIMINA TAG](../../odbc/microsoft/delete-tag-command.md)  
  
 [TABELLA DI RILASCIO](../../odbc/microsoft/drop-table-command.md)  
  
 [Indice](../../odbc/microsoft/index-command.md)  
  
 [Inserire](../../odbc/microsoft/insert-sql-command.md)  
  
 [Selezionare](../../odbc/microsoft/select-sql-command.md)  
  
 [Aggiornamento](../../odbc/microsoft/update-sql-command.md)
