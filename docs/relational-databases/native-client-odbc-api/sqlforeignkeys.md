---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d59eb895b735771a94fa04745b492fc68eb2ea74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63014511"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta aggiornamento a catena ed esegue l'eliminazione tramite il meccanismo dei vincoli della chiave esterna. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce SQL_CASCADE per le colonne UPDATE_RULE e/o DELETE_RULE se l'opzione CASCADE viene specificata sulla clausola ON UPDATE e/o ON DELETE dei vincoli FOREIGN KEY. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce SQL_NO_ACTION per le colonne UPDATE_RULE e/o DELETE_RULE se l'opzione NO ACTION viene specificata sulla clausola ON UPDATE e/o ON DELETE dei vincoli FOREIGN KEY.  
  
 Quando sono presenti in uno dei valori non validi **SQLForeignKeys** parametro **SQLForeignKeys** restituisce SQL_SUCCESS durante l'esecuzione. **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLForeignKeys** può essere eseguito su un cursore server statico. Un tentativo di eseguire **SQLForeignKeys** su un cursore aggiornabile (dinamico o keyset) restituisce SQL_SUCCESS_WITH_INFO, che indica che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta la segnalazione di informazioni relative alle tabelle sui server collegati mediante l'accettazione di un nome in due parti per il *FKCatalogName* e *PKCatalogName* parametri: *Linked_server_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLForeignKeys](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
