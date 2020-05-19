---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c55af9d21c669bd452de2bac9db56d158febc449
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704806"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters** espone il supporto per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML e i tipi definiti dall'utente (UDT). Si tratta di un'interfaccia facoltativa che eredita dall'interfaccia di base OLE DB **ICommandWithParameters**. Oltre ai tre metodi ereditati da **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**e **separameterinfo**; In **ISSCommandWithParameters** sono disponibili due nuovi metodi utilizzati per gestire i tipi di dati specifici del server.  
  
> [!NOTE]  
>  L'interfaccia **ISSCommandWithParameters** può essere utilizzata quando si utilizzano i componenti del servizio, ma i componenti del servizio non utilizzeranno questa interfaccia.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|Restituisce una struttura del set di proprietà **SSPARAMPROPS** della matrice per ogni parametro XML o tipo definito dall'utente passato al comando. Per gli altri tipi di parametro non ne restituisce nessuna.|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|Imposta le proprietà per i singoli parametri in base al numero ordinale oppure imposta proprietà dei parametri bulk specificando una matrice di strutture **SSPARAMPROPS**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Utilizzo di tipi di dati XML](../native-client/features/using-xml-data-types.md)   
 [Utilizzo dei tipi definiti dall'utente (UDT)](../native-client/features/using-user-defined-types.md)  
  
  
