---
description: bcp_done
title: bcp_done | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_done
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aace849b761ee4842ed60db055bd8bba198dc45f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460796"
---
# <a name="bcp_done"></a>bcp_done
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Termina una copia bulk dalle variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguite con [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBINT bcp_done (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Restituisce  
 Il numero di righe salvate in modo permanente dopo l'ultima chiamata a [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) o-1 in caso di errore.  
  
## <a name="remarks"></a>Osservazioni  
 Chiamare **bcp_done** dopo l'ultima chiamata a [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) o [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md). La mancata chiamata di **bcp_done** dopo la copia di tutti i dati genera errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
