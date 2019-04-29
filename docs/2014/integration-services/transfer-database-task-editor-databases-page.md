---
title: Editor attività Trasferisci Database (pagina database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 05a7b731ff6befc293b4779eb604ae15d04c0cb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62927214"
---
# <a name="transfer-database-task-editor-databases-page"></a>Editor attività Trasferisci database (pagina Database)
  Utilizzare la pagina **Database** della finestra di dialogo **Editor attività Trasferisci database** per specificare le proprietà relative ai database di origine e destinazione interessati dall'attività Trasferisci database. Questa attività consente di copiare o spostare un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tra due istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], Tramite questa attività è inoltre possibile copiare un database all'interno dello stesso server. Per altre informazioni su questa attività, vedere [Attività Trasferisci database](control-flow/transfer-database-task.md).  
  
## <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **\<Nuova connessione...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **Nuova connessione...>\<** per creare una nuova connessione al server di destinazione.  
  
 **DestinationDatabaseName**  
 Specificare il nome del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel server di destinazione.  
  
 Per inserire automaticamente il nome del database di origine in questo campo, specificare innanzitutto **SourceConnection** e **SourceDatabaseName** .  
  
 Per rinominare il database nel server di destinazione, digitare il nuovo nome in questo campo.  
  
 **DestinationDatabaseFiles**  
 Indica i nomi e i percorsi dei file di database nel server di destinazione.  
  
 Per inserire automaticamente i nomi e i percorsi dei file del database di origine in questo campo, specificare innanzitutto **SourceConnection**, **SourceDatabaseName**e **SourceDatabaseFiles** .  
  
 Per rinominare i file di database o specificare i nuovi percorsi nel server di destinazione, inserire in questo campo le informazioni sul database di origine e quindi fare clic sul pulsante Sfoglia. Nella finestra di dialogo **File di database di destinazione** modificare **File di destinazione**, **Cartella di destinazione**o **Condivisione file di rete**.  
  
> [!NOTE]  
>  Se i file di database vengono individuati tramite il pulsante Sfoglia, il percorso dei file viene immesso usando l'annotazione dell'unità locale, ad esempio c:\\. È necessario sostituire questa annotazione con quella di condivisione di rete, includendo il nome del computer e il nome di condivisione. In caso di condivisione amministrativa predefinita, è necessario utilizzare l'annotazione $ e disporre di accesso amministrativo alla condivisione.  
  
 **DestinationOverwrite**  
 Indicare se il database nel server di destinazione può essere sovrascritto.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**True**|Sovrascrive il database del server di destinazione.|  
|**False**|Non sovrascrive il database del server di destinazione.|  
  
> [!CAUTION]  
>  Se si specifica **True** per la proprietà **DestinationOverwrite**, i dati inclusi nel database del server di destinazione verranno sovrascritti ed è possibile che si verifichi una perdita di dati. Per evitare che i dati vadano perduti, procedere a un backup del database del server di destinazione in un'altra posizione prima di eseguire l'attività Trasferisci database.  
  
 **Azione**  
 Indicare se l'attività eseguirà il comando **Copia** o **Sposta** il database nel server di destinazione.  
  
 **Metodo**  
 Indicare se l'attività deve essere eseguita quando il database nel server di origine è in modalità online o offline.  
  
 Per trasferire un database in modalità offline, l'utente che esegue il pacchetto deve essere un membro del ruolo predefinito del server **sysadmin** .  
  
 Per trasferire un database in modalità online, l'utente che esegue il pacchetto deve essere un membro del ruolo predefinito del server **sysadmin** o il proprietario (**dbo**) del database selezionato.  
  
 **SourceDatabaseName**  
 Selezionare il nome del database da copiare o spostare.  
  
 **SourceDatabaseFiles**  
 Fare clic sul pulsante Sfoglia per selezionare i file di database.  
  
 **ReattachSourceDatabase**  
 Indicare se l'attività tenterà di ricollegare il database di origine in caso di errore.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**True**|Ricollega il database di origine.|  
|**False**|Non ricollega il database di origine.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Attività di Integration Services](control-flow/integration-services-tasks.md)   
 [Editor attività Trasferisci database &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Gestione connessione SMO](connection-manager/smo-connection-manager.md)  
  
  
