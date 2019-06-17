---
title: SET BLOCKSIZE (comando) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e904d341513047b3940cf5b3fc2ba9538cdb5c8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127849"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE (comando)
Specifica la modalità di allocazione di spazio su disco per l'archiviazione dei campi di tipo memo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argomenti  
 *nBytes*  
 Specifica la dimensione del blocco in cui è allocato spazio su disco per i campi di tipo memo. Se *nBytes* è 0, spazio su disco viene allocato in byte singoli (blocchi di 1 byte). Se *nBytes* è un numero intero compreso tra 1 e 32, spazio su disco allocato nei blocchi di *nBytes* moltiplicato per 512 byte. Se *nBytes* è maggiore di 32, in blocchi di cui è allocato spazio su disco *nBytes* byte. Se si specifica un valore di dimensioni di blocco maggiore di 32, è possibile risparmiare spazio su disco considerevole.  
  
## <a name="remarks"></a>Note  
 Il valore predefinito per impostare dimensioni del blocco è 64. Per reimpostare la dimensione del blocco su un valore diverso dopo aver creato il file, impostarlo su un nuovo valore e quindi usare copia per creare una nuova tabella. La nuova tabella ha le dimensioni del blocco specificato.
