---
title: SQLDriverConnect (driver file di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9343361e7ad6fbfdf68b82218a39a56fa8d928e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053908"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Le parole chiave seguenti sono supportate nella stringa di connessione per tutti i driver: **DSN**, **DBQ**e **fil**.  
  
 Nella tabella seguente vengono illustrate le parole chiave minime necessarie per connettersi a ogni driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori di DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Se DBQ o DefaultDir non è specificato per il driver di testo, il driver si connetterà alla directory corrente.  
  
|Driver|Parole chiave obbligatorie|Esempi|  
|------------|-----------------------|--------------|  
|Text|Driver|Driver = {Microsoft Text driver (*. txt;\*. CSV)}; DefaultDir = c:\Temp|
