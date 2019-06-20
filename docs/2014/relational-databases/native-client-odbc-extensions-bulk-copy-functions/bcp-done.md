---
title: bcp_done | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0326330e3d2052e8e997a293f666a8fc725391b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62689073"
---
# <a name="bcpdone"></a>bcp_done
  Termina una copia bulk dalle variabili di programma a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguita con [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Il numero di righe salvato in modo permanente dopo l'ultima chiamata a [bcp_batch](bcp-batch.md) oppure -1 in caso di errore.  
  
## <a name="remarks"></a>Note  
 Chiamare **bcp_done** dopo l'ultima chiamata a [bcp_sendrow](bcp-sendrow.md) oppure [bcp_moretext](bcp-moretext.md). Errore durante la chiamata **bcp_done** dopo aver copiato tutti i dati degli errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
