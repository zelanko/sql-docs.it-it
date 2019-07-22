---
title: Informazioni nelle interfacce di errore | Microsoft Docs
description: Le informazioni nelle interfacce di errore
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4ff18864e37575f78d129abb1569b0ffe83d4685
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994938"
---
# <a name="information-in-error-interfaces"></a>Informazioni nelle interfacce di errore
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il driver OLE DB per SQL Server segnala informazioni sullo stato e sugli errori nelle interfacce di errore definite da OLE DB **IErrorInfo**, **IErrorRecords** e **ISQLErrorInfo**.  
  
 Il driver OLE DB per SQL Server supporta le funzioni membro **IErrorInfo** come indicato di seguito.  
  
|Funzione membro|Descrizione|  
|---------------------|-----------------|  
|**GetDescription**|Stringa descrittiva del messaggio di errore.|  
|**GetGUID**|GUID dell'interfaccia che ha definito l'errore.|  
|**GetHelpContext**|Non supportato. Restituisce sempre zero.|  
|**GetHelpFile**|Non supportato. Viene restituito sempre NULL.|  
|**GetSource**|Stringa "Microsoft OLE DB Driver per SQL Server".|  
  
 Il driver OLE DB per SQL Server supporta le funzioni membro **IErrorRecords** disponibili per gli utenti, come indicato di seguito.  
  
|Funzione membro|Descrizione|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Inserisce in una struttura ERRORINFO le informazioni di base su un errore. Una struttura ERRORINFO contiene membri che identificano il valore restituito HRESULT per l'errore nonché il provider e l'interfaccia alle quali si applica l'errore.|  
|**GetCustomErrorObject**|Restituisce un riferimento nelle interfacce **ISQLErrorInfo** e [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Restituisce un riferimento in un'interfaccia **IErrorInfo**.|  
|**GetErrorParameters**|Il driver OLE DB per SQL Server non restituisce parametri al consumer tramite **GetErrorParameters**.|  
|**GetRecordCount**|Conteggio dei record di errore disponibili.|  
  
 Il driver OLE DB per SQL Server supporta i parametri **ISQLErrorInfo:: GetSQLInfo** come indicato di seguito.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*pbstrSQLState*|Restituisce un valore SQLSTATE per l'errore. I valori SQLSTATE vengono definiti nelle specifiche API, SQL-92, ODBC e ISO SQL. Né [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] né il driver OLE DB per SQL Server valori SQLSTATE specifici dell'implementazione definiti.|  
|*plNativeError*|Restituisce il numero di errore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da **master.dbo.sysmessages**, quando disponibile. Gli errori nativi sono disponibili dopo un tentativo riuscito di inizializzare un driver OLE DB per SQL Server origine dati. Prima del tentativo, il driver OLE DB per SQL Server restituisce sempre zero.|  
  
## <a name="see-also"></a>Vedere anche  
 [errori](../../oledb/ole-db-errors/errors.md)  
  
  
