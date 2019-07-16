---
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 28d16d1ef5e63ee48d2e2251f5661437883c4324
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895638"
---
# <a name="bcpdone"></a>bcp_done
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Termina una copia bulk dalle variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguita con [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBINT bcp_done (  
    HDBC hdbc);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Il numero di righe salvato in modo permanente dopo l'ultima chiamata a [bcp_batch](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md) oppure -1 in caso di errore.  
  
## <a name="remarks"></a>Note  
 Chiamare **bcp_done** dopo l'ultima chiamata a [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) oppure [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md). Errore durante la chiamata **bcp_done** dopo aver copiato tutti i dati degli errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
