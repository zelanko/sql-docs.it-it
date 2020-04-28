---
title: Proprietà CommandTimeout (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7c8c6b10e63e4cacce0124eb11102db796168d9b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919705"
---
# <a name="commandtimeout-property-ado"></a>Proprietà CommandTimeout (ADO)
Indica il tempo di attesa durante l'esecuzione di un comando prima di terminare il tentativo e generare un errore.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **Long** che indica, in secondi, il tempo di attesa per l'esecuzione di un comando. L'impostazione predefinita è 30.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **CommandTimeout** per un oggetto [connessione](../../../ado/reference/ado-api/connection-object-ado.md) o un oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) per consentire l'annullamento di una chiamata al metodo [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) , a causa di ritardi dal traffico di rete o da un utilizzo eccessivo del server. Se l'intervallo impostato nella proprietà **CommandTimeout** scade prima del completamento dell'esecuzione del comando, si verifica un errore e ADO Annulla il comando. Se si imposta la proprietà su zero, ADO resterà in attesa per un periodo di tempo indefinito fino al completamento dell'esecuzione. Verificare che il provider e l'origine dati in cui si scrive il codice supportino la funzionalità **CommandTimeout** .  
  
 L'impostazione **CommandTimeout** per un oggetto **Connection** non ha alcun effetto sull'impostazione **CommandTimeout** per un oggetto **Command** nella stessa **connessione**. ovvero la proprietà **CommandTimeout** dell'oggetto **comando** non eredita il valore del valore **CommandTimeout** dell'oggetto **connessione** .  
  
 In un oggetto **Connection** la proprietà **CommandTimeout** rimane in lettura/scrittura dopo l'apertura della **connessione** .  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Esempio di proprietà ActiveConnection, CommandText, CommandTimeout, CommandType, Size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Proprietà ConnectionTimeout (ADO)](../../../ado/reference/ado-api/connectiontimeout-property-ado.md)
