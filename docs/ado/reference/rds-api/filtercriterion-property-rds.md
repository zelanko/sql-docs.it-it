---
title: Proprietà FilterCriterion (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 60f66b1ff2fa7ad7424342da6b92e7d44d0e6444
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712710"
---
# <a name="filtercriterion-property-rds"></a>Proprietà FilterCriterion (Servizi Desktop remoto)
Indica l'operatore di valutazione da utilizzare nel valore di filtro.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *String*  
 Oggetto **stringa** valore che specifica l'operatore di valutazione delle [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) ai record. I possibili valori sono i seguenti: <, \<=, >, > =, =, o <>.  
  
## <a name="remarks"></a>Note  
 Il [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**, e [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)le proprietà forniscono l'ordinamento e filtrare le funzionalità della cache lato client. La funzionalità di ordinamento Ordina i record per i valori da una colonna. La funzionalità di filtro consente di visualizzare un subset di record basata su criteri di ricerca, mentre la versione completa [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) viene mantenuto nella cache. Il [reimpostare](../../../ado/reference/rds-api/reset-method-rds.md) esegue i criteri e sostituire il metodo **Recordset** con un aggiornabile **Recordset**.  
  
 Il "! =" operatore non è valido per **FilterCriterion**; in alternativa, usare "<>".  
  
 Se il filtro e ordinamento vengono impostate e si chiama il **reimpostare** metodo, il set di righe viene innanzitutto filtrato e quindi eseguire l'ordinamento. Per ordinamenti crescenti, i valori null sono in alto. per ordinamenti decrescenti, i valori null sono nella parte inferiore (crescente è il comportamento predefinito).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [FilterColumn, FilterCriterion, valore FilterValue, SortColumn e SortDirection Properties ed esempio di metodo Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Proprietà FilterColumn (Servizi Desktop remoto)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Proprietà FilterValue (Servizi Desktop remoto)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Proprietà SortColumn (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Proprietà SortDirection (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


