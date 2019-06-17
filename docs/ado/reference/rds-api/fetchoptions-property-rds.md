---
title: Proprietà FetchOptions (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FetchOptions property [ADO]
ms.assetid: 7b2e254a-9354-4541-bc98-bb185276388f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a85f6938ec0f97ff69eab1782c0a24b78a5a6e8b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712686"
---
# <a name="fetchoptions-property-rds"></a>Proprietà FetchOptions (Servizi Desktop remoto)
Indica il tipo di recupero asincrono.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="setting-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce uno dei valori seguenti.  
  
|Costante|Descrizione|  
|--------------|-----------------|  
|**adcFetchUpFront**|Tutti i record della [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) vengono recuperati prima che il controllo venga restituito all'applicazione. L'intero **Recordset** viene recuperato prima che l'applicazione può eseguire alcuna operazione con esso.|  
|**adcFetchBackground**|Controllo può restituire all'applicazione, non appena il primo batch di record è stato recuperato. Una lettura successiva del **Recordset** che tenta di accedere a un record non recuperato nel primo batch verrà ritardata fino al recupero record ricercato è in realtà, a ogni controllo viene restituito all'applicazione.|  
|**adcFetchAsync**|Valore predefinito. Il controllo ritorna immediatamente all'applicazione mentre vengono recuperati i record in background. Se l'applicazione tenta di leggere un record che non è ancora stato recuperato, verrà letto il record più vicino a quello cercato e controllo restituirà immediatamente, che indica che alla fine corrente del **Recordset** è stato raggiunto. Ad esempio, una chiamata a [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) sposterà la posizione corrente all'ultimo record effettivamente recuperate, anche se più record continuerà popolare le **Recordset**.|  
  
> [!NOTE]
>  Ogni file eseguibile dal lato client che usa le costanti debba fornire le relative dichiarazioni. È possibile tagliare e incollare le dichiarazioni costante desiderati dal file Adcvbs. Inc, che si trova nella cartella di installazione predefinito per la libreria di servizi desktop remoto.  
  
## <a name="remarks"></a>Note  
 In un'applicazione Web, è possibile usare **adcFetchAsync** (valore predefinito), poiché garantisce prestazioni migliori. In un'applicazione client compilata, è possibile usare **il valore adcFetchBackground**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà ExecuteOptions e FetchOptions (esempio di proprietà (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Metodo Cancel (Servizi Desktop remoto)](../../../ado/reference/rds-api/cancel-method-rds.md)


