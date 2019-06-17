---
title: ISSCommandWithParameters (OLE DB) | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de7c6a99afcbd7db7c6e233fb737f129b536b8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209762"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters** espone il supporto per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML e tipi definiti dall'utente (UDT). Si tratta di un'interfaccia facoltativa che eredita dall'interfaccia OLE DB core **ICommandWithParameters**. Oltre ai tre metodi ereditati da **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, e **la funzione SetParameterInfo**; **ISSCommandWithParameters** fornisce due nuovi metodi che vengono utilizzati per gestire server specifici tipi di dati.  
  
> [!NOTE]  
>  Il **ISSCommandWithParameters** interfaccia può essere utilizzata quando vengono utilizzati i componenti del servizio, ma i componenti dei servizi stessi non utilizzerà questa interfaccia.  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[ISSCommandWithParameters::GetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|Restituisce una struttura del set di proprietà **SSPARAMPROPS** della matrice per ogni parametro XML o tipo definito dall'utente passato al comando. Per gli altri tipi di parametro non ne restituisce nessuna.|  
|[ISSCommandWithParameters::SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|Imposta le proprietà per i singoli parametri in base al numero ordinale oppure imposta proprietà dei parametri bulk specificando una matrice di strutture **SSPARAMPROPS**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Le interfacce &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Uso di tipi di dati XML](../native-client/features/using-xml-data-types.md)   
 [Uso dei tipi definiti dall'utente](../native-client/features/using-user-defined-types.md)  
  
  
