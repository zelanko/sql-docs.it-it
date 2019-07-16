---
title: SQLSetConnectOption (Driver Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bea124a78e2a180180c59de3577fe1db7637e110
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897790"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Commento|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Il fOption SQL_ACCESS_MODE può essere impostato su SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Tuttavia, il driver non impedisce gli aggiornamenti se SQL_ACCESS_MODE è impostato su SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Quando viene usato il driver Microsoft Access, l'opzione SQL_AUTOCOMMIT può essere impostata su SQL_AUTOCOMMIT_ON o SQL_AUTOCOMMIT_OFF, perché il driver Microsoft Access supporta le transazioni [1].|  
|SQL_CURRENT_QUALIFIER|Supportato.|  
|SQL_LOGIN_TIMEOUT|Non supportati.|  
|SQL_OPT_TRACE|Supportato.|  
|SQL_OPT_TRACEFILE|Supportato.|  
|SQL_PACKET_SIZE|Non supportati.|  
|SQL_QUIET_MODE|Non supportati.|  
|SQL_TRANSLATE_DLL|Non supportati.|  
|SQL_TRANSLATION_OPTION|Non supportati.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION è sempre SQL_TXN_READ_COMMITTED.|  
  
 [1] transazioni atomiche non sono supportate dal driver Microsoft Access. Quando si esegue il commit di una transazione che utilizza il driver Microsoft Access, esiste un ritardo finito tra il momento in cui viene eseguito il commit della transazione e l'ora i valori vengono scritti su disco. Questo ritardo è determinato da un ritardo intrinseco nella gestione di Microsoft Jet. Il timeout della pagina non sarà inferiore a un valore minimo, anche se è impostata l'opzione PageTimeout sotto tale valore. Di conseguenza, vi è alcuna garanzia che il commit dei dati non è stabile, poiché è possibile apportare modifiche durante il ritardo.
