---
title: I parametri di evento | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2912328aa61437b663a290952deaaea7b5c06bca
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700753"
---
# <a name="event-parameters"></a>Parametri evento
Ogni gestore di evento include un parametro di stato che controlla il gestore dell'evento. Per gli eventi completati, questo parametro viene utilizzato anche per indicare l'esito positivo o negativo dell'operazione che ha generato l'evento. Gli eventi più completi hanno anche un parametro di errore per fornire informazioni su eventuali errori che potrebbero essersi verificati e uno o più parametri di oggetti che fanno riferimento a oggetti ADO usati per eseguire l'operazione. Ad esempio, il [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento include i parametri di oggetto per il **comando**, **Recordset**, e **connessione** oggetti associato all'evento. Nell'esempio seguente di Microsoft® Visual Basic®, è possibile visualizzare il pCommand, pCommand e pConnection gli oggetti che rappresentano il **comandi**, **Recordset**, e **connessione** gli oggetti utilizzati per il **Execute** (metodo).  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 Fatta eccezione per il **errore** dell'oggetto, gli stessi parametri vengono passati agli eventi Will. In questo modo si esamina ogni oggetto che verrà utilizzato nell'operazione in sospeso e determinare se l'operazione deve essere consentito alla fine.  
  
 Alcuni gestori di eventi presentano un *motivo* parametro, che fornisce informazioni aggiuntive sui motivi per cui si è verificato l'evento. Ad esempio, il **WillMove** e **MoveComplete** gli eventi possono verificarsi a causa di uno dei metodi di esplorazione (**MoveNext**, **MovePrevious**e così via) venga chiamato o come risultato di ripetizione di una query.  
  
## <a name="status-parameter"></a>Parametro di stato  
 Quando viene chiamata la routine del gestore eventi, il *stato* parametro è impostato su uno dei valori seguenti.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**adStatusOK**|Passato verrà sia eventi completati. Questo valore indica che l'operazione che ha causato l'evento completata.|  
|**adStatusErrorsOccurred**|Passato completati solo agli eventi. Questo valore indica che l'operazione che ha causato l'evento ha avuto esito negativo o un evento verrà annullato l'operazione. Verificare i *errore* parametro per altri dettagli.|  
|**adStatusCantDeny**|Passato verrà solo agli eventi. Questo valore indica che l'operazione non può essere annullato dall'evento verrà. Deve essere eseguita.|  
  
 Se si determina nell'evento Will che l'operazione deve continuare, lasciare il *stato* parametro invariato. Fino a quando il parametro di stato in entrata non è stato impostato **adStatusCantDeny**, tuttavia, è possibile annullare l'operazione in sospeso modificando *stato* al **adStatusCancel**. Quando si esegue questa operazione, l'evento di completamento associato con l'operazione ha relativi *lo stato* parametro impostato su **adStatusErrorsOccurred**. Il **errore** oggetto passato all'evento Complete, conterrà il valore **adErrOperationCancelled**.  
  
 Se non si desidera elaborare un evento, è possibile impostare *lo stato* al **adStatusUnwantedEvent** e l'applicazione non riceverà più notifiche di quell ' evento. Tuttavia, tenere presente che alcuni eventi possono essere generati per più di uno dei motivi. In tal caso, è necessario specificare **adStatusUnwantedEvent** per ciascun motivo possibili. Ad esempio, per interrompere la ricezione di notifiche in sospeso **RecordChange** eventi, è necessario impostare la *stato* parametro **adStatusUnwantedEvent** per  **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, e **adRsnFirstChange** appena si verificano.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|Richiesta che questo gestore eventi non riceverà alcun altre notifiche.|  
|**adStatusCancel**|Richiedere l'annullamento dell'operazione che sta per verificarsi.|  
  
## <a name="error-parameter"></a>Errore parametro  
 Il *errore* parametro è un riferimento a un oggetto ADO [errore](../../../ado/reference/ado-api/error-object.md) oggetto. Quando la *lo stato* parametro è impostato su **adStatusErrorsOccurred**, il **errore** oggetto contiene i dettagli sulla mancata riuscita dell'operazione. Se l'evento verrà associata a un evento di completamento ha annullato l'operazione impostando il *lo stato* parametro per **adStatusCancel**, l'oggetto errore viene sempre impostato su  **adErrOperationCancelled**.  
  
## <a name="object-parameter"></a>Parametro dell'oggetto  
 Ogni evento riceve uno o più oggetti che rappresentano gli oggetti che sono coinvolti nell'operazione. Ad esempio, il **ExecuteComplete** evento riceve un **comando** oggetto, una **Recordset** oggetto e un **connessione** oggetto.  
  
## <a name="reason-parameter"></a>Parametro Reason  
 Il *motivo* parametro *adReason*, fornisce informazioni aggiuntive sui motivi per cui si è verificato l'evento. Gli eventi con un *adReason* parametro può essere chiamato più volte, anche per la stessa operazione per un motivo diverso ogni volta. Ad esempio, il **WillChangeRecord** gestore eventi viene chiamato per le operazioni che stanno tentando di eseguire o annullare l'inserimento, eliminazione o la modifica di un record. Se si desidera elaborare un evento solo quando si verifica per un motivo particolare, è possibile usare la *adReason* parametro per filtrare le occorrenze non si è interessati. Ad esempio, se si desidera elaborare gli eventi di modifica di record solo quando si verificano perché è stato aggiunto un record, è possibile usare quanto segue.  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 In questo caso, la notifica può verificarsi per ognuno degli altri motivi. Tuttavia, che verrà eseguito una sola volta per ciascun motivo. Dopo la notifica si è verificata una volta per ciascun motivo, si riceverà la notifica solo per l'aggiunta di un nuovo record.  
  
 Al contrario, è necessario impostare *adStatus* al **adStatusUnwantedEvent** solo una volta per richiedere che un gestore eventi senza una **adReason** evento ricevente stop parametro notifiche.  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creazione di istanze evento ADO per linguaggio](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Sull'interagiscono tra i gestori eventi](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipi di eventi](../../../ado/guide/data/types-of-events.md)
