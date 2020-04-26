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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62631385"
---
# <a name="bcp_batch"></a>bcp_batch
  Esegue il commit di tutte le righe precedentemente copiate in massa dalle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] variabili di programma e inviate a da [bcp_sendrow](bcp-sendrow.md).  
  
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
 Numero di righe salvate dopo l'ultima chiamata a **bcp_batch**, oppure-1 in caso di errore.  
  
## <a name="remarks"></a>Osservazioni  
 I batch della copia bulk definiscono le transazioni. Quando un'applicazione utilizza [bcp_bind](bcp-bind.md) e **bcp_sendrow** per eseguire la copia bulk delle righe dalle variabili di programma alle tabelle SQL Server, viene eseguito il commit delle righe solo quando il programma chiama **bcp_batch** o [bcp_done](bcp-done.md).  
  
 È possibile chiamare **bcp_batch** una volta ogni *n* righe o quando si verifica una pausa nei dati in ingresso, come in un'applicazione di telemetria. Se un'applicazione non chiama **bcp_batch** viene eseguito il commit delle righe di cui è stata eseguita la copia bulk solo quando viene chiamato **bcp_done** .  
  
## <a name="see-also"></a>Vedi anche  
 [Funzioni di copia bulk](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
