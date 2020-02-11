---
title: Comando SET BLOCKSIZE | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997755"
---
# <a name="set-blocksize-command"></a>SET BLOCKSIZE (comando)
Specifica la modalità di allocazione dello spazio su disco per l'archiviazione dei campi di memo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argomenti  
 *nBytes*  
 Specifica la dimensione del blocco in cui è allocato lo spazio su disco per i campi Memo. Se *nBytes* è 0, lo spazio su disco viene allocato in byte singoli (blocchi di 1 byte). Se *nBytes* è un numero intero compreso tra 1 e 32, lo spazio su disco viene allocato in blocchi di byte *nBytes* moltiplicato per 512. Se *nBytes* è maggiore di 32, lo spazio su disco viene allocato in blocchi di *nBytes* byte. Se si specifica un valore di dimensione blocco maggiore di 32, è possibile risparmiare spazio su disco sostanziale.  
  
## <a name="remarks"></a>Osservazioni  
 Il valore predefinito per SET BLOCKSIZE è 64. Per reimpostare la dimensione del blocco su un valore diverso dopo che il file è stato creato, impostarlo su un nuovo valore e quindi usare COPY per creare una nuova tabella. La nuova tabella presenta le dimensioni del blocco specificate.
