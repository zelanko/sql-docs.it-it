---
title: SQLExecute | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ac50a5abd1f7e87017c6f0c559887b1796032328
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706128"
---
# <a name="sqlexecute"></a>SQLExecute
  Se l'attributo Statement SQL_SOPT_SS_PARAM_FOCUS non è impostato su 0, SQLExecute restituirà SQL_ERROR e genererà un record di diagnostica con SQLSTATE = HY024 e il messaggio "valore attributo non valido, SQL_SOPT_SS_PARAM_FOCUS (deve essere zero in fase di esecuzione)". Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
## <a name="remarks"></a>Commenti  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLExecute](https://go.microsoft.com/fwlink/?LinkId=80708)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
