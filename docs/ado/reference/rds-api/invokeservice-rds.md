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
ms.openlocfilehash: 86ebb27ebdc5de5a045304afe45cd8653e491827
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963866"
---
# <a name="invokeservice-rds"></a>InvokeService (Servizi Desktop remoto)
Restituisce un puntatore all'interfaccia richiesta su una versione più idonea dell'oggetto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.InvokeService(REFID riid, IUknown* punkNotSoFunctionalInterface, IUknown** ppunkMoreFunctionalInterface) As HRESULT  
```  
  
#### <a name="parameters"></a>Parametri  
 *riid*  
  
 in Identificatore dell'interfaccia richiesta.  
  
 *punkNotSoFunctionalInterface*  
  
 in Oggetto di origine meno idoneo.  
  
 *ppunkMoreFunctionalInterface*  
  
 out Indirizzo della variabile puntatore che riceve il puntatore a interfaccia richiesto in *riid*. In caso di esito positivo, il parametro *ppunkMoreFunctionalInterface* contiene il puntatore a interfaccia richiesto per l'oggetto. Se l'oggetto non supporta l'interfaccia specificata in *riid*, *ppunkMoreFunctionalInterface* è impostato su null.  
  
## <a name="return-value"></a>Valore restituito  
 Valore HRESULT che indica se la chiamata al metodo **InvokeService** è stata eseguita correttamente.  
  
## <a name="remarks"></a>Osservazioni  
 L'implementazione del motore di cursori RDS di **InvokeService** accetta il set di righe di input (o più oggetti risultati), popola il motore di cursori dal set di righe di input e quindi restituisce un puntatore su se stesso.  
  
## <a name="applies-to"></a>Si applica a  
 [Interfaccia IRDSService (Servizi Desktop remoto)](../../../ado/reference/rds-api/irdsservice-interface-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi di Servizi Desktop remoto](../../../ado/reference/rds-api/rds-methods.md)


