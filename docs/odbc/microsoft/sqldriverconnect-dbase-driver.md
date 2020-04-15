---
title: SQLDriverConnect (driver dBASE) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39d3d062ef8371ce37f812216cbb642d103eff98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302922"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Nella stringa di connessione sono supportate le seguenti parole chiave per tutti i driver: **DSN**, **DBQ**e **FIL**.  
  
 Quando viene utilizzato il driver Paradox, dopo che un file protetto da password è stato aperto da un utente, altri utenti non sono autorizzati ad aprire lo stesso file.  
  
 Nella tabella seguente vengono illustrate le parole chiave minime necessarie per connettersi a ogni driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).  
  
> [!NOTE]  
>  Se DBQ o DefaultDir non è specificato per dBASEdriver, il driver si connetterà alla directory corrente.  
  
|Driver|Parole chiave richieste|Esempi|  
|------------|-----------------------|--------------|  
|Dbase|Driver, DriverID|Driver: Driver dBASE Microsoft (con estensione dbf); DBQ: c:. ID del driver 277|
