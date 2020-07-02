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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b54af78e0156e85c872f5f487e06ef76b64a98d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789243"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta aggiornamento a catena ed esegue l'eliminazione tramite il meccanismo dei vincoli della chiave esterna. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce SQL_CASCADE per le colonne UPDATE_RULE e/o DELETE_RULE se l'opzione CASCADE viene specificata sulla clausola ON UPDATE e/o ON DELETE dei vincoli FOREIGN KEY. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce SQL_NO_ACTION per le colonne UPDATE_RULE e/o DELETE_RULE se l'opzione NO ACTION viene specificata sulla clausola ON UPDATE e/o ON DELETE dei vincoli FOREIGN KEY.  
  
 Quando sono presenti valori non validi in un parametro **SQLForeignKeys** , **SQLForeignKeys** restituisce SQL_SUCCESS in fase di esecuzione. **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLForeignKeys** può essere eseguito su un cursore del server statico. Il tentativo di eseguire **SQLForeignKeys** su un cursore aggiornabile (dinamico o keyset) restituisce SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per i parametri *FKCatalogName* e *PKCatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLForeignKeys (funzione)](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
