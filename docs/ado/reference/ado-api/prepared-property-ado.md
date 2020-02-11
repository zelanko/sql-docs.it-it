---
title: Proprietà preparata (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee7a94a06aa574c84c01cb8b9d05ebfcdf327d44
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917592"
---
# <a name="prepared-property-ado"></a>Proprietà Prepared (ADO)
Indica se salvare una versione compilata di un [comando](../../../ado/reference/ado-api/command-object-ado.md) prima dell'esecuzione.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **booleano** che, se impostato su **true**, indica che il comando deve essere preparato.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **preparata** per fare in modo che il provider salvi una versione preparata (o compilata) della query specificata nella proprietà [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) prima della prima esecuzione di un oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) . Questo può rallentare la prima esecuzione di un comando, ma una volta che il provider compila un comando, il provider utilizzerà la versione compilata del comando per le esecuzioni successive, con conseguente miglioramento delle prestazioni.  
  
 Se la proprietà è **false**, il provider eseguirà direttamente l'oggetto **Command** senza creare una versione compilata.  
  
 Se il provider non supporta la preparazione dei comandi, può restituire un errore quando questa proprietà è impostata su **true**. Se il provider non restituisce un errore, ignora semplicemente la richiesta di preparazione del comando e imposta la proprietà **preparata** su **false**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà preparata (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Esempio della proprietà Prepared (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
