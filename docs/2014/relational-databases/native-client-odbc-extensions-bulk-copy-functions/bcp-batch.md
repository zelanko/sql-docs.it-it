---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_batch
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c41e8d90adc8ff6eb2058feebe3f33c10edbfa92
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62631385"
---
# <a name="bcpbatch"></a>bcp_batch
  Esegue il commit di tutte le righe precedentemente bulk copiato dalle variabili di programma e inviate a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dal [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *hdbc*  
 Handle di connessione ODBC abilitato per la copia bulk.  
  
## <a name="returns"></a>Valori di codice restituiti  
 Il numero di righe salvato dopo l'ultima chiamata a **bcp_batch**, oppure -1 in caso di errore.  
  
## <a name="remarks"></a>Note  
 I batch della copia bulk definiscono le transazioni. Quando un'applicazione usa [bcp_bind](bcp-bind.md) e **bcp_sendrow** per copia bulk di righe dalle variabili di programma alle tabelle di SQL Server, le righe vengono eseguito il commit solo quando il programma chiama **bcp_batch** oppure [bcp_done](bcp-done.md).  
  
 È possibile chiamare **bcp_batch** una volta ogni *n* righe o quando c'è una pausa nei dati in entrata (come in un'applicazione telemetrica). Se un'applicazione non chiama **bcp_batch** le righe della copia bulk vengono eseguito il commit solo quando **bcp_done** viene chiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
