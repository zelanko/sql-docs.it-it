---
title: Proprietà FilterCriterion (RDS) | Microsoft Docs
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
ms.openlocfilehash: e5b14e042c7566b6b6f8559e9dc371028a509979
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964062"
---
# <a name="filtercriterion-property-rds"></a>Proprietà FilterCriterion (Servizi Desktop remoto)
Indica l'operatore di valutazione da utilizzare nel valore del filtro.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parametri  
 *DataControl*  
 Variabile oggetto che rappresenta un Servizi Desktop remoto [. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *Stringa*  
 Valore **stringa** che specifica l'operatore di valutazione di [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) ai record. Può essere uno dei seguenti: <, \<=, >, >=, = o <>.  
  
## <a name="remarks"></a>Osservazioni  
 Le proprietà [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**e [FilterColumn offrono](../../../ado/reference/rds-api/filtercolumn-property-rds.md) forniscono funzionalità di ordinamento e filtro nella cache sul lato client. La funzionalità di ordinamento ordina i record in base ai valori di una colonna. La funzionalità di filtro Visualizza un subset di record in base ai criteri di ricerca, mentre il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) completo viene mantenuto nella cache. Il metodo [Reset](../../../ado/reference/rds-api/reset-method-rds.md) eseguirà i criteri e sostituirà il **Recordset** corrente con un **Recordset**aggiornabile.  
  
 L'operatore "! =" non è valido per **FilterCriterion**; usare invece "<>".  
  
 Se vengono impostate entrambe le proprietà Filter e Sort e si chiama il metodo **Reset** , il set di righe viene filtrato per la prima volta e quindi viene ordinato. Per gli ordinamenti ascendenti, i valori null si trovano nella parte superiore; per gli ordinamenti decrescenti, i valori null sono nella parte inferiore (l'ordine crescente è il comportamento predefinito).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà FilterColumn offrono, FilterCriterion, FilterValue, SortColumn e SortDirection e metodo Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Proprietà FilterColumn offrono (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Proprietà FilterValue (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Proprietà SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Proprietà SortDirection (Servizi Desktop remoto)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


