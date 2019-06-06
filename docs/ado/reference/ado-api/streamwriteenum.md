---
title: StreamWriteEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamWriteEnum
helpviewer_keywords:
- StreamWriteEnum enumeration [ADO]
ms.assetid: bdbf3405-a0bd-4f02-85d4-e3fe8da3f3f7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f34ff1bba827678273590fdc1b39a001b5931644
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710822"
---
# <a name="streamwriteenum"></a>StreamWriteEnum
Specifica se un separatore di riga viene aggiunto alla stringa di cui è scritto in un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adWriteChar**|0|Valore predefinito. Scrive la stringa di testo specificato (specificato dal *Data* parametro) per il **Stream** oggetto.|  
|**adWriteLine**|1|Scrive una stringa di testo e un carattere separatore di riga a un **Stream** oggetto. Se il [LineSeparator](../../../ado/reference/ado-api/lineseparator-property-ado.md) proprietà non è definita, quindi viene restituito un errore di run-time.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Queste costanti non dispongono di equivalenti di ADO o WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo WriteText](../../../ado/reference/ado-api/writetext-method.md)
