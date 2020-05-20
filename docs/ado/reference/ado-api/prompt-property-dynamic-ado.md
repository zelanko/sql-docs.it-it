---
title: Proprietà richiesta-dinamica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
author: rothja
ms.author: jroth
ms.openlocfilehash: e99273a94fc38779b50203d3dd5b78106f6a90c6
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761919"
---
# <a name="prompt-property-dynamic-ado"></a>Proprietà dinamica Prompt (ADO)
Specifica se il provider di OLE DB deve richiedere all'utente le informazioni di inizializzazione.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta e restituisce un valore [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 **Prompt** è una proprietà dinamica, che può essere aggiunta alla raccolta [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) dell'oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) dal provider OLE DB. Per richiedere informazioni di inizializzazione, OLE DB provider visualizzeranno in genere una finestra di dialogo per l'utente.  
  
 Le proprietà dinamiche di un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) vengono perse quando la **connessione** viene chiusa. È necessario reimpostare la proprietà **prompt** prima di aprire nuovamente la **connessione** per utilizzare un valore diverso da quello predefinito.  
  
> [!NOTE]
>  Non specificare che il provider deve richiedere all'utente in scenari in cui l'utente non sarà in grado di rispondere alla finestra di dialogo. Ad esempio, l'utente non sarà in grado di rispondere se l'applicazione è in esecuzione in un sistema server invece che nel client dell'utente oppure se l'applicazione è in esecuzione in un sistema senza utente connesso. In questi casi, l'applicazione attende indefinitamente una risposta e sembra bloccarsi.  
  
## <a name="usage"></a>Usage  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
