---
description: Proprietà Mode (ADO)
title: Proprietà Mode (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: rothja
ms.author: jroth
ms.openlocfilehash: 7fd002f54010a9bc8d5cf543fe1fd4521bc6d221
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443253"
---
# <a name="mode-property-ado"></a>Proprietà Mode (ADO)
Indica le autorizzazioni disponibili per la modifica dei dati in una [connessione](../../../ado/reference/ado-api/connection-object-ado.md), un [record](../../../ado/reference/ado-api/record-object-ado.md)o un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) . Il valore predefinito per una **connessione** è **adModeUnknown**. Il valore predefinito per un oggetto **record** è **adModeRead**. Il valore predefinito per un **flusso** associato a un'origine sottostante (aperto con un URL come origine o come **flusso** predefinito di un **record**) è **adModeRead**. Il valore predefinito per un **flusso** non associato a un'origine sottostante (di cui è stata creata un'istanza in memoria) è **adModeUnknown**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **mode** per impostare o restituire le autorizzazioni di accesso in uso da parte del provider nella connessione corrente. È possibile impostare la proprietà **mode** solo quando l'oggetto **connessione** è chiuso.  
  
 Per un oggetto **Stream** , se la modalità di accesso non è specificata, viene ereditata dall'origine utilizzata per aprire l'oggetto **flusso** . Se, ad esempio, un **flusso** viene aperto da un oggetto **record** , per impostazione predefinita viene aperto nella stessa modalità del **record**.  
  
 Questa proprietà è di lettura/scrittura mentre l'oggetto è chiuso e in sola lettura mentre l'oggetto è aperto.  
  
> [!NOTE]
>  **Utilizzo servizio dati remoto** Se utilizzata su un oggetto **connessione** lato client, la proprietà **mode** può essere impostata solo su **adModeUnknown**.  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà IsolationLevel e Mode (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Esempio di proprietà IsolationLevel e Mode (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
