---
title: Attività Message Queue | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.messagequeuetask.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1b144e8e3ca5bcf96b588e8579dcdb52faa9e4f9
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360923"
---
# <a name="message-queue-task"></a>Message Queue Task
  L'attività Message Queue consente di usare Microsoft Message Queuing (noto anche come MSMQ) per scambiare messaggi tra pacchetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o per inviare messaggi a una coda di applicazione elaborata da un'applicazione personalizzata. I messaggi possono essere in forma di testo semplice, di file o di variabili con i rispettivi valori.  
  
 Tramite l'attività Message Queue è possibile coordinare operazioni nell'intera azienda. Se la destinazione è occupata o non disponibile, i messaggi possono essere messi in coda e recapitati in un secondo tempo. L'attività può ad esempio mettere in coda i messaggi destinati ai computer portatili offline dei rappresentanti, che li riceveranno quando si connetteranno alla rete. È possibile utilizzare l'attività Message Queue per gli scopi seguenti:  
  
-   Ritardare l'esecuzione dell'attività fino all'archiviazione di altri pacchetti. Si supponga ad esempio che, al termine della manutenzione notturna in ogni filiale dell'azienda, un'attività Message Queue invii un messaggio al computer della sede centrale e che in tale computer sia in esecuzione un pacchetto contenente varie attività Message Queue, ognuna delle quali in attesa del messaggio di una filiale specifica. Alla ricezione di un messaggio dalla filiale corrispondente, l'attività carica i dati dal computer della filiale. Al termine dell'archiviazione da parte di tutte le filiali, il pacchetto calcola i totali riepilogativi.  
  
-   Inviare file di dati al computer responsabile della loro elaborazione. L'output del registratore di cassa di un ristorante, ad esempio, può essere inviato in un messaggio di tipo file di dati al sistema di paghe della sede centrale, che estrae i dati relativi alle mance dei singoli camerieri.  
  
-   Distribuire file in tutta l'azienda. È ad esempio possibile utilizzare l'attività Message Queue per inviare il file di un pacchetto a un altro computer, dove è presente un pacchetto in esecuzione che utilizza un'attività Message Queue per recuperare e salvare il pacchetto localmente.  
  
 Per inviare o ricevere messaggi, l'attività Message Queue utilizza uno dei tipi di messaggi seguenti: file di dati, stringa, messaggio stringa in variabile o variabile. I messaggi di tipo messaggio stringa in variabile possono essere utilizzati solo per la ricezione di messaggi.  
  
 Per connettersi a una coda di messaggi l'attività utilizza una gestione connessione MSMQ. Per altre informazioni, vedere [Gestione connessione MSMQ](../connection-manager/msmq-connection-manager.md). Per altre informazioni su Microsoft Message Queuing, vedere [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022).  
  
 Affinché sia possibile usare l'attività Message Queue, è necessario avere installato il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Alcuni dei componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile selezionare per l'installazione nella pagina **Componenti da installare** o **Selezione funzionalità** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installano solo un subset parziale dei componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tali componenti si rivelano utili per attività specifiche, ma le funzionalità di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] risulteranno limitate. L'opzione [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , ad esempio, installa i componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] necessari per la progettazione dei pacchetti, ma il servizio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non viene installato e l'attività Message Queue non è disponibile. Per garantire l'installazione completa di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è necessario selezionare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nella pagina **Componenti da installare** . Per altre informazioni sull'installazione e l'esecuzione dell'attività Message Queue, vedere [Installazione di Integration Services](../install-windows/install-integration-services.md).  
  
> [!NOTE]  
>  L'attività Message Queue ha esito negativo in conformità con lo standard FIPS (Federal Information Processing Standard) 140-2 se il sistema operativo del computer è configurato in modalità FIPS e l'attività utilizza la crittografia. Se non viene utilizzata la crittografia, l'attività Message Queue viene eseguita correttamente.  
  
## <a name="message-types"></a>Tipi di messaggi  
 Per configurare i tipi di messaggi disponibili per l'attività Message Queue, procedere nel modo seguente:  
  
