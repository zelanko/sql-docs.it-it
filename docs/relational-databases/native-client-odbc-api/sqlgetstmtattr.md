---
title: Proprietà SQLGetStmtAttr . Documenti Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetStmtAttr function
ms.assetid: e64f4f94-eb73-4477-9745-080b6cbdc751
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f59b7f006387beea3d213b7f120e567487232e69
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282054"
---
# <a name="sqlgetstmtattr"></a>SQLGetStmtAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client estende SQLGetStmtAttr per esporre gli attributi dell'istruzione specifica del driver.  
  
 [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) elenca gli attributi dell'istruzione che sono sia di lettura che di scrittura. In questo argomento vengono elencati gli attributi dell'istruzione di sola lettura.  
  
## <a name="sql_sopt_ss_current_command"></a>SQL_SOPT_SS_CURRENT_COMMAND  
 L'attributo SQL_SOPT_SS_CURRENT_COMMAND espone il comando corrente di un batch di comandi. Il valore restituito è un numero intero che specifica il percorso del comando nel batch. Il *ValuePtr* valore è di tipo SQLLEN.  
  
## <a name="sql_sopt_ss_nocount_status"></a>SQL_SOPT_SS_NOCOUNT_STATUS  
 L'attributo SQL_SOPT_SS_NOCOUNT_STATUS indica l'impostazione corrente dell'opzione NOCOUNT, che controlla se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] segnala se indica se viene chiamato il numero di righe interessate da un'istruzione quando [sqlRowCount.](../../relational-databases/native-client-odbc-api/sqlrowcount.md) Il *ValuePtr* valore è di tipo SQLLEN.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|SQL_NC_OFF|NOCOUNT è OFF. SQLRowCount restituisce il numero di righe interessate.|  
|SQL_NC_ON|NOCOUNT è ON. Il numero di righe interessate non viene restituito da SQLRowCount e il valore restituito è 0.|  
  
 Se SQLRowCount restituisce 0, l'applicazione deve eseguire il test SQL_SOPT_SS_NOCOUNT_STATUS. Se SQL_NC_ON viene restituito, il valore 0 da SQLRowCount indica solo che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non ha restituito un conteggio delle righe. Se viene restituito SQL_NC_OFF, NOCOUNT è disattivato e il valore 0 di SQLRowCount indica che l'istruzione non ha influito sulle righe.  
  
 Quando SQL_SOPT_SS_NOCOUNT_STATUS è SQL_NC_OFF, le applicazioni non dovrebbero visualizzare il valore di SQLRowCount. Le stored procedure o i batch di grandi dimensioni possono contenere più istruzioni SET NOCOUNT, pertanto non è possibile presupporre che SQL_SOPT_SS_NOCOUNT_STATUS rimanga costante. Questa opzione deve essere testata ogni volta che SQLRowCount restituisce 0.This option should be tested each time SQLRowCount returns 0.  
  
## <a name="sql_sopt_ss_querynotification_msgtext"></a>SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
 L'attributo SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT restituisce il testo del messaggio per la richiesta di notifica di query.  
  
## <a name="sqlgetstmtattr-and-table-valued-parameters"></a>SQLGetStmtAttr e parametri con valori di tabella  
 SQLGetStmtAttr può essere chiamato per ottenere il valore di SQL_SOPT_SS_PARAM_FOCUS nel descrittore di parametri dell'applicazione (APD) quando si utilizzano parametri con valori di tabella. Per ulteriori informazioni sullSQL_SOPT_SS_PARAM_FOCUS, vedere [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLSetStmtAttrSQLSetStmtAttr Function](https://go.microsoft.com/fwlink/?LinkId=59370)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
