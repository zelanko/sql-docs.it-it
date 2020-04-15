---
title: Comando SET BLOCKSI-E Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eb9fbe9df90f7ddafebc6baa029164a578a6da3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300901"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE (comando)
Specifica la modalità di allocazione dello spazio su disco per l'archiviazione dei campi memo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argomenti  
 *nByte*  
 Specifica la dimensione del blocco in cui viene allocato lo spazio su disco per i campi memo. Se *nBytes* è 0, lo spazio su disco viene allocato in byte singoli (blocchi di 1 byte). Se *nBytes* è un numero intero compreso tra 1 e 32, lo spazio su disco viene allocato in blocchi di *nByte* byte moltiplicati per 512. Se *nBytes* è maggiore di 32, lo spazio su disco viene allocato in blocchi di *nBytes* byte. Se si specifica un valore di dimensione del blocco maggiore di 32, è possibile risparmiare spazio su disco considerevole.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore di default per SET BLOCKSIE è 64. Per reimpostare la dimensione del blocco su un valore diverso dopo la creazione del file, impostarlo su un nuovo valore e quindi utilizzare COPY per creare una nuova tabella. La nuova tabella ha la dimensione del blocco specificata.
