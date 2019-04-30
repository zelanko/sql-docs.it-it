---
title: Metodo Close (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f43e59ed38dfde8091cb851f75a133c60874a6af
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63302500"
---
# <a name="close-method-ado"></a>Metodo Close (ADO)
Chiude un oggetto aperto e tutti gli oggetti dipendenti.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Note  
 Usare la **chiudere** metodo per chiudere un [connessione](../../../ado/reference/ado-api/connection-object-ado.md), una [Record](../../../ado/reference/ado-api/record-object-ado.md), un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), o un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto Per liberare le risorse di sistema associate. Chiusura di un oggetto senza rimuoverlo dalla memoria. è possibile modificare le impostazioni delle proprietà e aprirlo più tardi. Per eliminare completamente un oggetto dalla memoria, chiudere l'oggetto e quindi impostare la variabile oggetto *Nothing* (in Visual Basic).  
  
## <a name="connection"></a>Connessione  
 Usando il **chiudere** metodo per chiudere un **connessione** oggetto chiude anche qualsiasi oggetto attivo **Recordset** oggetti associati alla connessione. Oggetto [comandi](../../../ado/reference/ado-api/command-object-ado.md) oggetto associato il **connessione** oggetto si sta chiudendo verrà mantenuti, ma lo sarà non è più associato un **connessione** oggetti, vale a dire il [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) verrà impostata su **Nothing**. Inoltre, il **comandi** dell'oggetto [parametri](../../../ado/reference/ado-api/parameters-collection-ado.md) insieme verrà cancellato di qualsiasi parametro definito dal provider.  
  
 Successivamente è possibile chiamare il [aperto](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo Ristabilire la connessione per lo stesso oppure a un'altra origine dati. Mentre il **connessione** oggetto è chiuso, chiamare i metodi che richiedono una connessione aperta all'origine dati genera un errore.  
  
 Chiusura un **connessione** dell'oggetto anche se non vi sono aperte **Recordset** oggetti per la connessione il rollback delle modifiche in sospeso in tutti i **Recordset** oggetti. Chiusura in modo esplicito un **connessione** oggetto (chiamata il **Chiudi** (metodo)) mentre una transazione è in corso genera un errore. Se un **connessione** oggetto non rientra nell'ambito, mentre è in corso una transazione, ADO automaticamente il rollback della transazione.  
  
## <a name="recordset-record-stream"></a>Recordset, Record, Stream  
 Usando il **chiudere** metodo per chiudere un **Recordset**, **Record**, oppure **Stream** oggetto rilascia i dati associati e qualsiasi accesso esclusivo potrebbe hanno dovuto i dati tramite questo particolare oggetto. Successivamente è possibile chiamare il [aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo per riaprire l'oggetto con lo stesso, o modificate, gli attributi.  
  
 Mentre un **Recordset** oggetto è chiuso, chiamare i metodi che richiedono un cursore in tempo reale genera un errore.  
  
 Se una modifica è in corso in modalità di aggiornamento immediato, chiamando il **Chiudi** metodo genera un errore; in alternativa, chiamare il [aggiornare](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) metodo prima. Se si chiude la **Recordset** dell'oggetto in modalità di aggiornamento batch, tutte le modifiche apportate dall'ultima [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) chiamata vengono persi.  
  
 Se si usa la [Clone](../../../ado/reference/ado-api/clone-method-ado.md) metodo per creare copie di un elemento aperto **Recordset** oggetto originale o un clone di chiusura non influisce sulle altre copie.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Open e Close (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Esempio di metodi Open e Close (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Esempio di metodi Open e Close (VC + +)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Metodo Open (connessione ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
