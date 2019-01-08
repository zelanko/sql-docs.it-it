---
title: Proprietà database di distribuzione, Server di pubblicazione | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.distproperties.publishers.f1
helpviewer_keywords:
- Distributor Properties dialog box
ms.assetid: 31c81898-11ca-4d2f-afea-2fbc71e19ce4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9ee329a923bf0b3c3c08b23fb6071a773dc16400
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816443"
---
# <a name="distributor-properties-publishers"></a>Proprietà server di distribuzione, Server di pubblicazione
  La pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione** consente di abilitare l'utilizzo del server di distribuzione corrente da parte dei server di pubblicazione. È inoltre possibile impostare le proprietà associate a tali server di pubblicazione. Tenere presente che, se si abilita un server di pubblicazione per l'utilizzo di questo server come server di distribuzione remoto, il server non diventerà un server di pubblicazione. È infatti necessario connettersi al server di pubblicazione, configurarlo per la pubblicazione e selezionare questo server come server di distribuzione. Utilizzando la Creazione guidata nuova pubblicazione è possibile configurare il server di pubblicazione e selezionare un server di distribuzione.  
  
## <a name="options"></a>Opzioni  
 **Server di pubblicazione**  
 Consente di selezionare i server autorizzati all'utilizzo del server di distribuzione corrente. Per visualizzare e impostare proprietà aggiuntive fare clic sul pulsante delle proprietà ( **...** ) accanto a un server di pubblicazione.  
  
 **Aggiungi**  
 Se il server desiderato non è incluso nell'elenco, fare clic su **Aggiungi** per aggiungere un server di pubblicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Oracle all'elenco dei server di pubblicazione disponibili. Se il server aggiunto è il primo server a utilizzare il server di distribuzione corrente come server di distribuzione remoto, viene richiesto di digitare una password per il collegamento amministrativo.  
  
 **Password per collegamento amministrativo**  
 Utilizzare questa opzione per specificare o aggiornare la password per la connessione che la replica stabilisce tra il server di pubblicazione e il server di distribuzione remoto utilizzando l'account di accesso **distributor_admin** :  
  
-   Se il server di distribuzione viene utilizzato solo come server di distribuzione locale, tale password viene generata in modo casuale e viene configurata automaticamente.  
  
-   Se il server di distribuzione viene utilizzato già da un server di pubblicazione remoto, una password è stata specificata inizialmente in questa pagina o nella pagina **Password server di distribuzione** della Configurazione guidata distribuzione.  
  
-   Se si tratta del primo server di pubblicazione abilitato per il server di distribuzione corrente viene richiesto di digitare una password.  
  
 Per altre informazioni sulla sicurezza dei database di distribuzione, vedere [Proteggere il database di distribuzione](security/secure-the-distributor.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](configure-distribution.md)   
 [Configurare la pubblicazione e la distribuzione](configure-publishing-and-distribution.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](view-and-modify-distributor-and-publisher-properties.md)  
  
  
