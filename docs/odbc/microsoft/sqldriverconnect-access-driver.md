---
title: SQLDriverConnect (driver Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a679cbb16ece3f239b1d17daabc8a294b808287
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302912"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Le parole chiave seguenti sono supportate nella stringa di connessione per tutti i driver: **DSN**, **DBQ**e **fil**.  
  
 Sono supportate anche le parole chiave **UID** e **pwd** .  
  
 La parola chiave PWD non deve includere alcun carattere speciale (vedere SQL_SPECIAL_CHARACTERS nei valori restituiti da **SQLGetInfo** ).  
  
 Nella tabella seguente vengono illustrate le parole chiave minime necessarie per connettersi a ogni driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori di DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).  
  
|Driver|Parole chiave obbligatorie|Esempi|  
|------------|-----------------------|--------------|  
|Microsoft Access|Driver, DBQ|Driver = {driver Microsoft Access (*. mdb)}; DBQ = c:\\\Temp\\\sample.mdb|
