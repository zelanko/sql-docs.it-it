---
title: Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (RDS) | Microsoft Docs
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
ms.openlocfilehash: 8e99ff17cad2bebcfaed509788ea3721ddfeb0ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963881"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-rds"></a>Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (Servizi Desktop remoto)
Passa al record primo, ultimo, successivo o precedente in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) specificato.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.Recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto [. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
## <a name="remarks"></a>Osservazioni  
 È possibile utilizzare i metodi **Move** con **RDS. Oggetto DataControl** per spostarsi tra i record di dati nei controlli associati a dati in una pagina Web. Si supponga, ad esempio, di visualizzare un **Recordset** in una griglia mediante l'associazione a un **RDS. Oggetto DataControl** . È quindi possibile includere i pulsanti primo, ultimo, successivo e precedente su cui gli utenti possono fare clic per passare al record primo, ultimo, successivo o precedente nel **Recordset**visualizzato. A tale scopo, chiamare i metodi **MoveFirst**, **MoveLast**, **MoveNext**e **MovePrevious** del Servizi Desktop remoto **. Oggetto DataControl** nelle procedure OnClick rispettivamente per i pulsanti First, Last, Next e Previous. Nell' [esempio](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md) di Rubrica viene illustrato come eseguire questa operazione.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Metodo MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)


