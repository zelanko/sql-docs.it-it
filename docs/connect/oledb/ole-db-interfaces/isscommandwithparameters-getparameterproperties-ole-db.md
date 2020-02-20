---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
description: ISSCommandWithParameters::GetParameterProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4ed73892ae0ebe88d4b18f2d2114143423570c60
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015425"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Restituisce una matrice di strutture di set di proprietà SSPARAMPROPS, un set di proprietà SSPARAMPROPS per ogni tipo definito dall'utente o parametro XML.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT GetParameterProperties(  
      DB_UPARAMS *pcParams,  
      SSPARAMPROPS **prgParamProperties);  
```  
  
## <a name="arguments"></a>Argomenti  
 *pcParams*[out][in]  
 Puntatore alla memoria contenente il numero di strutture SSPARAMPROPS restituite in *prgParamProperties*.  
  
 *prgParamProperties*[out]  
 Puntatore alla memoria nel quale viene restituita una matrice di strutture SSPARAMPROPS. Il provider alloca la memoria per le strutture e restituisce l'indirizzo alla memoria. Il consumer rilascia questa memoria con **IMalloc::Free** quando le strutture non sono più necessarie. Prima di chiamare **IMalloc::Free** per *prgParamProperties*, il consumer deve chiamare anche **VariantClear** per la proprietà *vValue* di ogni struttura DBPROP in modo da impedire una perdita di memoria nei casi in cui la variante contiene un tipo di riferimento, ad esempio BSTR. Se *pcParams* è zero nell'output o si verifica un errore diverso da DB_E_ERRORSOCCURRED, il provider non alloca alcuna memoria e verifica che *prgParamProperties* sia un puntatore Null nell'output.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 Il metodo **GetParameterProperties** restituisce gli stessi codici di errore del metodo **di ICommandProperties::GetProperties** OLE DB principale, a meno che non sia possibile generare DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED.  
  
## <a name="remarks"></a>Osservazioni  
 **ISSCommandWithParameters::GetParameterProperties** ha un comportamento coerente rispetto a **GetParameterInfo**. Se [ISSCommandWithParameters::SetParameterProperties](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) o **SetParameterInfo** non è stato chiamato, o è stato chiamato con cParams pari a zero, **GetParameterInfo** deriva le informazioni sul parametro e restituisce questo risultato. Se **ISSCommandWithParameters::SetParameterProperties** o **SetParameterInfo** sono stati chiamati per almeno un parametro, **ISSCommandWithParameters::GetParameterProperties** restituisce proprietà solo per i parametri per i quali è stato chiamato **ISSCommandWithParameters::SetParameterProperties**. Se **ISSCommandWithParameters::SetParameterProperties** viene chiamato dopo **ISSCommandWithParameters::GetParameterProperties** o **GetParameterInfo**, le chiamate successive a **ISSCommandWithParameters::GetParameterProperties** restituiscono i valori sottoposti a override per i parametri per i quali è stato chiamato **ISSCommandWithParameters::SetParameterProperties**.  
  
 La struttura SSPARAMPROPS viene definita nel modo seguente:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Membro|Descrizione|  
|------------|-----------------|  
|*iOrdinal*|Numero ordinale del parametro passato.|  
|*cPropertySets*|Numero di strutture DBPROPSET in *rgPropertySets*.|  
|*rgPropertySets*|Puntatore alla memoria nel quale restituire una matrice di strutture DBPROPSET.|  
  
## <a name="see-also"></a>Vedere anche  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
