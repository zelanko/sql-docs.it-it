---
title: Metodo CreateRecordset (RDS) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae2d78f4647e2aefa707e97349daa73d08ee492
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748847"
---
# <a name="createrecordset-method-rds"></a>Metodo CreateRecordset (Servizi Desktop remoto)
Crea un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)vuoto e disconnesso.  
  
> [!IMPORTANT]
>  A partire da Windows 8 e Windows Server 2012, i componenti server Servizi Desktop remoto non sono più inclusi nel sistema operativo Windows. per altri dettagli, vedere le informazioni di riferimento sulla compatibilità di Windows 8 e [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) . I componenti client Servizi Desktop remoto verranno rimossi in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Le applicazioni che utilizzano Servizi Desktop remoto devono eseguire la migrazione a [WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Oggetto*  
 Variabile oggetto che rappresenta un [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) o Servizi Desktop remoto [. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *ColumnsInfos*  
 Matrice **Variant** di attributi che definisce ogni colonna del **Recordset** creato. Ogni definizione di colonna contiene una matrice di quattro attributi obbligatori e un attributo facoltativo.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|Nome|Nome dell'intestazione di colonna.|  
|Tipo|Integer del tipo di dati.|  
|Dimensione|Integer della larghezza in caratteri, indipendentemente dal tipo di dati.|  
|Supporto di valori Null|.|  
|Scala (facoltativo)|Questo attributo facoltativo definisce la scala per i campi numerici. Se questo valore non viene specificato, i valori numerici verranno troncati a una scala di tre. La precisione non è interessata, ma il numero di cifre che seguono il separatore decimale verrà troncato a tre.|  
  
 Il set di matrici di colonne viene quindi raggruppato in una matrice, che definisce il **Recordset**.  
  
## <a name="remarks"></a>Osservazioni  
 L'oggetto business sul lato server può popolare il **Recordset** risultante con i dati di un provider di dati non OLE DB, ad esempio un file del sistema operativo contenente le virgolette predefinite.  
  
 Nella tabella seguente sono elencati i valori [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) supportati dal metodo **CreateRecordset** . Il numero elencato è il numero di riferimento utilizzato per definire i campi.  
  
 Ognuno dei tipi di dati è a lunghezza fissa o a lunghezza variabile. I tipi a lunghezza fissa devono essere definiti con una dimensione di-1, perché le dimensioni sono predeterminate e la definizione delle dimensioni è ancora richiesta. I tipi di dati a lunghezza variabile consentono una dimensione compresa tra 1 e 32767.  
  
 Per alcuni tipi di dati delle variabili, il tipo può essere assegnato al tipo indicato nella colonna di sostituzione. Le sostituzioni non vengono visualizzate finché non viene creato e compilato il **Recordset** . È quindi possibile verificare il tipo di dati effettivo, se necessario.  
  
|Length|Costante|Numero|Sostituzione|  
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



