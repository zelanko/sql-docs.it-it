---
title: Editor gestione connessione HTTP (pagina Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.httpconnection.server.f1
helpviewer_keywords:
- HTTP Connection Manager Editor
ms.assetid: 774778a0-ece6-4971-b93f-b121d8fc1fc1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3694eeb93e9edbc053a8534841a1edf438489ca9
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968331"
---
# <a name="http-connection-manager-editor-server-page"></a>Editor gestione connessione HTTP (pagina Server)
  La scheda **Server** della finestra di dialogo **Editor gestione connessione HTTP** consente di configurare la gestione connessione HTTP specificando proprietà quali l'URL e le credenziali di sicurezza. Una connessione HTTP consente a un pacchetto di accedere al server Web utilizzando il protocollo HTTP per l'invio o la ricezione di file. Dopo aver configurato la gestione connessione HTTP sarà inoltre possibile verificare la connessione.  
  
> [!IMPORTANT]  
>  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 Per ulteriori informazioni sulla gestione connessione HTTP, vedere [HTTP Connection Manager](connection-manager/http-connection-manager.md). Per ulteriori informazioni su uno scenario di utilizzo comune della gestione connessione HTTP, vedere [Web Service Task](control-flow/web-service-task.md).  
  
## <a name="options"></a>Opzioni  
 **URL server**  
 Digitare l'URL per il server.  
  
 Se si intende utilizzare il pulsante **Scarica WSDL** nella pagina **Generale** di **Editor attività Servizio Web** per scaricare un file WSDL, digitare l'URL del file WSDL. L'URL termina con "?wsdl".  
  
 **Usa credenziali**  
 Consente di specificare se si desidera che per la gestione connessione HTTP vengano utilizzate le credenziali di sicurezza dell'utente per l'autenticazione.  
  
 **Nome utente**  
 Se per la gestione connessione HTTP è stato impostato l'utilizzo di credenziali, è necessario specificare nome utente, password e dominio.  
  
 **Password**  
 Se per la gestione connessione HTTP è stato impostato l'utilizzo di credenziali, è necessario specificare nome utente, password e dominio.  
  
 **Dominio**  
 Se per la gestione connessione HTTP è stato impostato l'utilizzo di credenziali, è necessario specificare nome utente, password e dominio.  
  
 **Usa certificato client**  
 Consente di specificare se si desidera che per la gestione connessione HTTP venga utilizzato un certificato client per l'autenticazione.  
  
 **Certificate**  
 Consente di selezionare un certificato nell'elenco usando la finestra di dialogo **Seleziona certificato** . Nella casella di testo viene visualizzato il nome associato al certificato.  
  
 **Timeout (in secondi)**  
 Consente di fornire un valore di timeout per la connessione al server Web. Il valore predefinito di questa proprietà è 30 secondi.  
  
 **Dimensioni blocco (in KB)**  
 Consente di specificare le dimensioni del blocco per la scrittura dei dati.  
  
 **Test connessione**  
 Dopo aver configurato la gestione connessione HTTP, fare clic su **Test connessione**per assicurarsi che la connessione sia operativa.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)  
  
  
