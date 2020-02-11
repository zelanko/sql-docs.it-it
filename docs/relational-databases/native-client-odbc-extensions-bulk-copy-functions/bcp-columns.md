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
ms.openlocfilehash: d26f288c857cf44a932a91b250074c36453e2482
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73782982"
---
# <a name="bcp_columns"></a>bcp_columns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Imposta il numero totale di colonne individuate nel file utente da utilizzare con una copia bulk all'interno o all'esterno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. è possibile utilizzare [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) al posto di bcp_columns e [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
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
 Numero totale di colonne nel file utente. Anche se si prepara la copia bulk di dati dal file utente a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella e non si intende copiare tutte le colonne nel file utente, è comunque necessario impostare *nColumns sul* sul numero totale di colonne del file utente.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione può essere chiamata solo dopo che [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) è stato chiamato con un nome file valido.  
  
 È consigliabile chiamare questa funzione solo se si intende utilizzare un formato di file utente diverso da quello predefinito. Per ulteriori informazioni su una descrizione del formato di file utente predefinito, vedere **bcp_init**.  
  
 Dopo la chiamata di **bcp_columns**, è necessario chiamare [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) per ogni colonna del file utente per definire completamente un formato di file personalizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
