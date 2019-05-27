---
title: Editor attività FTP (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.general.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 28b46fdd-b04a-4f97-a99f-883f5735a6d9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ad2605902cb523c0147888e4aedee0df3c9f936e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058426"
---
# <a name="ftp-task-editor-general-page"></a>Editor attività FTP (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor attività FTP** per specificare la gestione connessione FTP tramite cui viene stabilita la connessione al server FTP con cui comunica l'attività. È inoltre possibile specificare un nome e una descrizione per l'attività FTP.  
  
 Per altre informazioni su questa attività, vedere [FTP Task](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opzioni  
 **FtpConnection**  
 Consente di selezionare una gestione connessione FTP esistente o di creare una gestione connessione facendo clic su \<**Nuova connessione**>.  
  
> [!IMPORTANT]  
>  La gestione connessione FTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 **Argomenti correlati**: [Gestione connessione FTP](connection-manager/ftp-connection-manager.md), [Editor gestione connessione FTP](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 Consente di specificare il termine dell'attività FTP in caso di esito negativo di un'operazione FTP.  
  
 **Name**  
 Consente di specificare un nome univoco per l'attività FTP. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività FTP.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività FTP &#40;pagina Trasferimento file&#41;](../../2014/integration-services/ftp-task-editor-file-transfer-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
