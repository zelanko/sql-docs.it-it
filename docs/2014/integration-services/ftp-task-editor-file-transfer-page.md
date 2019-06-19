---
title: Editor attività FTP (pagina trasferimento File) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9386070902022e29ba191f24eb8fbfb10ed92b9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058443"
---
# <a name="ftp-task-editor-file-transfer-page"></a>Editor attività FTP (pagina Trasferimento file)
  Usare la pagina **Trasferimento file** della finestra di dialogo **Editor attività FTP** per configurare l'operazione FTP eseguita dall'attività.  
  
 Per altre informazioni su questa attività, vedere [Attività FTP](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opzioni  
 **IsRemotePathVariable**  
 Consente di specificare se il percorso remoto è archiviato in una variabile. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**True**|Il percorso di destinazione è archiviato in una variabile. Selezionando il valore viene visualizzata l'opzione dinamica **RemoteVariable**.|  
|**False**|Il percorso di destinazione è specificato in una gestione connessione file. Selezionando il valore viene visualizzata l'opzione dinamica **RemotePath**.|  
  
 **OverwriteFileAtDestination**  
 Consente di specificare se è possibile sovrascrivere un file nella destinazione.  
  
 **IsLocalPathVariable**  
 Consente di specificare se il percorso locale è archiviato in una variabile. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**True**|Il percorso di destinazione è archiviato in una variabile. Selezionando il valore viene visualizzata l'opzione dinamica **LocalVariable**.|  
|**False**|Il percorso di destinazione è specificato in una gestione connessione file. Selezionando il valore viene visualizzata l'opzione dinamica **LocalPath**.|  
  
 **Operazione**  
 Consente di selezionare l'operazione FTP da eseguire. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Invia file**|Consente di inviare i file. Selezionando questo valore vengono visualizzate le opzioni dinamiche **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath**.|  
|**Ricevi file**|Consente di ricevere i file. Selezionando questo valore vengono visualizzate le opzioni dinamiche **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath**.|  
|**Crea directory locale**|Consente di creare una directory locale. Selezionando questo valore vengono visualizzate le opzioni dinamiche **LocalVariable** e **LocalPath**.|  
|**Crea directory remota**|Consente di creare una directory remota. Selezionando questo valore vengono visualizzate le opzioni dinamiche **RemoteVariable** e **RemotelPath**.|  
|**Rimuovi directory locale**|Consente di rimuovere una directory locale. Selezionando questo valore vengono visualizzate le opzioni dinamiche **LocalVariable** e **LocalPath**.|  
|**Rimuovi directory remota**|Consente di rimuovere una directory remota. Selezionando questo valore vengono visualizzate le opzioni dinamiche **RemoteVariable** e **RemotePath**.|  
|**Elimina file locali**|Consente di eliminare file locali. Selezionando questo valore vengono visualizzate le opzioni dinamiche **LocalVariable** e **LocalPath**.|  
|**Elimina file remoti**|Consente di eliminare file remoti. Selezionando questo valore vengono visualizzate le opzioni dinamiche **RemoteVariable** e **RemotePath**.|  
  
 **IsTransferASCII**  
 Consente di specificare se i file ricevuti e inviati dal server FTP remoto devono essere trasferiti in modalità ASCII.  
  
## <a name="isremotepathvariable-dynamic-options"></a>Opzioni dinamiche di IsRemotePathVariable  
  
### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **RemoteVariable**  
 Consente di selezionare una variabile esistente definita dall'utente o di creare una variabile definita dall'utente facendo clic su \<**Nuova variabile**>.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), Aggiungere una variabile  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 Consente di selezionare una gestione connessione FTP esistente o di creare una gestione connessione facendo clic su \<**Nuova connessione**>.  
  
 **Argomenti correlati:** [Gestione connessione FTP](connection-manager/ftp-connection-manager.md), [Editor gestione connessione FTP](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>Opzioni dinamiche di IsLocalPathVariable  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 Consente di selezionare una variabile esistente definita dall'utente o di creare una variabile facendo clic su \<**Nuova variabile**>.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), Aggiungere una variabile  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 Selezionare una gestione connessione file esistente oppure crearne una nuova facendo clic su \<**Nuova connessione**>.  
  
 **Argomenti correlati**: [Gestione connessione File flat](connection-manager/file-connection-manager.md), [Editor gestione connessione File](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività FTP &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
