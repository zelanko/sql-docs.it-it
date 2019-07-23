---
title: Dettagli errore SQL Server | Microsoft Docs
description: Dettagli relativi agli errori SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ddc9a1b1a242f9a92b1e854520d16abeb7baf809
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015656"
---
# <a name="sql-server-error-detail"></a>Dettagli relativi agli errori SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il driver OLE DB per SQL Server definisce l'interfaccia di errore specifica del provider [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1). L'interfaccia restituisce maggiori dettagli relativi agli errori [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e risulta molto utile quando operazioni di esecuzione di comandi o del set di righe non riescono.  
  
 È possibile accedere all'interfaccia **ISQLServerErrorInfo** in due modi.  
  
 Il consumer può chiamare **IErrorRecords::GetCustomerErrorObject** per ottenere un puntatore **ISQLServerErrorInfo**, come indicato nell'esempio di codice seguente. Non è necessario ottenere **ISQLErrorInfo.** Sia **ISQLErrorInfo** sia **ISQLServerErrorInfo** sono oggetti errore OLE DB personalizzati, in cui **ISQLServerErrorInfo** rappresenta l'interfaccia da usare per ottenere informazioni sugli errori del server, inclusi dettagli quali i numeri di riga e il nome di procedura.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Un altro modo per ottenere un puntatore **ISQLServerErrorInfo** consiste nel chiamare il metodo **QueryInterface** su un puntatore **ISQLErrorInfo** già ottenuto. Dal momento che **ISQLServerErrorInfo** contiene un superset delle informazioni disponibili in **ISQLErrorInfo**, è consigliabile accedere direttamente a **ISQLServerErrorInfo** mediante **GetCustomerErrorObject**.  
  
 L'interfaccia **ISQLServerErrorInfo** espone una funzione membro, [ISQLServerErrorInfo::GetErrorInfo](../../oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). La funzione restituisce un puntatore a una struttura SSERRORINFO e un puntatore a un buffer di stringhe. Entrambi i puntatori fanno riferimento a una memoria che il consumer deve deallocare usando il metodo **IMalloc::Free**.  
  
 I membri di struttura SSERRORINFO vengono interpretati dal consumer come segue.  
  
|Membro|Descrizione|  
|------------|-----------------|  
|*pwszMessage*|Messaggio di errore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Identico alla stringa restituita in **IErrorInfo::GetDescription**.|  
|*pwszServer*|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per la sessione.|  
|*pwszProcedure*|Se appropriato, restituisce il nome della stored procedure in cui ha avuto origine l'errore. In caso contrario, una stringa vuota.|  
|*lNative*|Numero di errore nativo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Identico al valore restituito nel parametro *plNativeError* di **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|Stato di un messaggio di errore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravità di un messaggio di errore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando è applicabile, restituisce il numero di riga di una stored procedure in cui si è verificato l'errore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Errori](../../oledb/ole-db-errors/errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  
