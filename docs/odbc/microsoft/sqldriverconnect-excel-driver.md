---
title: SQLDriverConnect (driver di Excel) Documenti Microsoft
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
ms.openlocfilehash: 1108206bf38183887540b114fda5a1e913aa67d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307122"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel.This topic provides Excel Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Nella stringa di connessione sono supportate le seguenti parole chiave per tutti i driver: **DSN**, **DBQ**e **FIL**.  
  
 Nella tabella seguente vengono illustrate le parole chiave minime necessarie per connettersi a ogni driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Se DBQ o DefaultDir non è specificato per il driver di Microsoft Excel 3.0 o 4.0, il driver si connetterà alla directory corrente.  
  
|Driver|Parole chiave richieste|Esempi|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 o 4.0|Driver, DriverID|Driver , Driver di Microsoft Excel (con estensione xls) e driver di Microsoft Excel . DBQ: c:. ID del conducente 278|  
|Microsoft Excel 5.0/7.0|Driver, DriverID, DBQ|Driver , Driver di Microsoft Excel (con estensione xls) e driver di Microsoft Excel . DBQ: c: temp sample.xls; ID del driver 22|  
|Microsoft Excel 97 e versioni successive|Driver, DriverID, DBQ|Driver , Driver di Microsoft Excel (con estensione xls) e driver di Microsoft Excel . DBQ: c: temp sample.xls; ID del conducente: 790|
