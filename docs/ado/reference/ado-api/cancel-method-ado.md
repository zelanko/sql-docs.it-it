---
title: Metodo Cancel (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db369b32737c0e2dae4603a4a5a6c26cdd3a7142
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920233"
---
# <a name="cancel-method-ado"></a>Metodo Cancel (ADO)
Annulla l'esecuzione di una chiamata al metodo asincrono in sospeso.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **Cancel** per terminare l'esecuzione di una chiamata al metodo asincrono, ovvero un metodo richiamato con l'opzione **adAsyncConnect**, **adAsyncExecute**o **adAsyncFetch** .  
  
 Nella tabella seguente viene illustrata l'attività terminata quando si utilizza il metodo **Cancel** su un particolare tipo di oggetto.  
  
|Se l'oggetto è un *oggetto*|L'ultima chiamata asincrona a questo metodo viene terminata|  
|----------------------|-------------------------------------------------------------|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|[Eseguire](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Connessione](../../../ado/reference/ado-api/connection-object-ado.md)|[Esegui](../../../ado/reference/ado-api/execute-method-ado-connection.md) o [Apri](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[Record](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)o [Open](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[recordset](../../../ado/reference/ado-api/recordset-object-ado.md)|[Apri](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Flusso](../../../ado/reference/ado-api/stream-object-ado.md)|[Apri](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>Si applica a  
  
||||  
|-|-|-|  
|[Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Cancel (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Esempio di metodo Cancel (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Esempio di metodo Cancel (VC + +)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Metodo Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Metodo CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Metodo Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Metodo Execute (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (Recordset - ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
