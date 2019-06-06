---
title: Proprietà ConnectionTimeout (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 594c96d73302b907f5bc9b2167f69c8b33047aab
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698641"
---
# <a name="connectiontimeout-property-ado"></a>Proprietà ConnectionTimeout (ADO)
Indica per quanto tempo di attesa durante il tentativo di stabilire una connessione prima di terminare il tentativo e generare un errore.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **lungo** valore che indica, in secondi, quanto tempo di attesa per la connessione da aprire. Valore predefinito è 15.  
  
## <a name="remarks"></a>Note  
 Usare la **ConnectionTimeout** proprietà in un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) se ritardi di rete del traffico o con intensa attività di server rendono necessario interrompere un tentativo di connessione dell'oggetto. Se l'ora dal **ConnectionTimeout** l'impostazione della proprietà deve trascorrere prima dell'apertura della connessione, si verifica un errore e ADO non annullerà il tentativo. Se si imposta la proprietà su zero, ADO attenderà all'infinito finché non viene aperta la connessione. Assicurarsi che il provider a cui si sta scrivendo codice supporta il **ConnectionTimeout** funzionalità.  
  
 Il **ConnectionTimeout** è di lettura/scrittura quando la connessione è chiusa e di sola lettura quando è aperto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [ConnectionString, ConnectionTimeout ed esempio di proprietà State (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Esempio ConnectionString, ConnectionTimeout e proprietà State (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Proprietà CommandTimeout (ADO)](../../../ado/reference/ado-api/commandtimeout-property-ado.md)
