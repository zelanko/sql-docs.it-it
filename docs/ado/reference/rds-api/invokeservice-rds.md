---
title: InvokeService (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- InvokeService [RDS]
ms.assetid: ad45c676-ec7e-4a3a-9a6b-a54f75eb3012
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efcb67792eed98caebd541ab7dab3a3fef4cd626
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63308769"
---
# <a name="invokeservice-rds"></a>InvokeService (Servizi Desktop remoto)
Restituisce un puntatore all'interfaccia richiesta in una versione più con supporta dell'oggetto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parametri  
 *riid*  
  
 [in] L'identificatore dell'interfaccia richiesto.  
  
 *punkNotSoFunctionalInterface*  
  
 [in] Oggetto di origine meno efficienti.  
  
 *ppunkMoreFunctionalInterface*  
  
 [out] L'indirizzo della variabile puntatore che riceve il puntatore a interfaccia richiesto *riid*. Dopo la restituzione ha esito positivo, il *ppunkMoreFunctionalInterface* parametro contiene il puntatore all'interfaccia richiesta per l'oggetto. Se l'oggetto non supporta l'interfaccia specificata nella *riid*, *ppunkMoreFunctionalInterface* è impostato su NULL.  
  
## <a name="return-value"></a>Valore restituito  
 Valore HRESULT che indica se la chiamata per il **InvokeService** metodo è stato completato.  
  
## <a name="remarks"></a>Note  
 L'implementazione di motore del cursore di servizi desktop remoto del **InvokeService** accetta il set di righe di input (o più risultati object), consente di popolare il motore del cursore dal set di righe di input e quindi restituisce un puntatore in se stesso.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia IRDSService (Servizi Desktop remoto)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Servizi Desktop remoto](../../../ado/reference/rds-api/rds-methods.md)


