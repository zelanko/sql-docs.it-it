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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 381493758306e3f7c638f46f7c331f0e6cc3e83f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425318"
---
# <a name="ftp-task-editor-general-page"></a>Editor attività FTP (pagina Generale)
  Utilizzare la pagina **Generale** della finestra di dialogo **Editor attività FTP** per specificare la gestione connessione FTP tramite cui viene stabilita la connessione al server FTP con cui comunica l'attività. È inoltre possibile specificare un nome e una descrizione per l'attività FTP.  
  
 Per altre informazioni su questa attività, vedere [FTP Task](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opzioni  
 **FtpConnection**  
 Selezionare una gestione connessione FTP esistente oppure fare clic su \<**New connection...**> per creare una gestione connessione.  
  
> [!IMPORTANT]  
>  La gestione connessione FTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 **Argomenti correlati**: [FTP Connection Manager](connection-manager/ftp-connection-manager.md), [FTP Connection Manager Editor](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 Consente di specificare il termine dell'attività FTP in caso di esito negativo di un'operazione FTP.  
  
 **Nome**  
 Consente di specificare un nome univoco per l'attività FTP. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività FTP.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività FTP &#40;pagina trasferimento file&#41;](../../2014/integration-services/ftp-task-editor-file-transfer-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
