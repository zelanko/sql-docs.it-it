---
title: Dettagli relativi agli errori di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d3d8c392312f98140f2a75becb175fab26c4e590
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704953"
---
# <a name="sql-server-error-detail"></a>Dettagli relativi agli errori SQL Server
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client definisce l'interfaccia di errore specifica del provider [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md). L'interfaccia restituisce maggiori dettagli relativi agli errori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e risulta molto utile quando operazioni di esecuzione di comandi o del set di righe non riescono.  
  
 È possibile accedere all'interfaccia **ISQLServerErrorInfo** in due modi.  
  
 Il consumer può chiamare **IErrorRecords::GetCustomerErrorObject** per ottenere un puntatore **ISQLServerErrorInfo**, come indicato nell'esempio di codice seguente. Non è necessario ottenere **ISQLErrorInfo.** Sia **ISQLErrorInfo** sia **ISQLServerErrorInfo** sono oggetti errore OLE DB personalizzati, in cui **ISQLServerErrorInfo** rappresenta l'interfaccia da usare per ottenere informazioni sugli errori del server, inclusi dettagli quali i numeri di riga e il nome di procedura.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Un altro modo per ottenere un puntatore **ISQLServerErrorInfo** consiste nel chiamare il metodo **QueryInterface** su un puntatore **ISQLErrorInfo** già ottenuto. Dal momento che **ISQLServerErrorInfo** contiene un superset delle informazioni disponibili in **ISQLErrorInfo**, è consigliabile accedere direttamente a **ISQLServerErrorInfo** mediante **GetCustomerErrorObject**.  
  
 L'interfaccia **ISQLServerErrorInfo** espone una funzione membro, [ISQLServerErrorInfo::GetErrorInfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). La funzione restituisce un puntatore a una struttura SSERRORINFO e un puntatore a un buffer di stringhe. Entrambi i puntatori fanno riferimento a una memoria che il consumer deve deallocare usando il metodo **IMalloc::Free**.  
  
 I membri di struttura SSERRORINFO vengono interpretati dal consumer come segue.  
  
|Membro|Description|  
|------------|-----------------|  
|*pwszMessage*|Messaggio di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Identico alla stringa restituita in **IErrorInfo::GetDescription**.|  
|*pwszServer*|Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la sessione.|  
|*pwszProcedure*|Se appropriato, restituisce il nome della stored procedure in cui ha avuto origine l'errore. In caso contrario, una stringa vuota.|  
|*lNative*|Numero di errore nativo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Identico al valore restituito nel parametro *plNativeError* di **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|Stato di un messaggio di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|Gravità di un messaggio di errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando è applicabile, restituisce il numero di riga di una stored procedure in cui si è verificato l'errore.|  
  
## <a name="see-also"></a>Vedere anche  
 [Errori](errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  
