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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fcfbbdb1881662401e791ea197115120444cf855
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225533"
---
# <a name="bcpcolumns"></a>bcp_columns
  Imposta il numero totale di colonne individuate nel file utente da utilizzare con una copia bulk all'interno o all'esterno di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [bcp_setbulkmode](bcp-setbulkmode.md) può essere usato invece bcp_columns e [bcp_colfmt](bcp-colfmt.md).  
  
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
 Numero totale di colonne nel file utente. Anche se ci si prepara a copia bulk di dati dal file utente a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella e non si intende copiare tutte le colonne nel file utente, è necessario impostare ancora *nColumns* al numero totale di colonne del file utente.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Note  
 Questa funzione può essere chiamata solo dopo aver [bcp_init](bcp-init.md) è stato chiamato con un nome file valido.  
  
 È consigliabile chiamare questa funzione solo se si intende utilizzare un formato di file utente diverso da quello predefinito. Per altre informazioni su una descrizione del formato di file utente predefinito, vedere **bcp_init**.  
  
 Dopo avere chiamato `bcp_columns`, è necessario chiamare [bcp_colfmt](bcp-colfmt.md)per ogni colonna nel file utente per definire completamente un formato di file personalizzato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
