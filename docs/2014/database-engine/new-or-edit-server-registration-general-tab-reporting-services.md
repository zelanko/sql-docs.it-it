---
title: Nuova registrazione o modifica registrazione server (scheda generale) (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: a9892a6fb3033be549d95b708a012e55d40bcb80
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930507"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>Creazione o modifica della registrazione del server (scheda Generale) (Reporting Services)
  Utilizzare questa scheda per specificare le opzioni per la registrazione di un'istanza di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Per accedere a questa pagina, in Server registrati fare clic su **Reporting Services** sulla barra degli strumenti **Server registrati** , fare clic con il pulsante destro del mouse su qualsiasi gruppo di server registrati, ad esempio **Reporting Services**, scegliere **Nuovo**e quindi fare clic su **Nuova registrazione server**.  
  
## <a name="options"></a>Opzioni  
 **Tipo di server**  
 Quando un server viene registrato da server registrati, la casella **tipo server** è di sola lettura e corrisponde al tipo di server visualizzato nel riquadro **Server registrati** . Per registrare un tipo diverso di server, selezionare il server desiderato dalla barra degli strumenti **Server registrati** prima di iniziare la registrazione del nuovo server.  
  
 **Nome server**  
 Consente di selezionare l'istanza del server di report a cui connettersi. In [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]è possibile accedere a un server di report tramite il nome della relativa istanza. È possibile disporre di un'istanza del server di report per ogni istanza di SQL Server installata Se si utilizza l'istanza predefinita, digitare il nome dell'istanza di SQL Server. Se si utilizza un'istanza denominata, indicarla nel formato MSSQL$instancename per la connessione al server di report.  
  
 **autenticazione**  
 Il processo di autenticazione a un server di report viene eseguito tramite Internet Information Services (IIS). Selezionare una delle modalità di autenticazione disponibili seguenti per la connessione a Reporting Services:  
  
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
  
 **Memorizza password**  
 Consente di archiviare la password immessa. Questa opzione è disponibile solo se si è scelto di utilizzare **l'autenticazione di base** o **basata su form**.  
  
> [!NOTE]  
>  Se la password è stata archiviata e si desidera arrestarne la memorizzazione, deselezionare questa casella di controllo e quindi fare clic su **Salva**.  
  
 **Nome server registrato**  
 Nome che si desidera venga visualizzato nel componente Server registrati. Non è necessario che questo nome corrisponda a quello indicato nella casella **Nome server** .  
  
 **Descrizione server registrato**  
 Consente di immettere una descrizione facoltativa del server.  
  
 **Test**  
 Consente di testare la connessione al server selezionato in **Nome server**.  
  
 **Salva**  
 Fare clic su questo pulsante per salvare le impostazioni del server registrato.  
  
  
