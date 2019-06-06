---
title: Proprietà IsolationLevel | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9e027e325ec27bf5a80cf4df85afcfe59656ce3c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697591"
---
# <a name="isolationlevel-property"></a>Proprietà IsolationLevel
Indica il livello di isolamento per una [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un [IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md) valore. Il valore predefinito è **adXactReadCommitted**.  
  
## <a name="remarks"></a>Note  
 Usare la **IsolationLevel** per impostare l'isolamento a livello di un **connessione** oggetto. L'impostazione ha effetto fino al successivo si chiama il [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) (metodo). Se il livello di isolamento richiesto non è disponibile, il provider può restituire il successivo livello più alto di isolamento senza aggiornare il **IsolationLevel** proprietà.  
  
 Il **IsolationLevel** è di lettura/scrittura.  
  
> [!NOTE]
>  **Utilizzo del servizio dati remoto** quando viene usato in un client-side **Connection** oggetto, il **IsolationLevel** proprietà può essere impostata solo su **adXactUnspecified**. Poiché gli utenti stanno lavorando con disconnessa **Recordset** gli oggetti in una cache lato client, è possibile riscontrare problemi. Ad esempio, quando due utenti diversi tentano di aggiornare il record stesso, il servizio dati remoto semplicemente consente all'utente che ha aggiornato il record prima di tutto "win". La seconda richiesta dell'utente update avrà esito negativo con un errore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio IsolationLevel e modalità proprietà (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Esempio IsolationLevel e modalità proprietà (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
