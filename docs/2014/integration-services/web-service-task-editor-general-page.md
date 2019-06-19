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
manager: craigg
ms.openlocfilehash: c6f993f1f2386782bf8225f22b285b9385e2f8e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054536"
---
# <a name="web-service-task-editor-general-page"></a>Editor attività Servizio Web (pagina Generale)
  Usare la pagina **Generale** della finestra di dialogo **Editor attività Servizio Web** per specificare una gestione connessione HTTP e il percorso del file WSDL (Web Services Description Language) usato dall'attività Servizio Web, descrivere l'attività Servizio Web e scaricare il file WSDL.  
  
 Per altre informazioni su questa attività, vedere [Attività Servizio Web](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opzioni  
 **HTTPConnection**  
 Selezionare una gestione connessione nell'elenco oppure crearne una nuova facendo clic su \<**Nuova connessione**>.  
  
> [!IMPORTANT]  
>  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 **Argomenti correlati:**  [Gestione connessione HTTP](connection-manager/http-connection-manager.md), [Editor gestione connessione HTTP &#40;pagina Server&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)  
  
 **WSDLFile**  
 Digitare il percorso completo di un file WSDL presente in locale nel computer oppure fare clic sul pulsante sfoglia **(...)** e individuare il file.  
  
 Sezionare il file WSDL presente nel computer, se è già stato scaricato manualmente. Se invece il file WSDL non è stato ancora scaricato, attenersi alla seguente procedura:  
  
-   Creare un file vuoto con l'estensione di file "wsdl".  
  
-   Selezionare questo file vuoto per l'opzione **WSDLFile** .  
  
-   Impostare il valore della **OverwriteWSDLFile** a `True` per consentire al file vuoto di essere sovrascritto con il file WSDL effettivo.  
  
-   Fare clic su **Scarica WSDL** per scaricare il file WSDL effettivo e sovrascrivere il file vuoto.  
  
    > [!NOTE]  
    >  L'opzione **Scarica WSDL** non è abilitato fino a quando non si fornisce il nome di un file locale esistente nella casella **WSDLFile** .  
  
 **OverwriteWSDLFile**  
 Consente di specificare se il file WSDL per l'attività Servizio Web può essere sovrascritto.  
  
 Se si intende scaricare il file WSDL tramite il **Scarica WSDL** pulsante, impostare questo valore su `True`.  
  
 **Name**  
 Consente di specificare un nome univoco per l'attività Servizio Web. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Servizio Web.  
  
 **Scarica WSDL**  
 Consente di scaricare il file WSDL.  
  
 Questo pulsante non è attivato fino a quando non si fornisce il nome di un file locale esistente nella casella **WSDLFile** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Servizio Web &#40;pagina Input&#41;](../../2014/integration-services/web-service-task-editor-input-page.md)   
 [Editor attività Servizio Web &#40;pagina Output&#41;](../../2014/integration-services/web-service-task-editor-output-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
