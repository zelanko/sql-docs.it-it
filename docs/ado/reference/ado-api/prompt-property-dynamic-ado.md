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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cde7a5ad0324bc7d5cde5e1a794eeb9e2cb3381a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931588"
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
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
