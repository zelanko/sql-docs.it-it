---
title: Editor attività Message Queue (pagina invio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msgqueuetask.send.f1
helpviewer_keywords:
- Message Queue Task Editor
ms.assetid: 565aa079-ac44-4407-8efc-cddab839de30
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7c78b6665e761b0ffa9da4a4abcefc2489bff07a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424688"
---
# <a name="message-queue-task-editor-send-page"></a>Editor attività Message Queue (pagina Invio)
  Usare la pagina **Invio** della finestra di dialogo **Editor attività Message Queue** per configurare un'attività Message Queue per l'invio di messaggi da un pacchetto di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
 Per ulteriori informazioni su questa attività, vedere [Message Queue Task](control-flow/message-queue-task.md).  
  
## <a name="options"></a>Opzioni  
 **UseEncryption**  
 Consente di indicare se crittografare il messaggio. Il valore predefinito è `False`.  
  
 **EncryptionAlgorithm**  
 Se si sceglie di utilizzare la crittografia, consente di specificare il nome dell'algoritmo di crittografia da utilizzare. L'attività Message Queue può utilizzare gli algoritmi RC2 e RC4. L'impostazione predefinita è **RC2**.  
  
> [!NOTE]  
>  L'algoritmo RC4 è supportato solo per motivi di compatibilità con le versioni precedenti. È possibile crittografare il nuovo materiale usando RC4 o RC4_128 solo quando il livello di compatibilità del database è 90 o 100. (Non consigliato.) Usare un algoritmo più recente, ad esempio uno degli algoritmi AES. Nella versione corrente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]il materiale crittografato utilizzando RC4 o RC4_128 può essere decrittografato in qualsiasi livello di compatibilità.  
  
> [!IMPORTANT]  
>  Questi algoritmi di crittografia sono quelli supportati dalla tecnologia Microsoft Message Queuing (nota anche come MSMQ). Entrambi gli algoritmi di crittografia sono ormai considerati vulnerabili rispetto ad altri più recenti che tuttavia non sono ancora supportati da MSMQ. È pertanto consigliabile valutare con attenzione le esigenze di crittografia ai fini dell'invio di messaggi tramite l'attività Message Queue.  
  
 **MessageType**  
 Consente di selezionare il tipo di messaggio. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Messaggio file di dati**|Il messaggio viene archiviato in un file. La selezione del valore determina la visualizzazione dell'opzione dinamica **DataFileMessage**.|  
|**Messaggio variabili**|Il messaggio viene archiviato in una variabile. La selezione del valore determina la visualizzazione dell'opzione dinamica **VariableMessage**.|  
|**Messaggio stringa**|Il messaggio viene archiviato nell'attività Message Queue. La selezione del valore determina la visualizzazione dell'opzione dinamica **StringMessage**.|  
  
## <a name="messagetype-dynamic-options"></a>Opzioni dinamiche di MessageType  
  
### <a name="messagetype--data-file-message"></a>MessageType = Messaggio file di dati  
 **DataFileMessage**  
 Digitare il percorso del file di dati oppure fare clic sui puntini di sospensione **(...)** e quindi individuare il file.  
  
### <a name="messagetype--variable-message"></a>MessageType = Messaggio variabili  
 **VariableMessage**  
 Digitare i nomi delle variabili oppure fare clic sui puntini di sospensione **(...)** e quindi selezionare le variabili. Le variabili sono separate da virgole.  
  
 **Argomenti correlati:** Seleziona variabili  
  
### <a name="messagetype--string-message"></a>MessageType = Messaggio stringa  
 **StringMessage**  
 Digitare il messaggio stringa oppure fare clic sui puntini di sospensione **(...)** e quindi digitare il messaggio nella finestra di dialogo **Immetti messaggio stringa** .  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Message Queue &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor attività Message Queue &#40;pagina ricezione&#41;](../../2014/integration-services/message-queue-task-editor-receive-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
