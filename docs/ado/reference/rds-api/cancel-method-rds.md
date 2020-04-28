---
title: Metodo Cancel (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Cancel method [RDS]
ms.assetid: 560b5b3d-fba9-4275-8920-9c3e186134f7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90d3e60a77df15d1b2db302df8a3c1d4a39de245
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964612"
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
 Quando si chiama **Annulla**, [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) viene impostato automaticamente su **adcReadyStateLoaded**e il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sarà vuoto.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Cancel (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Metodo Cancel (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Metodo CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Proprietà ExecuteOptions (Servizi Desktop remoto)](../../../ado/reference/rds-api/executeoptions-property-rds.md)


