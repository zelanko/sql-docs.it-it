---
title: Connetti al server (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 18afc2a57f4e86417f4228baa459117f1dc7f7a2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934592"
---
# <a name="connect-to-server-reporting-services"></a>Connetti al server (Reporting Services)
  Usare questa finestra di dialogo per visualizzare o specificare le opzioni per la connessione a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
 **Tipo di server**  
 Quando si registra un server da **Esplora oggetti**, selezionare il tipo di server a cui connettersi: [!INCLUDE[ssDE](../includes/ssde-md.md)] , Analysis Services, Reporting Services o Integration Services. Nelle altre parti della finestra di dialogo vengono visualizzate solo le opzioni applicabili al tipo di server selezionato. Quando si registra un server da **Server registrati**, la casella **tipo server** è di sola lettura e corrisponde al tipo di server visualizzato nel componente **Server registrati** . Per registrare un tipo diverso di server, selezionare [!INCLUDE[ssDE](../includes/ssde-md.md)] , Analysis Services, Reporting Services o Integration Services dalla barra degli strumenti **Server registrati** prima di avviare la registrazione di un nuovo server.  
  
 **Nome server**  
 La modalità server dell'istanza del server di report a cui ci si connette determina il valore che è necessario immettere.  
  
 Per un server di report in esecuzione in modalità nativa, specificare l'istanza del server di report a cui connettersi. Se si utilizza l'istanza predefinita, il nome del server corrisponde in genere al nome del computer. Se è stata installata un'istanza denominata, aggiungere il nome dell'istanza al nome del server nel formato: \<servername> \\<NomeIstanza \> . Reporting Services utilizza il carattere barra rovesciata per delimitare il nome dell'istanza.  
  
 Per un server di report in esecuzione in modalità integrata SharePoint, è necessario specificare un sito di SharePoint. È possibile specificare qualsiasi sito di una raccolta siti integrata con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. L'URL specificato deve includere il prefisso HTTP o HTTPS. Per connettersi al sito in Management Studio, è necessario disporre delle autorizzazioni necessarie per accedere al sito di SharePoint. Il livello di autorizzazione assegnato determinerà gli elementi che è possibile visualizzare e gestire. Per altre informazioni, vedere [Eseguire la connessione a un server di report in Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
 **autenticazione**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] può essere configurato per accettare richieste di autenticazione di Windows o richieste di autenticazione basata su form gestite da un'estensione di autenticazione personalizzata definita. Selezionare una delle modalità di autenticazione seguenti per la connessione a [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
 **Modalità di autenticazione di Windows (Autenticazione di Windows)**  
 Consente di connettersi a un'istanza del server di report tramite le credenziali di [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Autenticazione base**  
 Consente di connettersi mediante la modalità di **Autenticazione di base** se l'installazione di Reporting Services è configurata per usarla.  
  
 **Autenticazione basata su form**  
 Consente di connettersi mediante la modalità **Autenticazione basata su form** se l'installazione di Reporting Services è configurata per usare un'estensione di autenticazione personalizzata.  
  
 **Nome utente**  
 Immettere il nome account di accesso da utilizzare per la connessione. Questa opzione è disponibile solo se si è scelto di utilizzare **l'autenticazione di base** o **basata su form**.  
  
 **Password**  
 Immettere il nome utente e la password Questa opzione può essere modificata solo se si è scelto di utilizzare **l'autenticazione di base** o **basata su form**.  
  
 **Connettere**  
 Fare clic su questo pulsante per connettersi al server selezionato.  
  
 **Opzioni**  
 Fare clic su questo pulsante per visualizzare ulteriori opzioni per la connessione al server, come le opzioni per la registrazione di un server e la memorizzazione della password.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare una connessione al database del server di report &#40;Configuration Manager SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Connettersi a un server di report in Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Autenticazione con il server di report](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