-   Il tipo di messaggio `Data file` specifica che il messaggio è contenuto in un file. Per quanto riguarda la ricezione dei messaggi, è possibile configurare l'attività in modo da salvare il file, sovrascrivere un file esistente e specificare il pacchetto da cui l'attività può ricevere messaggi.  
  
-   Il tipo di messaggio `String` specifica che il messaggio è una stringa. Per quanto riguarda la ricezione dei messaggi, è possibile configurare l'attività in modo da confrontare la stringa ricevuta con una stringa definita dall'utente ed eseguire un'azione che dipende dal risultato del confronto. Il confronto tra le stringhe può essere esatto, con o senza distinzione tra maiuscole e minuscole oppure utilizzare una sottostringa.  
  
-   Il tipo di messaggio `String message to variable` specifica che l'origine del messaggio è una stringa che viene inviata a una variabile di destinazione. È possibile configurare l'attività in modo da confrontare la stringa ricevuta con una stringa definita dall'utente, utilizzando un confronto esatto, senza distinzione tra maiuscole e minuscole o tra sottostringhe. Questo tipo di messaggio è disponibile solo quando l'attività riceve messaggi.  
  
-   Il tipo di messaggio `Variable` specifica che il messaggio contiene una o più variabili. È possibile configurare l'attività in modo da specificare i nomi delle variabili incluse nel messaggio. Per quanto riguarda la ricezione dei messaggi, è possibile configurare l'attività in modo da specificare sia il pacchetto da cui può ricevere messaggi, sia la variabile che costituisce la destinazione del messaggio.  
  
## <a name="sending-messages"></a>sending messages  
 Quando si configura l'attività Message Queue per l'invio di messaggi, per crittografare i messaggi è possibile utilizzare uno degli algoritmi di crittografia attualmente supportati dalla tecnologia MSMQ, ovvero RC2 e RC4. Entrambi questi algoritmi di crittografia sono attualmente considerati vulnerabili rispetto ad algoritmi più recenti non ancora supportati dalla tecnologia MSMQ. È pertanto consigliabile valutare con attenzione le esigenze di crittografia ai fini dell'invio di messaggi tramite l'attività Message Queue.  
  
## <a name="receiving-messages"></a>ricezione di messaggi  
 Per quanto riguarda la ricezione di messaggi, è possibile configurare l'attività Message Queue in modo da:  
  
-   Ignorare il messaggio ricevuto oppure rimuoverlo dalla coda.  
  
-   Specificare un timeout.  
  
-   Generare un errore in caso di timeout.  
  
-   Sovrascrivere un file esistente, se il messaggio è archiviato in un `Data file`.  
  
-   Salvare il file del messaggio con un nome di file diverso, se il messaggio è di tipo `Data file message`.  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>Messaggi di registrazione personalizzati disponibili nell'attività Message Queue  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Message Queue. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`MSMQAfterOpen`|Indica che l'attività ha terminato l'apertura della coda di messaggi.|  
|`MSMQBeforeOpen`|Indica che l'attività ha iniziato ad aprire la coda di messaggi.|  
|`MSMQBeginReceive`|Indica che l'attività ha iniziato a ricevere un messaggio.|  
|`MSMQBeginSend`|Indica che l'attività ha iniziato a inviare un messaggio.|  
|`MSMQEndReceive`|Indica che l'attività ha terminato la ricezione di un messaggio.|  
|`MSMQEndSend`|Indica che l'attività ha terminato l'invio di un messaggio.|  
|`MSMQTaskInfo`|Offre informazioni descrittive sull'attività.|  
|`MSMQTaskTimeOut`|Indica che si è verificato il timeout dell'attività.|  
  
## <a name="configuration-of-the-message-queue-task"></a>Configurazione dell'attività Message Queue  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice. Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Message Queue &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Message Queue &#40;pagina Ricezione&#41;](../message-queue-task-editor-receive-page.md)  
  
-   [Editor attività Message Queue &#40;pagina Invio&#41;](../message-queue-task-editor-send-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione a livello di programmazione di queste proprietà, vedere la documentazione per la classe **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** nella Guida per gli sviluppatori.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni su come impostare queste proprietà nella finestra di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
