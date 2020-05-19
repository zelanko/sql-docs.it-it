---
title: bcp_columns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_columns
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c0c48fa00e8bf3eadfa955876840bebf5b6816f5
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701996"
---
# <a name="bcp_columns"></a>bcp_columns
  Imposta il numero totale di colonne individuate nel file utente da utilizzare con una copia bulk all'interno o all'esterno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. è possibile utilizzare [bcp_setbulkmode](bcp-setbulkmode.md) al posto di bcp_columns e [bcp_colfmt](bcp-colfmt.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RETCODE bcp_columns (  
HDBC   
hdbc  
,  
INT   
nColumns  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
 *nColumns*  
 Numero totale di colonne nel file utente. Anche se si prepara la copia bulk di dati dal file utente a una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella e non si intende copiare tutte le colonne nel file utente, è comunque necessario impostare *nColumns sul* sul numero totale di colonne del file utente.  
  
## <a name="returns"></a>Restituisce  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Osservazioni  
 Questa funzione può essere chiamata solo dopo che [bcp_init](bcp-init.md) è stato chiamato con un nome file valido.  
  
 È consigliabile chiamare questa funzione solo se si intende utilizzare un formato di file utente diverso da quello predefinito. Per ulteriori informazioni su una descrizione del formato di file utente predefinito, vedere **bcp_init**.  
  
 Dopo aver chiamato `bcp_columns` , è necessario chiamare [bcp_colfmt](bcp-colfmt.md)per ogni colonna del file utente per definire completamente un formato di file personalizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
