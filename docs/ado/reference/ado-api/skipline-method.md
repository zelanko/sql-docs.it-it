---
description: Metodo SkipLine
title: Metodo SkipLine | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: rothja
ms.author: jroth
ms.openlocfilehash: c0897d90ffeccabbce57525f268214577a523d92
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777470"
---
# <a name="skipline-method"></a>Metodo SkipLine
Ignora un'intera riga durante la lettura di un [flusso](./stream-object-ado.md)di testo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>Osservazioni  
 Tutti i caratteri fino al separatore di riga successivo verranno ignorati. Per impostazione predefinita, [LineSeparator](./lineseparator-property-ado.md) è **adCRLF**. Se si tenta di saltare oltre [EOS](./eos-property.md), la posizione corrente rimarrà in **EOS**.  
  
 Il metodo **SkipLine** viene usato con i flussi di testo (il[tipo](./type-property-ado-stream.md) è **adTypeText**).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](./stream-object-ado.md)