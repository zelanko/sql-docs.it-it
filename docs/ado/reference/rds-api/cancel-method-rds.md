---
description: Metodo Cancel (Servizi Desktop remoto)
title: Metodo Cancel (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: rothja
ms.author: jroth
ms.openlocfilehash: ade9d0092a5dbc0ebdaba0ae968d52b23c97ba27
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982782"
---
# <a name="cancel-method-rds"></a>Metodo Cancel (Servizi Desktop remoto)
Annulla l'esecuzione di una chiamata al metodo asincrona in sospeso.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
RDS.DataControl.Cancel  
```  
  
## <a name="remarks"></a>Osservazioni  
 Quando si chiama **Annulla**, [ReadyState](./readystate-property-rds.md) viene impostato automaticamente su **adcReadyStateLoaded**e il [Recordset](../ado-api/recordset-object-ado.md) sarà vuoto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Cancel (VBScript)](./cancel-method-example-vbscript.md)   
 [Metodo Cancel (ADO)](../ado-api/cancel-method-ado.md)   
 [Metodo CancelBatch (ADO)](../ado-api/cancelbatch-method-ado.md)   
 [Metodo CancelUpdate (ADO)](../ado-api/cancelupdate-method-ado.md)   
 [Metodo CancelUpdate (RDS)](./cancelupdate-method-rds.md)   
 [Proprietà ExecuteOptions (Servizi Desktop remoto)](./executeoptions-property-rds.md)