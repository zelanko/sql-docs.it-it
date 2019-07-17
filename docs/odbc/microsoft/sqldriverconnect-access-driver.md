---
title: SQLDriverConnect (Driver Access) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e211797147c4da8f197247244f6f2805185b3b0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053986"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** consente di connettersi a un driver senza creare un'origine dati (DSN).  
  
 Le parole chiave seguenti sono supportate nella stringa di connessione per tutti i driver: **DSN**, **DBQ**, e **FIL**.  
  
 Il **UID** e **PWD** sono supportate anche le parole chiave.  
  
 La parola chiave PWD non deve includere i caratteri speciali (vedere in SQL_SPECIAL_CHARACTERS **SQLGetInfo** restituiti valori).  
  
 Nella tabella seguente illustra le parole chiave minime necessarie per connettersi a tutti i driver e viene fornito un esempio di coppie parola chiave/valore utilizzate con **SQLDriverConnect**. Per un elenco completo dei valori DRIVERID, vedere [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).  
  
|Driver|Parole chiave necessarie|Esempi|  
|------------|-----------------------|--------------|  
|Microsoft Access|Driver, DBQ|Driver={Microsoft Access Driver (*.mdb)}; DBQ=c:\\\temp\\\sample.mdb|
