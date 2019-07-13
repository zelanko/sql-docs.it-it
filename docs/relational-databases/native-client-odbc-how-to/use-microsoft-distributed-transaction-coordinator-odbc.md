---
title: Utilizzare Microsoft Distributed Transaction Coordinator (ODBC) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, using
ms.assetid: 12a275e1-8c7e-436d-8a4e-b7bee853b35c
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1305ba5412ba29f0ebf69b2480351674a68b37c
ms.sourcegitcommit: 636c02bd04f091ece934e78640b2363d88cac28d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860572"
---
# <a name="use-microsoft-distributed-transaction-coordinator-odbc"></a>Utilizzare Microsoft Distributed Transaction Coordinator (ODBC).
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-update-two-or-more-sql-servers-by-using-ms-dtc"></a>Per aggiornare due o più computer SQL Server mediante MS DTC  
  
1.  Connettersi a MS DTC utilizzando la funzione MS DTC OLE DtcGetTransactionManager. Per informazioni su MS DTC, vedere Microsoft Distributed Transaction Coordinator.  
  
2.  Chiamare SQL DriverConnect una volta per ogni connessione di SQL Server si desidera stabilire.  
  
3.  Chiamare la funzione MS DTC OLE ITransactionDispenser::BeginTransaction per iniziare una transazione MS DTC e ottenere un oggetto Transaction che rappresenta la transazione.  
  
4.  Chiamare [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) una o più volte per ogni connessione ODBC che si desidera integrare nella transazione MS DTC. Il secondo parametro [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) deve essere SQL_ATTR_ENLIST_IN_DTC mentre il terzo parametro deve essere l'oggetto Transaction, ottenuto nel passaggio 3.  
  
5.  Chiamare [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) una volta per ogni computer SQL Server da aggiornare.  
  
6.  Chiamare la funzione MS DTC OLE ITransaction::Commit per eseguire il commit della transazione MS DTC. L'oggetto Transaction non è più valido.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Per eseguire una serie di transazioni MS DTC, ripetere i passaggi da 3 a 6.  
  
 Per rilasciare il riferimento all'oggetto Transaction, chiamare la funzione MS DTC OLE ITransaction::Return.  
  
 Per usare una connessione ODBC con una transazione MS DTC e quindi usare la stessa connessione con una transazione di SQL Server locale, chiamare [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) con SQL_DTC_DONE.  
  
> [!NOTE]  
>  È inoltre possibile chiamare [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399) per ogni computer SQL Server anziché come suggerito nei passaggi 4 e 5.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di transazioni di &#40;ODBC&#41;](https://msdn.microsoft.com/library/f431191a-5762-4f0b-85bb-ac99aff29724)  
  
  
