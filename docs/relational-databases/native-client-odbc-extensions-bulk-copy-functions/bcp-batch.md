---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_batch
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c6f6899186b328afb8aa7da7c87aaceed10c6637
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62738617"
---
# <a name="bcpbatch"></a>bcp_batch
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Esegue il commit di tutte le righe precedentemente bulk copiato dalle variabili di programma e inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBINT bcp_batch (HDBC  
        hdbc);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Il numero di righe salvato dopo l'ultima chiamata a **bcp_batch**, oppure -1 in caso di errore.  
  
## <a name="remarks"></a>Note  
 I batch della copia bulk definiscono le transazioni. Quando un'applicazione usa [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) e **bcp_sendrow** per copia bulk di righe dalle variabili di programma alle tabelle di SQL Server, le righe vengono eseguito il commit solo quando il programma chiama **bcp_batch** oppure [bcp_done](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-done.md).  
  
 È possibile chiamare **bcp_batch** una volta ogni *n* righe o quando c'è una pausa nei dati in entrata (come in un'applicazione telemetrica). Se un'applicazione non chiama **bcp_batch** le righe della copia bulk vengono eseguito il commit solo quando **bcp_done** viene chiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
