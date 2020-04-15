---
title: Comando SET UNIQUE Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
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
 Specifica che qualsiasi record con un valore di chiave di indice duplicato non deve essere incluso nel file di indice. Nel file di indice viene incluso solo il primo record con il valore della chiave di indice originale.  
  
 OFF  
 (Impostazione predefinita.) Specifica che i record con valori di chiave di indice duplicati devono essere inclusi nel file di indice.  
  
## <a name="remarks"></a>Osservazioni  
 Un file di indice mantiene l'impostazione SET UNIQUE quando si rilascia REINDEX. Per ulteriori informazioni, vedere [INDEX](../../odbc/microsoft/index-command.md).
