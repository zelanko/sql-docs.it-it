---
title: Proprietà FilterValue (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1e45986cdd44d0ab9bffc1ea11fe1a9ced350e3c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712620"
---
# <a name="filtervalue-property-rds"></a>Proprietà FilterValue (Servizi Desktop remoto)
Indica il valore con cui si desidera filtrare i record.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *String*  
 Oggetto **stringa** valore che rappresenta un valore di dati con il quale filtrare i record (ad esempio `'Programmer'` o `125`).  
  
## <a name="remarks"></a>Note  
 Il [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), **FilterValue**, [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), e [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)le proprietà forniscono l'ordinamento e filtrare le funzionalità della cache lato client. La funzionalità di ordinamento Ordina i record per i valori da una colonna. La funzionalità di filtro consente di visualizzare un subset di record basata su criteri di ricerca, mentre la versione completa [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) viene mantenuto nella cache. Il [reimpostare](../../../ado/reference/rds-api/reset-method-rds.md) esegue i criteri e sostituire il metodo **Recordset** con un aggiornabile **Recordset**.  
  
 I valori null generano un errore di mancata corrispondenza di tipo.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [FilterColumn, FilterCriterion, valore FilterValue, SortColumn e SortDirection Properties ed esempio di metodo Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Proprietà FilterColumn (Servizi Desktop remoto)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Proprietà FilterCriterion (Servizi Desktop remoto)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [Proprietà SortColumn (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Proprietà SortDirection (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortdirection-property-rds.md)






















