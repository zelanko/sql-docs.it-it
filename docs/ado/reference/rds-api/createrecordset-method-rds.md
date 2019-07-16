---
title: Esempio di metodo CreateRecordset (Servizi Desktop remoto) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65f7d415864b169b683e0c9ab858506d31783b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964518"
---
# <a name="createrecordset-method-rds"></a>Metodo CreateRecordset (Servizi Desktop remoto)
Crea un oggetto vuoto, disconnesso [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server di servizi desktop remoto non sono più incluse nel sistema operativo Windows (vedere Windows 8 e [indicazioni sulla compatibilità di Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) per altri dettagli). I componenti client di servizi desktop remoto verranno rimosso in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che usano servizi desktop remoto devono eseguire la migrazione a [di WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Oggetto*  
 Una variabile oggetto che rappresenta un' [RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) o [Servizi Desktop remoto. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) oggetto.  
  
 *ColumnsInfos*  
 Oggetto **Variant** matrice di attributi che definiscono ciascuna colonna il **Recordset** creato. Ogni definizione di colonna contiene una matrice di quattro attributi obbligatori e un attributo facoltativo.  
  
|attribute|Descrizione|  
|---------------|-----------------|  
|Name|Nome dell'intestazione di colonna.|  
|type|Valore intero del tipo di dati.|  
|Size|Valore intero della larghezza in caratteri, indipendentemente dal tipo di dati.|  
|Supporto di valori Null|Valore booleano.|  
|Scalabilità (facoltativo)|Questo attributo facoltativo definisce la scala per i campi numerici. Se questo valore viene omesso, verranno troncati in una scala pari a tre valori numerici. Precisione non è interessata, ma verrà troncato a tre il numero di cifre dopo il separatore decimale.|  
  
 Il set di matrici di colonna viene quindi raggruppati in una matrice, che definisce il **Recordset**.  
  
## <a name="remarks"></a>Note  
 L'oggetto business sul lato server è possibile popolare l'oggetto risultante **Recordset** con i dati da un provider di dati non OLE DB, ad esempio un sistema operativo file contenenti le quotazioni di borsa.  
  
 La tabella seguente elenca i [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) i valori supportati per il **CreateRecordset** (metodo). Il numero indicato è il numero di riferimento usato per definire i campi.  
  
 Ognuno dei tipi di dati è a lunghezza fissa o a lunghezza variabile. Tipi a lunghezza fissa devono essere definiti con una dimensione di -1, perché la dimensione è predeterminata e una definizione di dimensioni è ancora necessaria. Tipi di dati a lunghezza variabile consentono una dimensione compreso tra 1 e 32767.  
  
 Per alcuni dei tipi di dati della variabile, il tipo può essere assegnato al tipo indicato nella colonna di sostituzione. Non si vedranno le sostituzioni fino a dopo il **Recordset** creato e riempito. È quindi possibile cercare il tipo di dati effettivo, se necessario.  
  
|Length|Costante|Number|Sostituzione|  
|------------|--------------|------------|------------------|  
|Fisso|**adTinyInt**|16||  
|Fisso|**adSmallInt**|2||  
|Fisso|**adInteger**|3||  
|Fisso|**adBigInt**|20||  
|Fisso|**adUnsignedTinyInt**|17||  
|Fisso|**adUnsignedSmallInt**|18||  
|Fisso|**adUnsignedInt**|19||  
|Fisso|**adUnsignedBigInt**|21||  
|Fisso|**adSingle**|4||  
|Fisso|**adDouble**|5||  
|Fisso|**adCurrency**|6||  
|Fisso|**adDecimal**|14||  
|Fisso|**adNumeric**|131||  
|Fisso|**adBoolean**|11||  
|Fisso|**adError**|10||  
|Fisso|**adGuid**|72||  
|Fisso|**adDate**|7||  
|Fisso|**adDBDate**|133||  
|Fisso|**adDBTime**|134||  
|Fisso|**adDBTimestamp**|135|7|  
|Variabile|**adBSTR**|8|130|  
|Variabile|**adChar**|129|200|  
|Variabile|**adVarChar**|200||  
|Variabile|**adLongVarChar**|201|200|  
|Variabile|**adWChar**|130||  
|Variabile|**adVarWChar**|202|130|  
|Variabile|**adLongVarWChar**|203|130|  
|Variabile|**adBinary**|128||  
|Variabile|**adVarBinary**|204||  
|Variabile|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto DataControl (Servizi Desktop remoto)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Oggetto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo CreateRecordset (VB)](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [Esempio di metodo CreateRecordset (VBScript)](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [Metodo CreateObject (Servizi Desktop remoto)](../../../ado/reference/rds-api/createobject-method-rds.md)



