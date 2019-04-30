---
title: Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- MoveLast method [RDS]
- MovePrevious method [RDS]
- MoveFirst method [RDS]
- MoveNext method [RDS]
ms.assetid: 45c80bb5-136f-4204-9df2-78740fa55574
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3afc55ca26a8462eb5662287288ee885f9104a8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225827"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (Servizi Desktop remoto)
Sposta il primo, ultimo, successivo o precedente record in un oggetto specificato [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
## <a name="remarks"></a>Note  
 È possibile usare la **spostare** metodi con il **Servizi Desktop remoto. DataControl** oggetto per spostarsi tra i record dei dati nei controlli con associazione a dati in una pagina Web. Ad esempio, si supponga di visualizzare una **Recordset** in una griglia utilizzando l'associazione a un **Servizi Desktop remoto. DataControl** oggetto. È possibile includere First, Last, Next e Previous pulsanti che gli utenti possono spostarsi al primo, ultimo, successivo, o record precedente visualizzati **Recordset**. Eseguire questa operazione chiamando il **MoveFirst**, **MoveLast**, **MoveNext**, e **MovePrevious** metodi del **Servizi Desktop remoto. DataControl** oggetto nelle procedure onClick per i pulsanti First, Last, Avanti e indietro, rispettivamente. Il [esempio Address Book](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) viene illustrato come eseguire questa operazione.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Metodo MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


