---
title: 'Isscommandwithparameters:: Getparameterproperties (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSCommandWithParameters::GetParameterProperties (OLE DB)
apitype: COM
helpviewer_keywords:
- GetParameterProperties method
ms.assetid: 7f4cc5ea-d028-4fe5-9192-bd153ab3c26c
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5e03e1ef1cd62dda40cd9b138c3d2ff3d7395ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050995"
---
# <a name="isscommandwithparametersgetparameterproperties-ole-db"></a>ISSCommandWithParameters::GetParameterProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

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
 Puntatore alla memoria nel quale viene restituita una matrice di strutture SSPARAMPROPS. Il provider alloca memoria per le strutture e restituisce l'indirizzo per la memoria. il consumer rilascia questa memoria con **IMalloc:: Free** quando non è più necessario le strutture. Prima di chiamare **IMalloc:: Free** per *prgParamProperties*, il consumer deve anche chiamare **VariantClear** per il *vValue* proprietà ogni struttura DBPROP per evitare una perdita di memoria nei casi in cui la variante contiene un riferimento di tipo (ad esempio BSTR). Se *pcParams* è zero nell'output o si verifica un errore diverso da DB_E_ERRORSOCCURRED, il provider non alloca alcuna memoria e assicura che *prgParamProperties* è un puntatore null nell'output.  
  
## <a name="return-code-values"></a>Valori restituiti  
 Il **GetParameterProperties** metodo restituisce gli stessi codici di errore OLE DB principali **ICommandProperties** metodo, ad eccezione di tale DB_S_ERRORSOCCURRED e DB_E_ERRORSOCCURED non può essere generato.  
  
## <a name="remarks"></a>Note  
 **Isscommandwithparameters:: Getparameterproperties** si comporta coerentemente rispetto alle **GetParameterInfo**. Se [isscommandwithparameters:: Setparameterproperties](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md) oppure **SetParameterInfo** non è stato chiamato o è stato chiamato con cParams pari a zero, **GetParameterInfo**deriva le informazioni sui parametri e restituisce l'oggetto. Se **isscommandwithparameters:: Setparameterproperties** oppure **SetParameterInfo** sono stati chiamati per almeno un parametro, **isscommandwithparameters:: Getparameterproperties**  restituisce le proprietà solo per i parametri per il quale **isscommandwithparameters:: Setparameterproperties** è stato chiamato. Se **isscommandwithparameters:: Setparameterproperties** viene chiamato dopo **isscommandwithparameters:: Getparameterproperties** oppure **GetParameterInfo**, le chiamate successive a **isscommandwithparameters:: Getparameterproperties** restituiscono i valori sottoposti a override per i parametri per il quale **isscommandwithparameters:: Setparameterproperties** è stato chiamato.  
  
 La struttura SSPARAMPROPS viene definita nel modo seguente:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
|Member|Descrizione|  
|------------|-----------------|  
|*iOrdinal*|Numero ordinale del parametro passato.|  
|*cPropertySets*|Numero di strutture DBPROPSET in *rgPropertySets*.|  
|*rgPropertySets*|Puntatore alla memoria nel quale restituire una matrice di strutture DBPROPSET.|  
  
## <a name="see-also"></a>Vedere anche  
 [ISSCommandWithParameters &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md)  
  
  
