---
title: Eseguire il metodo (connessione ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a52ca419f3f06e4156c278cb0ba8999c24e09ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63071137"
---
# <a name="execute-method-ado-connection"></a>Metodo Execute (Connection - ADO)
Esegue la query specificata, SQL istruzione, stored procedure o il testo del provider.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un [Recordset ADO (Object)](../../../ado/reference/ado-api/recordset-object-ado.md) riferimento all'oggetto.  
  
#### <a name="parameters"></a>Parametri  
 *CommandText*  
 Oggetto **stringa** valore contenente l'istruzione SQL, stored procedure, un URL o il testo del provider per l'esecuzione. **Facoltativamente**, nomi di tabella possono essere usati solo se il provider è compatibile con SQL. Per ad esempio se un nome di tabella "Customers" viene usato, ADO anteporrà la sintassi SQL Select standard per creare e passare a "SELECT * FROM Customers" automaticamente come un [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzione per il provider.  
  
 *RecordsAffected*  
 Facoltativo. Oggetto **lungo** variabile in cui il provider restituisce il numero di record interessati dall'operazione.  
  
 *Opzioni*  
 Facoltativo. Oggetto **lungo** valore che indica come il provider deve restituire l'argomento CommandText. Può essere una maschera di bit di uno o più [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) oppure [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) valori.  
  
 **Nota** usare il **ExecuteOptionEnum** valore **adExecuteStream** per migliorare le prestazioni riducendo al minimo l'elaborazione interna e per le applicazioni che si esegue il porting da Visual Basic 6.0.  
  
 Non utilizzare **adExecuteStream** con il **Execute** metodo di un **connessione** oggetto.  
  
 Non utilizzare valori CommandTypeEnum adCmdFile o adCmdTableDirect con Execute. Questi valori possono essere usati solo come opzioni con il [metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [metodo Requery](../../../ado/reference/ado-api/requery-method.md) metodi di una **Recordset**.  
  
## <a name="remarks"></a>Note  
 Usando il **Execute** metodo su un [connessione ADO (Object)](../../../ado/reference/ado-api/connection-object-ado.md) viene eseguito l'oggetto di qualsiasi query passata al metodo nell'argomento CommandText della connessione specificata. Se l'argomento CommandText specifica una query che restituiscono righe, i risultati generati dall'esecuzione vengono archiviati in una nuova **Recordset** oggetto. Se il comando non può restituire risultati (ad esempio, una query di aggiornamento di SQL) restituisce il provider **Nothing** fino a quando l'opzione **adExecuteStream** è specificata; in caso contrario, il metodo Execute restituisce un chiuso **Recordset**.  
  
 L'oggetto restituito **Recordset** oggetto è sempre un cursore forward-only in sola lettura. Se è necessario un **Recordset** dell'oggetto con più funzionalità, creare prima una **Recordset** con le impostazioni delle proprietà desiderate, quindi specificare la **Recordset** dell'oggetto [ Metodo (Recordset ADO) Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo per eseguire la query e restituire il tipo di cursore desiderati.  
  
 Il contenuto del *CommandText* argomento sono specifico del provider e può essere la sintassi SQL standard o qualsiasi formato di comando speciale che supporta il provider.  
  
 Verrà generato un evento ExecuteComplete quando questa operazione è terminata.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
