---
title: Livelli di isolamento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 319453b209f8d7306bee73c4492678e676e05441
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85658270"
---
# <a name="isolation-levels-ole-db"></a>Livelli di isolamento (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  I client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono controllare i livelli di isolamento delle transazioni per una connessione. Per controllare il livello di isolamento delle transazioni, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider OLE DB di Native Client USA:  
  
-   DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS proprietà per la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modalità autocommit predefinita del provider OLE DB di Native Client.  
  
     Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valore predefinito del provider OLE DB di Native Client per il livello è DBPROPVAL_TI_READCOMMITTED.  
  
-   Parametro *isoLevel* del metodo **ITransactionLocal::StartTransaction** per le transazioni locali di cui viene eseguito il commit manuale.  
  
-   Parametro *isoLevel* del metodo **ITransactionDispenser::BeginTransaction** per le transazioni distribuite coordinate da MS DTC.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente accesso di sola lettura nel livello di isolamento di lettura dirty. Tutti gli altri livelli limitano la concorrenza applicando blocchi agli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Poiché il client richiede livelli di concorrenza maggiori, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applica restrizioni superiori all'accesso simultaneo ai dati. Per mantenere il livello più elevato di accesso simultaneo ai dati, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumer del provider di OLE DB di Native client deve controllare in modo intelligente le richieste di livelli di concorrenza specifici.  
  
> [!NOTE]  
>  In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] è stato introdotto il livello di isolamento dello snapshot. Per altre informazioni, vedere [Uso dell'isolamento dello snapshot](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Transazioni](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
