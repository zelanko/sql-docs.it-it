---
title: ISSCommandWithParameters::GetParameterProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ebc423dd019b5a161fd767d7b9ca8eaac8d8e335
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704808"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
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
 Puntatore alla memoria nel quale viene restituita una matrice di strutture SSPARAMPROPS. Il provider alloca memoria per le strutture e restituisce l'indirizzo alla memoria. il consumer rilascia la memoria con **IMalloc:: Free** quando non necessita più delle strutture. Prima di chiamare **IMalloc:: Free** per *prgParamProperties*, il consumer deve chiamare anche **VariantClear** per la proprietà *vValue* di ogni struttura DBPROP per evitare una perdita di memoria nei casi in cui la variante contiene un tipo di riferimento, ad esempio un BSTR. Se *pcParams* è zero nell'output o si verifica un errore diverso da DB_E_ERRORSOCCURRED, il provider non alloca alcuna memoria e assicura che *prgParamProperties* sia un puntatore null nell'output.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 Il metodo **GetParameterProperties** restituisce gli stessi codici di errore del metodo Core OLE DB **ICommandProperties:: GetProperties** , ad eccezione del fatto che non è possibile generare DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED.  
  
## <a name="remarks"></a>Osservazioni  
 **ISSCommandWithParameters:: GetParameterProperties** si comporta in modo coerente rispetto a **GetParameterInfo**. Se [ISSCommandWithParameters:: SetParameterProperties](isscommandwithparameters-setparameterproperties-ole-db.md) o **sqlparameterinfo** non sono stati chiamati o sono stati chiamati con cParams uguale a zero, **GetParameterInfo** deriva le informazioni sui parametri e restituisce this. Se **ISSCommandWithParameters:: SetParameterProperties** o **separameterinfo** è stato chiamato per almeno un parametro, **ISSCommandWithParameters:: GetParameterProperties** restituisce proprietà solo per i parametri per i quali è stato chiamato **ISSCommandWithParameters:: SetParameterProperties** . Se **ISSCommandWithParameters:: SetParameterProperties** viene chiamato dopo **ISSCommandWithParameters:: GetParameterProperties** o **GetParameterInfo**, le chiamate successive a **ISSCommandWithParameters:: GetParameterProperties** restituiscono i valori sottoposti a override per i parametri per i quali è stato chiamato **ISSCommandWithParameters:: SetParameterProperties** .  
  
 La struttura SSPARAMPROPS viene definita nel modo seguente:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Membro|Description|  
|------------|-----------------|  
|*iOrdinal*|Numero ordinale del parametro passato.|  
|*cPropertySets*|Numero di strutture DBPROPSET in *rgPropertySets*.|  
|*rgPropertySets*|Puntatore alla memoria nel quale restituire una matrice di strutture DBPROPSET.|  
  
## <a name="see-also"></a>Vedere anche  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
