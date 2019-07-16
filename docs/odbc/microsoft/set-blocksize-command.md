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
ms.openlocfilehash: 4fe84a470f5e877c73701168394cd85d75253fb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997755"
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
