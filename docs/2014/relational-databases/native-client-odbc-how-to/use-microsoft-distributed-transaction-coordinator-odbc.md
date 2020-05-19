---
title: Usare Microsoft Distributed Transaction Coordinator (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7e351dc2e9669fc47bc87a01c2882c0006401c5
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82711873"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Utilizzare Microsoft Distributed Transaction Coordinator (ODBC).
    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>Per aggiornare due o più computer SQL Server mediante MS DTC  
  
1.  Connettersi a MS DTC utilizzando la funzione MS DTC OLE DtcGetTransactionManager. Per informazioni su MS DTC, vedere Microsoft Distributed Transaction Coordinator.  
  
2.  Chiamare SQL DriverConnect una volta per ogni connessione Microsoft SQL Server che si desidera stabilire.  
  
3.  Chiamare la funzione MS DTC OLE ITransactionDispenser::BeginTransaction per iniziare una transazione MS DTC e ottenere un oggetto Transaction che rappresenta la transazione.  
  
4.  Chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) una o più volte per ogni connessione ODBC che si desidera integrare nella transazione MS DTC. Il secondo parametro [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) deve essere SQL_ATTR_ENLIST_IN_DTC mentre il terzo parametro deve essere l'oggetto Transaction, ottenuto nel passaggio 3.  
  
5.  Chiamare [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) una volta per ogni computer SQL Server da aggiornare.  
  
6.  Chiamare la funzione MS DTC OLE ITransaction::Commit per eseguire il commit della transazione MS DTC. L'oggetto Transaction non è più valido.  
  
 Per eseguire una serie di transazioni MS DTC, ripetere i passaggi da 3 a 6.  
  
 Per rilasciare il riferimento all'oggetto Transaction, chiamare la funzione MS DTC OLE ITransaction::Return.  
  
 Per usare una connessione ODBC con una transazione MS DTC e quindi usare la stessa connessione con una transazione di SQL Server locale, chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) con SQL_DTC_DONE.  
  
> [!NOTE]  
>  È inoltre possibile chiamare [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) e [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) per ogni computer SQL Server anziché come suggerito nei passaggi 4 e 5.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di transazioni &#40;ODBC&#41;](../../database-engine/dev-guide/performing-transactions-odbc.md)  
  
  
