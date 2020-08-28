---
description: Proprietà ConnectionTimeout (ADO)
title: Proprietà ConnectionTimeout (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: rothja
ms.author: jroth
ms.openlocfilehash: bd8fd11c017583ef49981021688210245589e971
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974742"
---
# <a name="connectiontimeout-property-ado"></a>Proprietà ConnectionTimeout (ADO)
Indica il tempo di attesa durante il tentativo di stabilire una connessione prima di terminare il tentativo e generare un errore.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che indica, in secondi, il tempo di attesa per l'apertura della connessione. L'impostazione predefinita è 15.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **ConnectionTimeout** su un oggetto [Connection](./connection-object-ado.md) se i ritardi dal traffico di rete o da un utilizzo eccessivo del server rendono necessario l'abbandono di un tentativo di connessione. Se il tempo trascorso dall'impostazione della proprietà **ConnectionTimeout** è scaduto prima dell'apertura della connessione, si verifica un errore e ADO Annulla il tentativo. Se si imposta la proprietà su zero, ADO attenderà un tempo illimitato fino a quando non verrà aperta la connessione. Verificare che il provider a cui si sta scrivendo il codice supporti la funzionalità **ConnectionTimeout** .  
  
 La proprietà **ConnectionTimeout** è in lettura/scrittura quando la connessione è chiusa e in sola lettura quando è aperta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ConnectionString, ConnectionTimeout e state (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Esempio di proprietà ConnectionString, ConnectionTimeout e state (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Proprietà CommandTimeout (ADO)](./commandtimeout-property-ado.md)