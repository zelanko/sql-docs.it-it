---
title: Proprietà SortColumn (Servizi Desktop remoto) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5a9c3f9f50968f3b5e8085052917397bcd90226
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963402"
---
# <a name="sortcolumn-property-rds"></a>Proprietà SortColumn (Servizi Desktop remoto)
Indica da quale colonna per ordinare i record.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Una variabile oggetto che rappresenta un [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *String*  
 Oggetto **stringa** valore che rappresenta il nome o alias della colonna in base al quale ordinare i record.  
  
## <a name="remarks"></a>Note  
 Il **SortColumn**, [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), e [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)le proprietà forniscono l'ordinamento e filtrare le funzionalità della cache lato client. La funzionalità di ordinamento Ordina i record per i valori da una colonna. La funzionalità di filtro consente di visualizzare un subset di record basata su criteri di ricerca, mentre la versione completa [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) viene mantenuto nella cache. Il [reimpostare](../../../ado/reference/rds-api/reset-method-rds.md) esegue i criteri e sostituire il metodo **Recordset** con un aggiornabile **Recordset**.  
  
 Per ordinare in un **Recordset**, è prima necessario salvare le modifiche in sospeso. Se si usa il **Servizi Desktop remoto. DataControl**, è possibile usare il [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) (metodo). Ad esempio, se il **Servizi Desktop remoto. DataControl** è denominato ADC1, il codice sarebbe `ADC1.SubmitChanges`. Se si usa un oggetto ADO **Recordset**, è possibile usare relativo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) (metodo). Usando **UpdateBatch** è il metodo consigliato per **Recordset** gli oggetti creati con il [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) (metodo). Ad esempio, il codice può essere `myRS.UpdateBatch` o `ADC1.Recordset.UpdateBatch`.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [FilterColumn, FilterCriterion, valore FilterValue, SortColumn e SortDirection Properties ed esempio di metodo Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Proprietà di ordinamento](../../../ado/reference/ado-api/sort-property.md)   
 [Proprietà SortDirection (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





