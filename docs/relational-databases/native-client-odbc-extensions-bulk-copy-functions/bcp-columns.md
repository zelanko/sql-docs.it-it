---
title: bcp_columns | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_columns
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 904353ca9b5ff6c23ea463d1333ed13499b6c341
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707706"
---
# <a name="bcp_columns"></a>bcp_columns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Imposta il numero totale di colonne individuate nel file utente da utilizzare con una copia bulk all'interno o all'esterno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. è possibile usare [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) invece di bcp_columns e [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_columns (  
        HDBC hdbc,  
        INT nColumns);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *nColumns*  
 Numero totale di colonne nel file utente. Anche se si prepara la copia bulk di dati dal file utente a una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non si intende copiare tutte le colonne nel file utente, è comunque necessario impostare *nColumns sul* sul numero totale di colonne del file utente.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Questa funzione può essere chiamata solo dopo la chiamata di [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) con un nome file valido.  
  
 È consigliabile chiamare questa funzione solo se si intende utilizzare un formato di file utente diverso da quello predefinito. Per ulteriori informazioni su una descrizione del formato di file utente predefinito, vedere **bcp_init**.  
  
 Dopo la chiamata a **bcp_columns**, è necessario chiamare [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) per ogni colonna del file utente per definire completamente un formato di file personalizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
