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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65f7d415864b169b683e0c9ab858506d31783b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964518"
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
 *Object*  
 Variabile oggetto che rappresenta un [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) o Servizi Desktop remoto [. Oggetto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *ColumnsInfos*  
 Matrice **Variant** di attributi che definisce ogni colonna del **Recordset** creato. Ogni definizione di colonna contiene una matrice di quattro attributi obbligatori e un attributo facoltativo.  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|Nome|Nome dell'intestazione di colonna.|  
|Type|Integer del tipo di dati.|  
|Dimensione|Integer della larghezza in caratteri, indipendentemente dal tipo di dati.|  
|Supporto di valori Null|Valore booleano.|  
|Scala (facoltativo)|Questo attributo facoltativo definisce la scala per i campi numerici. Se questo valore non viene specificato, i valori numerici verranno troncati a una scala di tre. La precisione non è interessata, ma il numero di cifre che seguono il separatore decimale verrà troncato a tre.|  
  
 Il set di matrici di colonne viene quindi raggruppato in una matrice, che definisce il **Recordset**.  
  
## <a name="remarks"></a>Osservazioni  
 L'oggetto business sul lato server può popolare il **Recordset** risultante con i dati di un provider di dati non OLE DB, ad esempio un file del sistema operativo contenente le virgolette predefinite.  
  
 Nella tabella seguente sono elencati i valori [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) supportati dal metodo **CreateRecordset** . Il numero elencato è il numero di riferimento utilizzato per definire i campi.  
  
 Ognuno dei tipi di dati è a lunghezza fissa o a lunghezza variabile. I tipi a lunghezza fissa devono essere definiti con una dimensione di-1, perché le dimensioni sono predeterminate e la definizione delle dimensioni è ancora richiesta. I tipi di dati a lunghezza variabile consentono una dimensione compresa tra 1 e 32767.  
  
 Per alcuni tipi di dati delle variabili, il tipo può essere assegnato al tipo indicato nella colonna di sostituzione. Le sostituzioni non vengono visualizzate finché non viene creato e compilato il **Recordset** . È quindi possibile verificare il tipo di dati effettivo, se necessario.  
  
|Length|Costante|Number|Sostituzione|  
|------------|--------------|------------|------------------|  
|Correzione|**adTinyInt**|16||  
|Correzione|**adSmallInt**|2||  
|Correzione|**adInteger**|3||  
|Correzione|**adBigInt**|20||  
|Correzione|**adUnsignedTinyInt**|17||  
|Correzione|**adUnsignedSmallInt**|18||  
|Correzione|**adUnsignedInt**|19||  
|Correzione|**adUnsignedBigInt**|21||  
|Correzione|**adSingle**|4||  
|Correzione|**adDouble**|5||  
|Correzione|**adCurrency**|6||  
|Correzione|**adDecimal**|14||  
|Correzione|**adNumeric**|131||  
|Correzione|**adBoolean**|11||  
|Correzione|**adError**|10||  
|Correzione|**adGuid**|72||  
|Correzione|**adDate**|7||  
|Correzione|**adDBDate**|133||  
|Correzione|**adDBTime**|134||  
|Correzione|**adDBTimestamp**|135|7|  
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



