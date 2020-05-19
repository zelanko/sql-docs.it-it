---
title: Individuazione dei metadati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: ec3c0f4f-f838-43ce-85f2-cf2761e2aac5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 50455f67760c920881f9f8daaf42d7abe4037c45
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707285"
---
# <a name="metadata-discovery"></a>Individuazione dei metadati
  Il miglioramento dell'individuazione dei metadati in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] consente alle [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] applicazioni client native di garantire che i metadati delle colonne o dei parametri restituiti dall'esecuzione di una query siano identici o compatibili con il formato dei metadati specificato prima di eseguire la query. Se i metadati restituiti dopo l'esecuzione di una query non sono compatibili con il formato dei metadati specificato prima dell'esecuzione della query, viene generato un errore.  
  
 Nelle funzioni ODBC e bcp, nonché nelle interfacce IBCPSession e IBCPSession2, è ora possibile specificare una lettura ritardata (individuazione dei metadati ritardata) per evitare l'individuazione dei metadati per le operazioni di esportazione di query. In questo modo, è possibile migliorare le prestazioni ed eliminare gli errori di individuazione dei metadati.  
  
 Se si sviluppa un'applicazione utilizzando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] ma si esegue la connessione a una versione del server precedente a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] , la funzionalità di individuazione dei metadati corrisponderà alla versione del server.  
  
## <a name="remarks"></a>Commenti  
 Le funzioni bcp seguenti sono state migliorate in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] per garantire una migliore individuazione dei metadati:  
  
-   [bcp_columns](../../native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)  
  
-   [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)  
  
-   [bcp_getcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-getcolfmt.md)  
  
-   [bcp_readfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)  
  
-   [bcp_setcolfmt](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setcolfmt.md)  
  
 Si noterà anche un miglioramento delle prestazioni quando si specifica il formato dei metadati utilizzando [bcp_setbulkmode](../../native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md).  
  
 [bcp_control](../../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) dispone di un nuovo *eOption* per controllare il comportamento di bcp_readfmt: `BCPDELAYREADFMT` .  
  
 Le funzioni ODBC seguenti sono state migliorate in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] per garantire una migliore individuazione dei metadati:  
  
-   [SQLNumResultCols](../../native-client-odbc-api/sqlnumresultcols.md)  
  
-   [SQLDescribeCol](../../native-client-odbc-api/sqldescribecol.md)  
  
-   [SQLNumParams](../../native-client-odbc-api/sqlnumparams.md)  
  
-   [SQLDescribeParam](../../native-client-odbc-api/sqldescribeparam.md)  
  
 Le funzioni membro OLE DB seguenti sono state migliorate in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] per garantire una migliore individuazione dei metadati:  
  
-   IColumnsInfo::GetColumnInfo  
  
-   IColumnsRowset::GetColumnsRowset  
  
-   ICommandWithParameters:: GetParameterInfo (per altre informazioni, vedere [ICommandWithParameters](../../native-client-ole-db-interfaces/icommandwithparameters.md))  
  
 È inoltre possibile notare un miglioramento nelle prestazioni quando si specifica il formato dei metadati utilizzando IBCPSession::BCPSetBulkMode  
  
 L'individuazione dei metadati migliorata in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è possibile grazie all'aggiunta di due stored procedure in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   sp_describe_first_result_set  
  
-   sp_describe_undeclared_parameters  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)  
  
  
