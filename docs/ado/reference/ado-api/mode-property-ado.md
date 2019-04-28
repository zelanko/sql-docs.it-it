---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fc2a9dffe5dc22c1dadfa075b91d8a6b26215de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62863678"
---
# <a name="mode-property-ado"></a>Proprietà Mode (ADO)
Indica le autorizzazioni disponibili per la modifica dei dati in un [Connection](../../../ado/reference/ado-api/connection-object-ado.md), [Record](../../../ado/reference/ado-api/record-object-ado.md), o [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valore. Il valore predefinito per un **Connection** viene **adModeUnknown**. Il valore predefinito per un **Record** oggetto viene **adModeRead**. Il valore predefinito per un **Stream** associato a un'origine sottostante (aperta con un URL come origine o come valore predefinito **Stream** di un **Record**) viene  **adModeRead**. Il valore predefinito per un **Stream** non associato a un oggetto sottostante origine (creazione di un'istanza in memoria) sia **adModeUnknown**.  
  
## <a name="remarks"></a>Note  
 Usare la **modalità** proprietà per impostare o restituire le autorizzazioni di accesso utilizzato dal provider nella connessione corrente. È possibile impostare il **modalità** proprietà solo quando il **connessione** oggetto è chiuso.  
  
 Per un **Stream** dell'oggetto, se la modalità di accesso non è specificata, viene ereditato dall'origine consente di aprire le **Stream** oggetto. Ad esempio, se un **Stream** viene aperto da un **Record** oggetto, per impostazione predefinita è aperto nella stessa modalità del **Record**.  
  
 Questa proprietà è di lettura/scrittura mentre l'oggetto è chiuso e di sola lettura mentre l'oggetto è aperto.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Connection** oggetto, il **modalità** proprietà può essere impostata solo su **adModeUnknown**.  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio IsolationLevel e modalità proprietà (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Esempio IsolationLevel e modalità proprietà (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
