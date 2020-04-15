---
title: SQLDriverConnect (driver Di Paradox) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68171cfab2b65634433b107d829dd2a6e9b5c985
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307112"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (driver Paradox)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver Paradox.This topic provides Paradox Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Nella stringa di connessione sono supportate le seguenti parole chiave per tutti i driver: **DSN**, **DBQ**e **FIL**.  
  
 È supportata anche la parola chiave **PWD.** La parola chiave PWD non deve includere alcuno dei caratteri speciali (vedere SQL_SPECIAL_CHARACTERS in **SQLGetInfo** Returned Values).  
  
 Dopo che un file protetto da password è stato aperto da un utente, ad altri utenti non è consentito aprire lo stesso file.  
  
 Nella tabella seguente vengono illustrate le parole chiave minime necessarie per connettersi a ogni driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Se DBQ o DefaultDir non è specificato per il driver Paradox, il driver si connetterà alla directory corrente.  
  
|Driver|Parole chiave richieste|Esempio|  
|------------|-----------------------|-------------|  
|Paradosso|Driver, DriverID|Driver: Driver Microsoft Paradox (con estensione db) ; DBQ : c: temp;IDDriver 26|
