---
title: Gestione connessione HTTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- HTTP connection manager
- Web site connections [Integration Services]
- connection managers [Integration Services], HTTP
- Web server connections [Integration Services]
- connections [Integration Services], HTTP
ms.assetid: 26b2b3e1-d02c-46ca-8d31-7aef2bbc3c53
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f79a882e3a3e4520cb8cfcd4468f3c908b79abf5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833757"
---
# <a name="http-connection-manager"></a>gestione connessione HTTP
  Una connessione HTTP consente a un pacchetto di accedere al server Web utilizzando il protocollo HTTP per l'invio o la ricezione di file. L'attività Servizio Web inclusa in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa questa gestione connessione.  
  
 Quando si aggiunge una gestione connessione HTTP a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione HTTP, imposta le proprietà della gestione connessione e quindi la aggiunge alla raccolta `Connections` del pacchetto.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `HTTP.`  
  
 Per configurare la gestione connessione HTTP, procedere nel modo seguente:  
  
-   Utilizzo di credenziali. Se la gestione connessione utilizza credenziali, le sue proprietà includeranno nome utente, password e dominio.  
  
    > [!IMPORTANT]  
    >  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
-   Utilizzo di un certificato client. Se la gestione connessione utilizza un certificato client, le sue proprietà includeranno il nome del certificato.  
  
-   Specificare il timeout per la connessione al server e le dimensioni del blocco per la scrittura dei dati.  
  
-   Utilizzo di un server proxy. È inoltre possibile configurare il server proxy in modo da utilizzare credenziali e da ignorare il server proxy e utilizzare indirizzi locali.  
  
## <a name="configuration-of-the-http-connection-manager"></a>Configurazione della gestione connessione HTTP  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor gestione connessione HTTP &#40;pagina Server&#41;](../http-connection-manager-editor-server-page.md)  
  
-   [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../http-connection-manager-editor-proxy-page.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di codice, vedere <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Servizio Web](../control-flow/web-service-task.md)   
 [Connessioni in Integration Services &#40;SSIS&#41;](integration-services-ssis-connections.md)  
  
  
