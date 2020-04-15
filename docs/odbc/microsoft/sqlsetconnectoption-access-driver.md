---
title: SQLSetConnectOption (Driver di accesso) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301534"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOpzione|Comment|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Il SQL_ACCESS_MODE fOption può essere impostato su SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Tuttavia, il driver non impedisce gli aggiornamenti se SQL_ACCESS_MODE è impostato su SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Quando viene utilizzato il driver di Microsoft Access, l'opzione SQL_AUTOCOMMIT può essere impostata su SQL_AUTOCOMMIT_ON o SQL_AUTOCOMMIT_OFF, poiché il driver di Microsoft Access supporta le transazioni[1].|  
|SQL_CURRENT_QUALIFIER|Supportato.|  
|SQL_LOGIN_TIMEOUT|Non supportato.|  
|SQL_OPT_TRACE|Supportato.|  
|SQL_OPT_TRACEFILE|Supportato.|  
|SQL_PACKET_SIZE|Non supportato.|  
|SQL_QUIET_MODE|Non supportato.|  
|SQL_TRANSLATE_DLL|Non supportato.|  
|SQL_TRANSLATION_OPTION|Non supportato.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION è sempre SQL_TXN_READ_COMMITTED.|  
  
 [1] Le transazioni atomiche non sono supportate dal driver Microsoft Access. Quando si esegue il commit di una transazione utilizzando il driver di Microsoft Access, si verifica un ritardo finito tra il momento in cui viene eseguito il commit della transazione e il momento in cui i valori vengono scritti su disco. Questo ritardo è determinato da un ritardo inerente al motore Microsoft Jet. Il timeout della pagina non sarà inferiore a un valore minimo, anche se l'opzione PageTimeout è impostata al di sotto di tale valore. Di conseguenza, non vi è alcuna garanzia che i dati di cui è stato eseguito il commit siano stabili, poiché le modifiche possono essere apportate durante il ritardo.
