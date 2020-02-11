---
title: Utilizzo dell'isolamento dello snapshot | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], snapshot isolation
- SQLNCLI, snapshot isolation
- isolation levels [SQL Server], snapshot
- DBPROPSET_SESSION property set
- DBDROPSET_DATASOURCEINFO property set
- snapshot isolation [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, snapshot isolation
- SQL Server Native Client ODBC driver, snapshot isolation
- SQL Server Native Client, snapshot isolation
- SQLGetInfo function
- concurrency [SQL Server Native Client]
- SQLSetConnectAttr function
ms.assetid: 39e87eb1-677e-45dd-bc61-83a4025a7756
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcf2003873de6f6ca15fed4d0818337ce4920906
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63205861"
---
# <a name="working-with-snapshot-isolation"></a>Utilizzo dell'isolamento dello snapshot
  In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] è stato introdotto un nuovo livello di isolamento dello "snapshot" destinato a migliorare la concorrenza delle applicazioni per l'elaborazione delle transazioni online (OLTP). Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la concorrenza è basata esclusivamente sul blocco. Questa caratteristica può causare problemi di blocco e deadlock per alcune applicazioni. L'isolamento dello snapshot dipende dai miglioramenti apportati al controllo delle versioni delle righe e ha lo scopo di migliorare le prestazioni evitando scenari di blocco in lettura/scrittura.  
  
 Le transazioni avviate con l'isolamento dello snapshot leggono uno snapshot del database che risale all'avvio della transazione. Uno dei possibili risultati è che, se aperti nel contesto di una transazione snapshot, i cursori server keyset statici e dinamici si comporteranno come cursori statici aperti in transazioni serializzabili. Tuttavia, quando i cursori vengono aperti con il livello di isolamento dello snapshot, non vengono acquisiti blocchi. In questo modo viene ridotto il numero di blocchi nel server.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provider OLE DB di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native client include miglioramenti che sfruttano l'isolamento dello snapshot introdotto [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]in. Tra questi miglioramenti figurano le modifiche ai set di proprietà DBPROPSET_DATASOURCEINFO e DBPROPSET_SESSION.  
  
### <a name="dbpropset_datasourceinfo"></a>DBPROPSET_DATASOURCEINFO  
 Il set di proprietà DBPROPSET_DATASOURCEINFO è stato modificato per indicare che il livello di isolamento dello snapshot è supportato dall'aggiunta del valore DBPROPVAL_TI_SNAPSHOT utilizzato nella proprietà DBPROP_SUPPORTEDTXNISOLEVELS. Questo nuovo valore indica che il livello di isolamento dello snapshot è supportato indipendentemente dall'abilitazione del controllo delle versioni nel database. Di seguito viene presentato un elenco dei valori DBPROP_SUPPORTEDTXNISOLEVELS:  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_SUPPORTEDTXNISOLEVELS|Tipo: VT_I4<br /><br /> L/S: Sola lettura<br /><br /> Descrizione: maschera di bit che specifica i livelli di isolamento delle transazioni supportati. Combinazione di zero o più dei valori seguenti:<br /><br /> -DBPROPVAL_TI_CHAOS<br />-DBPROPVAL_TI_READUNCOMMITTED<br />-DBPROPVAL_TI_BROWSE<br />-DBPROPVAL_TI_CURSORSTABILITY<br />-DBPROPVAL_TI_READCOMMITTED<br />-DBPROPVAL_TI_REPEATABLEREAD<br />-DBPROPVAL_TI_SERIALIZABLE<br />-DBPROPVAL_TI_ISOLATED<br />-DBPROPVAL_TI_SNAPSHOT|  
  
### <a name="dbpropset_session"></a>DBPROPSET_SESSION  
 Il set di proprietà DBPROPSET_SESSION è stato modificato per indicare che il livello di isolamento dello snapshot è supportato dall'aggiunta del valore DBPROPVAL_TI_SNAPSHOT utilizzato nella proprietà DBPROP_SESS_AUTOCOMMITISOLEVELS. Questo nuovo valore indica che il livello di isolamento dello snapshot è supportato indipendentemente dall'abilitazione del controllo delle versioni nel database. Di seguito viene presentato un elenco dei valori DBPROP_SESS_AUTOCOMMITISOLEVELS:  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Tipo: VT_I4<br /><br /> L/S: Sola lettura<br /><br /> Descrizione: specifica una maschera di bit che indica il livello di isolamento delle transazioni durante la modalità di autocommit. I valori che è possibile impostare in questa maschera di bit sono uguali a quelli che è possibile impostare per DBPROP_SUPPORTEDTXNISOLEVELS.|  
  
> [!NOTE]  
>  Si verifica l'errore DB_S_ERRORSOCCURRED o DB_E_ERRORSOCCURRED se DBPROPVAL_TI_SNAPSHOT viene impostato quando si utilizzano versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Per informazioni sul modo in cui l'isolamento dello snapshot è supportato nelle transazioni, vedere [Supporting local Transactions](../../native-client-ole-db-transactions/transactions.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client fornisce supporto per l'isolamento dello snapshot, sebbene siano stati apportati miglioramenti alle funzioni [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) .  
  
### <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 La funzione **SQLSetConnectAttr** supporta ora l'utilizzo dell'attributo SQL_COPT_SS_TXN_ISOLATION. Impostando SQL_COPT_SS_TXN_ISOLATION su SQL_TXN_SS_SNAPSHOT si indica che la transazione si verificherà con il livello di isolamento dello snapshot.  
  
### <a name="sqlgetinfo"></a>SQLGetInfo  
 La funzione [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) supporta ora il valore SQL_TXN_SS_SNAPSHOT aggiunto al tipo di informazioni di SQL_TXN_ISOLATION_OPTION.  
  
 Per informazioni sul supporto dell'isolamento dello snapshot nelle transazioni, vedere [livello di isolamento delle transazioni del cursore](../../native-client-odbc-cursors/properties/cursor-transaction-isolation-level.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)   
 [Proprietà e comportamenti dei set di righe](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
  
