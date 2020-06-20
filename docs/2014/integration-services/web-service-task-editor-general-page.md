---
title: Editor attività servizio Web (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicestask.general.f1
helpviewer_keywords:
- Web Service Task Editor
ms.assetid: 4d7df283-430d-4f0f-9dd4-5909554cd5eb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 254680ce380b88aca01184bb744a7dde1b8e5611
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972479"
---
# <a name="web-service-task-editor-general-page"></a>Editor attività Servizio Web (pagina Generale)
  Usare la pagina **Generale** della finestra di dialogo **Editor attività Servizio Web** per specificare una gestione connessione HTTP e il percorso del file WSDL (Web Services Description Language) usato dall'attività Servizio Web, descrivere l'attività Servizio Web e scaricare il file WSDL.  
  
 Per altre informazioni su questa attività, vedere [Attività Servizio Web](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opzioni  
 **HTTPConnection**  
 Selezionare una gestione connessione nell'elenco oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
> [!IMPORTANT]  
>  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 **Argomenti correlati: **  [Gestione connessione HTTP](connection-manager/http-connection-manager.md), [Editor gestione connessione HTTP &#40;pagina Server&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Digitare il percorso completo di un file WSDL locale nel computer oppure fare clic sul pulsante Sfoglia **(...)** per individuare il file.  
  
 Sezionare il file WSDL presente nel computer, se è già stato scaricato manualmente. Se invece il file WSDL non è stato ancora scaricato, attenersi alla seguente procedura:  
  
-   Creare un file vuoto con l'estensione di file "wsdl".  
  
-   Selezionare questo file vuoto per l'opzione **WSDLFile** .  
  
-   Impostare il valore di **OverwriteWsdlFile** su `True` per consentire la sovrascrittura del file vuoto con il file WSDL effettivo.  
  
-   Fare clic su **Scarica WSDL** per scaricare il file WSDL effettivo e sovrascrivere il file vuoto.  
  
    > [!NOTE]  
    >  L'opzione **Scarica WSDL** non è abilitato fino a quando non si fornisce il nome di un file locale esistente nella casella **WSDLFile** .  
  
 **OverwriteWSDLFile**  
 Consente di specificare se il file WSDL per l'attività Servizio Web può essere sovrascritto.  
  
 Se si intende scaricare il file WSDL tramite il pulsante **Scarica WSDL** , impostare questo valore su `True` .  
  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Servizio Web. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Servizio Web.  
  
 **Scarica WSDL**  
 Consente di scaricare il file WSDL.  
  
 Questo pulsante non è attivato fino a quando non si fornisce il nome di un file locale esistente nella casella **WSDLFile** .  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività servizio Web &#40;pagina di input&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Editor attività servizio Web &#40;pagina output&#41;](../../2014/integration-services/web-service-task-editor-output-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
