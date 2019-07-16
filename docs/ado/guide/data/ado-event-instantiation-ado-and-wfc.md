---
title: 'Creazione di istanze di eventi ADO: ADO e WFC | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ee4be21-657b-407a-afa4-0b27a6b096ce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e83ffa37af2a6e33cad2645105b0df034f59d9f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926184"
---
# <a name="ado-event-instantiation-ado-and-wfc"></a>Creazione di istanze di eventi ADO: ADO e WFC
ADO per Windows Foundation Classes (ADO/WFC) si basa sul modello di eventi ADO e presenta un'interfaccia di programmazione di applicazioni semplificati. In generale, ADO/WFC intercetta eventi ADO, consente di consolidare i parametri dell'evento in una classe di evento singolo e quindi chiama il gestore eventi.  
  
### <a name="to-use-ado-events-in-adowfc"></a>Usare gli eventi ADO in ADO/WFC  
  
1.  Definire il proprio gestore dell'evento per l'elaborazione di un evento. Ad esempio, se si desidera elaborare le **ConnectComplete** evento nel **ConnectionEvent** della famiglia, è possibile usare questo codice:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    {  
        System.out.println("onConnectComplete:" + e);  
    }  
    ```  
  
2.  Definire un oggetto gestore per rappresentare il gestore eventi. L'oggetto gestore deve essere del tipo di dati **ConnectEventHandler** per un evento di tipo **ConnectionEvent**, o tipo di dati **RecordsetEventHandler** per un evento di tipo  **RecordsetEvent**. Esempio di codice seguente per il **ConnectComplete** gestore dell'evento:  
  
    ```  
    ConnectionEventHandler handler =   
        new ConnectionEventHandler(this, "onConnectComplete");  
    ```  
  
     Il primo argomento del **ConnectionEventHandler** costruttore è un riferimento alla classe che contiene il gestore eventi specificato nel secondo argomento.  
  
3.  Aggiungere il gestore eventi per un elenco di gestori designato per l'elaborazione di un particolare tipo di evento. Utilizzare il metodo con un nome, ad esempio **addOn** *EventName*(*gestore*).  
  
4.  ADO/WFC internamente implementa tutti i gestori eventi ADO. Pertanto, un evento è causato da un **connessione** oppure **Recordset** operazione viene intercettata da un gestore eventi ADO o WFC.  
  
     Il gestore di eventi ADO/WFC passa ADO **ConnectionEvent** i parametri in un'istanza di ADO o WFC **ConnectionEvent** classe o ADO **RecordsetEvent** parametri in un istanza di ADO o WFC **RecordsetEvent** classe. Queste classi di ADO o WFC consolidano i parametri dell'evento ADO; vale a dire, ogni classe di ADO o WFC contiene un membro di dati per ogni parametro univoca in tutto l'oggetto ADO **ConnectionEvent** oppure **RecordsetEvent** metodi.  
  
5.  ADO/WFC quindi chiama il gestore eventi con l'oggetto evento di ADO o WFC. Ad esempio, il **onConnectComplete** gestore ha una firma simile al seguente:  
  
    ```  
    public void onConnectComplete(Object sender,ConnectionEvent e)  
    ```  
  
     Il primo argomento è il tipo di oggetto che ha inviato l'evento ([Connection](../../../ado/reference/ado-api/connection-object-ado.md) oppure [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)), mentre il secondo argomento è l'oggetto evento di ADO o WFC (**ConnectionEvent** o **RecordsetEvent**).  
  
     La firma del gestore dell'evento è più semplice rispetto a un evento di ADO. Tuttavia, è comunque necessario comprendere il modello di eventi ADO conoscere ciò che si applicano i parametri a un evento e come rispondere.  
  
6.  Restituito dal gestore eventi per il gestore di ADO o WFC per l'evento di ADO. ADO/WFC copia i membri dati di eventi ADO/WFC pertinenti ai parametri di eventi ADO e restituisce quindi il gestore di eventi ADO.  
  
7.  Al termine l'elaborazione, rimuovere il gestore dall'elenco di gestori eventi ADO o WFC. Utilizzare il metodo con un nome, ad esempio **removeOn** *EventName*(*gestore*).  
  
## <a name="see-also"></a>Vedere anche  
 [Riepilogo dei gestori eventi ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO - WFC sintassi indice](../../../ado/reference/ado-api/ado-wfc-syntax-index.md)   
 [Parametri di evento](../../../ado/guide/data/event-parameters.md)   
 [Sull'interagiscono tra i gestori eventi](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipi di eventi](../../../ado/guide/data/types-of-events.md)
