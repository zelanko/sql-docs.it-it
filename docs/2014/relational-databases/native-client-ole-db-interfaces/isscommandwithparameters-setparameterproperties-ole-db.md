---
title: ISSCommandWithParameters::SetParameterProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters::SetParameterProperties (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- SetParameterProperties method
ms.assetid: 4cd0281a-a2a0-43df-8e46-eb478b64cb4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 778021ce007f0c1eac68197e0c07e2cb7b0bb001
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62638775"
---
# <a name="isscommandwithparameterssetparameterproperties-ole-db"></a>ISSCommandWithParameters::SetParameterProperties (OLE DB)
  Imposta le proprietà dei parametri per i singoli parametri in base al numero ordinale oppure imposta proprietà dei parametri bulk specificando una matrice di strutture SSPARAMPROPS.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
HRESULT SetParameterProperties(  
DB_UPARAMS cParams,   
SSPARAMPROPS rgParamProperties[]);  
```  
  
## <a name="arguments"></a>Argomenti  
 *cParams*[in]  
 Numero di strutture SSPARAMPROPS nella matrice *rgParamProperties*. Se questo numero è zero, `ISSCommandWithParameters::SetParameterProperties` eliminerà tutte le proprietà che potrebbero essere state specificate per tutti i parametri nel comando.  
  
 *rgParamProperties*[in]  
 Matrice di strutture SSPARAMPROPS da impostare.  
  
## <a name="return-code-values"></a>Valori del codice restituito  
 Il `ISSCommandWithParameters::SetParameterProperties` metodo restituisce gli stessi codici di errore del metodo Core OLE DB **ICommandProperties:: seproperties** .  
  
## <a name="remarks"></a>Osservazioni  
 L'impostazione delle proprietà dei parametri con questo metodo è consentita per ogni parametro in base al numero `ISSCommandWithParameters::SetParameterProperties` ordinale oppure con una singola chiamata dopo che il SSPARAMPROPS è stato compilato dalla matrice di proprietà.  
  
 Il **Metodo** SetValue deve essere chiamato prima di chiamare il `ISSCommandWithParameters::SetParameterProperties` metodo. Se si chiama `SetParameterProperties(0, NULL)`, si cancellano tutte le proprietà di parametro specificate, mentre se si chiama `SetParameterInfo(0,NULL,NULL)`, si cancellano tutte le informazioni di parametro che includono le proprietà che potrebbero essere associate a un parametro.  
  
 La `ISSCommandWithParameters::SetParameterProperties` chiamata a per specificare le proprietà per un parametro che non è di tipo DBTYPE_XML o DBTYPE_UDT restituisce DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED e contrassegna il campo *DwStatus* di tutti DBPROPs contenuti in SSPARAMPROPS per il parametro con DBPROPSTATUS_NOTSET. È necessario attraversare la matrice DBPROP di ogni proprietà DBPROPSET contenuta nella struttura SSPARAMPROPS per individuare il parametro al quale DB_E_ERRORSOCCURRED o DB_S_ERRORSOCCURRED fa riferimento.  
  
 Se `ISSCommandWithParameters::SetParameterProperties` viene chiamato il metodo per specificare le proprietà dei parametri le cui informazioni sui parametri non sono ancora state impostate con il metodo **sqlparameterinfo**, il provider restituisce E_UNEXPECTED con il messaggio di errore seguente:  
  
 Impossibile chiamare il metodo SetParameterProperties per i parametri specificati senza chiamare prima il metodo SetParameterInfo. È necessario impostare le informazioni sui parametri prima di impostare le proprietà dei parametri stessi.  
  
 Se la chiamata a `ISSCommandWithParameters::SetParameterProperties` contiene alcuni parametri in cui sono state impostate le informazioni sul parametro e alcuni parametri in cui non sono state impostate le informazioni sul parametro, le proprietà DWSTATUS in DBPROPSET del set di proprietà SSPARAMPROPS restituiranno con DBSTATUS_NOTSET.  
  
 La struttura SSPARAMPROPS viene definita nel modo seguente:  
  
 `struct SSPARAMPROPS {`  
  
 `DBORDINAL iOrdinal;`  
  
 `ULONG cPropertySets;`  
  
 `DBPROPSET *rgPropertySets;`  
  
 `};`  
  
 I miglioramenti apportati al motore di database a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] consentono a ISSCommandWithParameters::SetParameterProperties di ottenere descrizioni più accurate dei risultati previsti. È possibile che questi risultati più accurati differiscano dai valori restituiti da ISSCommandWithParameters::SetParameterProperties nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
|Membro|Descrizione|  
|------------|-----------------|  
|*iOrdinal*|Numero ordinale del parametro passato.|  
|*cPropertySets*|Numero di strutture DBPROPSET in *rgPropertySets*.|  
|*rgPropertySets*|Puntatore alla memoria nel quale restituire una matrice di strutture DBPROPSET.|  
  
## <a name="see-also"></a>Vedi anche  
 [ISSCommandWithParameters &#40;OLE DB&#41;](isscommandwithparameters-ole-db.md)  
  
  
