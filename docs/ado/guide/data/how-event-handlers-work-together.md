---
title: Sull'interagiscono tra i gestori di eventi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cb02a96e6ee3d28c67e21996677c02b58fc97c07
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718386"
---
# <a name="how-event-handlers-work-together"></a>Interazione tra i gestori eventi
A meno che la programmazione in Visual Basic, tutti i gestori di eventi per **Connection** e **Recordset** gli eventi devono essere implementati, indipendentemente dal fatto che è effettivamente elaborare tutti gli eventi. La quantità di lavoro di implementazione che è necessario eseguire dipende dal linguaggio di programmazione. Per altre informazioni, vedere [creazione di istanze evento ADO per linguaggio](../../../ado/guide/data/ado-event-instantiation-by-language.md).  
  
## <a name="paired-event-handlers"></a>Gestori eventi associati  
 È associato un ciascun gestore eventi verrà **completa** gestore dell'evento. Ad esempio, quando l'applicazione modifica il valore di un campo, il **WillChangeField** gestore eventi viene chiamato. Se la modifica è accettabile, l'applicazione non modifica il **adStatus** parametro invariato e viene eseguita l'operazione. Al termine dell'operazione, un **FieldChangeComplete** evento informa l'applicazione che l'operazione è stata completata. Se completata correttamente, **adStatus** contiene **adStatusOK**; in caso contrario, **adStatus** contiene **adStatusErrorsOccurred** e è necessario controllare la **errore** oggetto per determinare la causa dell'errore.  
  
 Quando **WillChangeField** viene chiamato, si potrebbe determinare che la modifica non dovrebbe essere eseguita. In questo caso, impostare **adStatus** a **adStatusCancel.** L'operazione sia annullata e il **FieldChangeComplete** evento riceve un **adStatus** pari a **adStatusErrorsOccurred**. Il **errore** oggetto contiene **adErrOperationCancelled** in modo che il **FieldChangeComplete** gestore riconosce che l'operazione è stata annullata. Tuttavia, è necessario controllare il valore della **adStatus** prima di modificarla, perché l'impostazione del parametro **adStatus** a **adStatusCancel** non ha alcun effetto se è stato impostato il parametro per **adStatusCantDeny** sulla voce per la procedura.  
  
 In alcuni casi un'operazione può generare più di un evento. Ad esempio, il **Recordset** oggetto dispone di eventi per accoppiati **campo** modifiche e **Record** le modifiche. Quando l'applicazione modifica il valore di una **campo**, il **WillChangeField** gestore eventi viene chiamato. Se determina che l'operazione può continuare, la **WillChangeRecord** gestore eventi viene inoltre generato. Se questo gestore consente anche l'evento continuare, la modifica venga apportata e il **FieldChangeComplete** e **RecordChangeComplete** vengono chiamati i gestori di eventi. L'ordine in cui vengono chiamati i gestori di eventi verranno per una determinata operazione non è definito, è consigliabile evitare la scrittura di codice che dipende da una determinata sequenza di chiamata dei gestori.  
  
 Nelle istanze quando vengono generati più eventi Will, uno degli eventi può annullare l'operazione in sospeso. Ad esempio, quando l'applicazione modifica il valore di una **campo**, entrambi **WillChangeField** e **WillChangeRecord** viene chiamati in genere i gestori eventi. Tuttavia, se l'operazione viene annullata nel primo gestore dell'evento, a esso associata **completa** gestore viene chiamato immediatamente con **adStatusOperationCancelled**. Il secondo gestore non viene mai chiamato. Se, tuttavia, il primo gestore dell'evento consente all'evento di procedere, verrà chiamato il gestore di evento. Se Annulla quindi l'operazione, entrambe **completa** eventi verranno chiamati come negli esempi precedenti.  
  
## <a name="unpaired-event-handlers"></a>Gestori di eventi non abbinati  
 Fino a quando lo stato passati per l'evento non è **adStatusCantDeny**, è possibile disattivare le notifiche degli eventi per qualsiasi evento restituendo **adStatusUnwantedEvent** nel *stato*parametro. Ad esempio, quando le **completa** gestore eventi viene chiamato la prima volta, è possibile restituire **adStatusUnwantedEvent**. Successivamente verranno ricevuti solo **verranno** gli eventi. Tuttavia, alcuni eventi possono essere attivati per più di un motivo. In tal caso, l'evento avrà un *motivo* parametro. Quando si torna **adStatusUnwantedEvent**, verrà interrotta la ricezione delle notifiche per l'evento solo quando si verificano per tale motivo particolare. In altre parole, potenzialmente si riceverà la notifica per ogni possibile motivo che è stato attivato l'evento.  
  
 Singolo **verranno** gestori di eventi possono essere utili quando si desidera esaminare i parametri che verranno usati in un'operazione. È possibile modificare i parametri dell'operazione o annullare l'operazione.  
  
 In alternativa, lasciare **completa** attivata la notifica evento. Quando viene chiamato il primo gestore dell'evento verrà, restituire **adStatusUnwantedEvent**. Successivamente verranno ricevuti solo **completa** gli eventi.  
  
 Singolo **completa** gestori di eventi possono essere utili per la gestione delle operazioni asincrone. Ogni operazione asincrona ha un'apposita **completa** evento.  
  
 Ad esempio, può richiedere molto tempo per popolare un grande [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto. Se l'applicazione è scritta correttamente, è possibile avviare un `Recordset.Open(...,adAsyncExecute)` operazione e continuare con altre attività di elaborazione. Sarà infine una notifica quando la **Recordset** viene popolato da un **ExecuteComplete** evento.  
  
## <a name="single-event-handlers-and-multiple-objects"></a>I gestori eventi singolo e più oggetti  
 La flessibilità di un linguaggio di programmazione, ad esempio Microsoft Visual C++® consente di avere uno degli eventi di processo del gestore eventi da più oggetti. Ad esempio, si potrebbe avere uno **Disconnect** evento gestore elaborare eventi da diversi **connessione** oggetti. Se una delle connessioni è terminata, il **Disconnect** gestore eventi viene chiamato. È possibile indicare connessione che ha causato l'evento perché il parametro dell'oggetto del gestore eventi potrebbe essere impostato su corrispondente **connessione** oggetto.  
  
> [!NOTE]
>  Questa tecnica non può essere usata in Visual Basic perché tale lingua è in grado di correlare un solo oggetto a un gestore eventi.  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creazione di istanze evento ADO per linguaggio](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Parametri di evento](../../../ado/guide/data/event-parameters.md)   
 [Tipi di eventi](../../../ado/guide/data/types-of-events.md)
