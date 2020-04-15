---
title: Proprietà SQLExecute . Documenti Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLExecute function
ms.assetid: 4d7db8b6-611f-4fe4-be85-2a407059de45
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8965ce25c009f50e1879084e2c61d66e21419698
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300293"
---
# <a name="sqlexecute"></a>SQLExecute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Se l'attributo dell'istruzione SQL_SOPT_SS_PARAM_FOCUS non è impostato su 0, SQLExecute restituirà SQL_ERROR e genererà un record di diagnostica con SQLSTATE-HY024 e il messaggio "Valore dell'attributo non valido, SQL_SOPT_SS_PARAM_FOCUS (deve essere zero in fase di esecuzione)". Per ulteriori informazioni su SQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
## <a name="remarks"></a>Osservazioni  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Sqlexecute](https://go.microsoft.com/fwlink/?LinkId=80708)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
