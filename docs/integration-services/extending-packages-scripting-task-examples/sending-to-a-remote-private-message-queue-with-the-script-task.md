---
description: Invio di messaggi a una coda privata remota tramite l'attività Script
title: Invio di messaggi a una coda privata remota tramite l'attività Script | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5bc25b37bb4dfac2aa03795972edb56eb406aebd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430343"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>Invio di messaggi a una coda privata remota tramite l'attività Script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Accodamento messaggi (noto anche come MSMQ) consente agli sviluppatori di applicazioni di comunicare in modo rapido, semplice e affidabile con i programmi applicativi mediante l'invio e la ricezione di messaggi. Una coda di messaggi può trovarsi nel computer locale o in un computer remoto e può essere pubblica o privata. In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], la gestione connessione MSMQ e l'attività Message Queue non supportano l'invio a una coda privata su un computer remoto. Tuttavia, utilizzando l'attività Script, è possibile inviare facilmente un messaggio a una coda privata remota.  
  
> [!NOTE]  
>  Se si desidera creare un'attività da riutilizzare più facilmente con più pacchetti, è possibile utilizzare il codice di questo esempio di attività Script come punto iniziale per un'attività personalizzata. Per altre informazioni, vedere [Sviluppo di un'attività personalizzata](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Descrizione  
 Nell'esempio seguente viene usata una gestione connessione MSMQ esistente, insieme agli oggetti e ai metodi dello spazio dei nomi System.Messaging, per inviare il testo contenuto in una variabile di pacchetto a una coda di messaggi privata remota. La chiamata al metodo M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) della gestione connessione MSMQ restituisce un oggetto **MessageQueue** il cui metodo **Send** porta a termine questa attività.  
  
#### <a name="to-configure-this-script-task-example"></a>Per configurare l'esempio di attività Script  
  
1.  Creare una gestione connessione MSMQ con il nome predefinito. Impostare il percorso di una coda privata remota valida, nel formato seguente:  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  Creare una variabile [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] denominata **MessageText** di tipo **String** per passare il testo del messaggio nello script. Immettere un messaggio predefinito come valore della variabile.  
  
3.  Aggiungere un'attività Script all'area di progettazione e modificarla. Nella scheda **Script** dell'**Editor attività Script** aggiungere la variabile `MessageText` alla proprietà **ReadOnlyVariables** per rendere disponibile la variabile all'interno dello script.  
  
4.  Fare clic su **Modifica script** per aprire l'editor di script di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA).  
  
5.  Aggiungere un riferimento nel progetto di script allo spazio dei nomi **System.Messaging**.  
  
6.  Sostituire il contenuto della finestra dello script con il codice nella sezione seguente.  
  
## <a name="code"></a>Codice  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Message Queue](../../integration-services/control-flow/message-queue-task.md)  
  
  
