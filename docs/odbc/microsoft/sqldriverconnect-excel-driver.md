---
description: SQLDriverConnect (driver Excel)
title: SQLDriverConnect (driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6320033d83e9b46c3567b3bf0b845144dbe9250e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449193"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Le parole chiave seguenti sono supportate nella stringa di connessione per tutti i driver: **DSN**, **DBQ**e **fil**.  
  
 Nella tabella seguente vengono illustrate le parole chiave minime necessarie per connettersi a ogni driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori di DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Se DBQ o DefaultDir non è specificato per il driver Microsoft Excel 3,0 o 4,0, il driver si connetterà alla directory corrente.  
  
|Driver|Parole chiave obbligatorie|Esempi|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3,0 o 4,0|Driver, DriverID|Driver = {driver Microsoft Excel (*. xls)}; DBQ = c:\Temp; DriverID = 278|  
|Microsoft Excel 5.0/7.0|Driver, DriverID, DBQ|Driver = {driver Microsoft Excel (*. xls)}; DBQ =c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 e versioni successive|Driver, DriverID, DBQ|Driver = {driver Microsoft Excel (*. xls)}; DBQ =c:\temp\sample.xls; DriverID = 790|
