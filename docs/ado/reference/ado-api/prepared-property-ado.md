---
title: Proprietà (ADO) preparato | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917592"
---
# <a name="prepared-property-ado"></a>Proprietà Prepared (ADO)
Indica se salvare una versione compilata di un [comando](../../../ado/reference/ado-api/command-object-ado.md) prima dell'esecuzione.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **booleana** valore che, se impostato su **True**, indica che il comando deve essere preparato.  
  
## <a name="remarks"></a>Note  
 Usare la **Prepared** per rendere il provider di salvare una versione preparata (o compilata) della query specificata nella proprietà di [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) proprietà prima di un [comando](../../../ado/reference/ado-api/command-object-ado.md) dell'oggetto prima esecuzione. Potrebbero risultare rallentate prima esecuzione del comando, ma una volta che il provider consente di compilare un comando, il provider Usa la versione compilata del comando per le esecuzioni successive, determinando un miglioramento delle prestazioni.  
  
 Se la proprietà **False**, il provider eseguirà il **comando** oggetti direttamente senza creare una versione compilata.  
  
 Se il provider non supporta la preparazione dei comandi, può restituire un errore quando questa proprietà è impostata su **True**. Se il provider non restituisce un errore, ignora semplicemente la richiesta per preparare il comando e imposta il **Prepared** proprietà **False**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Prepared (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Esempio di proprietà Prepared (VC++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
