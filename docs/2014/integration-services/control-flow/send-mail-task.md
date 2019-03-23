---
title: Attività Invia messaggi| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3308899190aa63ebb9be93c4c9af15d5e0f94600
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380129"
---
# <a name="send-mail-task"></a>Invia messaggi - attività
  L'attività Invia messaggi consente di inviare un messaggio di posta elettronica. Tramite l'attività Invia messaggi un pacchetto può inviare messaggi quando le attività nel flusso di lavoro del pacchetto vengono completate o non riescono oppure in risposta a un evento generato dal pacchetto in fase di esecuzione. È ad esempio possibile utilizzare questa attività per notificare all'amministratore di un database l'esito positivo o negativo dell'attività Backup database.  
  
 Per configurare l'attività Invia messaggi, procedere nel modo seguente:  
  
-   Specificare il testo del messaggio di posta elettronica.  
  
-   Specificare l'oggetto del messaggio di posta elettronica.  
  
-   Impostare il livello di priorità del messaggio. L'attività supporta tre livelli di priorità: normale, medio e alto.  
  
-   Specificare i destinatari nelle righe A, Cc e Ccn. Per specificare più destinatari, separarli con punti e virgola.  
  
    > [!NOTE]  
    >  Le righe A, Cc e Ccn presentano il limite di 256 caratteri ognuna, in conformità agli standard Internet.  
  
-   Includere eventuali allegati. Per specificare più allegati, separarli con una barra verticale (|).  
  
    > [!NOTE]  
    >  Se un file allegato non esiste al momento dell'esecuzione del pacchetto, verrà generato un errore.  
  
-   Specificare la gestione connessione SMTP da utilizzare.  
  
    > [!IMPORTANT]  
    >  La gestione connessione SMTP supporta solo l'autenticazione anonima e l'autenticazione di Windows. Non supporta l'autenticazione di base.  
  
 Il testo del messaggio può essere una stringa specificata, una connessione a un file che contiene il testo o il nome di una variabile che contiene il testo. Per connettersi a un file l'attività utilizza una gestione connessione file. Per ulteriori informazioni, vedere [Flat File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 Per connettersi a un server di posta elettronica l'attività utilizza una gestione connessione SMTP. Per altre informazioni, vedere [Gestione connessione SMTP](../connection-manager/smtp-connection-manager.md).  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>Messaggi di registrazione personalizzati disponibili nell'attività Invia messaggi  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività Invia messaggi. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`SendMailTaskBegin`|Indica che l'attività ha iniziato a inviare un messaggio di posta elettronica.|  
|`SendMailTaskEnd`|Indica che l'attività ha terminato l'invio di un messaggio di posta elettronica.|  
|`SendMailTaskInfo`|Offre informazioni descrittive sull'attività.|  
  
## <a name="configuring-the-send-mail-task"></a>Configurazione dell'attività Invia messaggi  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Invia messaggi &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Invia messaggi &#40;pagina Messaggio&#41;](../send-mail-task-editor-mail-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare queste proprietà nella finestra di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md).  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Articolo tecnico relativo all' [invio della posta elettronica con notifica di recapito in C#](https://go.microsoft.com/fwlink/?LinkId=237625)su shareourideas.com  
  
## <a name="see-also"></a>Vedere anche  
 [Attività di Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
