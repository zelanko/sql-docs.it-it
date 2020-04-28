---
title: IMPOSTA comando univoco | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d3d37509450d1305891100b37bfd1ad026166e8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300841"
---
# <a name="set-unique-command"></a>SET UNIQUE (comando)
Specifica se i record con valori di chiave di indice duplicati vengono mantenuti in un file di indice.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Specifica che i record con un valore di chiave di indice duplicato non verranno inclusi nel file di indice. Nel file di indice è incluso solo il primo record con il valore di chiave di indice originale.  
  
 OFF  
 (Impostazione predefinita). Specifica che i record con valori di chiave di indice duplicati siano inclusi nel file di indice.  
  
## <a name="remarks"></a>Osservazioni  
 Un file di indice mantiene l'impostazione UNIVOCa impostata quando si rilascia REINDEX. Per ulteriori informazioni, vedere [index](../../odbc/microsoft/index-command.md).
