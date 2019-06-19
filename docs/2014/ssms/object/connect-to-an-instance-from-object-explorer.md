---
title: Connettersi a un'istanza da Esplora oggetti | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 9803a8a0-a8f1-4b65-87b8-989b06850194
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 92e3b7b2099aabaa763fb6f6642bcc6267ebe6f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63277424"
---
# <a name="connect-to-an-instance-from-object-explorer"></a>Connettersi a un'istanza da Esplora oggetti
  Per gestire oggetti tramite Esplora oggetti, è necessario connettere Esplora oggetti all'istanza che contiene gli oggetti. È possibile connettere Esplora oggetti a più istanze contemporaneamente.  
  
## <a name="connecting-object-explorer-to-a-server"></a>Connessione di Esplora oggetti a un server  
 Per utilizzare Esplora oggetti, è necessario connettersi innanzitutto a un server. Fare clic su **Connetti** sulla barra degli strumenti Esplora oggetti e selezionare il tipo di server desiderato dall'elenco a discesa. Verrà visualizzata la finestra di dialogo **Connetti al server** . Per eseguire la connessione è necessario specificare almeno il nome del server e le informazioni di autenticazione corrette.  
  
## <a name="optional-object-explorer-connection-settings"></a>Impostazioni di connessione facoltative di Esplora oggetti  
 Quando ci si collega a un server è possibile specificare altre informazioni nella finestra di dialogo **Connetti al server**. In **Connetti al server**questa finestra verranno mantenute le ultime impostazioni, che saranno utilizzate per le nuove connessioni, ad esempio per le nuove finestre dell'editor del codice.  
  
 Per specificare impostazioni di connessione facoltative, eseguire la procedura seguente:  
  
1.  Fare clic su **Connetti** sulla barra degli strumenti Esplora oggetti e quindi sul tipo di server al quale collegarsi. Verrà visualizzata la finestra di dialogo **Connetti al server** .  
  
2.  Nella casella **Nome server** digitare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Fare clic su **Opzioni**. Nella finestra di dialogo **Connetti al server** verranno visualizzate opzioni aggiuntive.  
  
4.  Fare clic sulla scheda **Proprietà connessione** per configurare le impostazioni aggiuntive. Le impostazioni disponibili variano in base al tipo di server. Per [!INCLUDE[ssDE](../../includes/ssde-md.md)]sono disponibili le opzioni seguenti.  
  
    |Impostazione|Descrizione|  
    |-------------|-----------------|  
    |**Connetti al database**|Consente di eseguire selezioni dall'elenco dei database disponibili sul server. Questo elenco contiene solo i database che l'utente è autorizzato a visualizzare.|  
    |**Protocollo di rete**|Consente di selezionare tra Shared Memory, TCP/IP o Named pipe.|  
    |**Dimensioni pacchetto di rete**|La configurazione deve essere espressa in byte. L'impostazione predefinita è 4096 byte.|  
    |**Timeout connessione**|La configurazione deve essere espressa in secondi. L'impostazione predefinita è 15 secondi.|  
    |**Timeout esecuzione**|La configurazione deve essere espressa in secondi. L'impostazione predefinita (0) indica che l'esecuzione non andrà mai in timeout.|  
    |**Crittografia connessione**|Forza la crittografia.|  
  
5.  Per aggiungere il server specificato all'elenco dei server registrati, fare clic sulla scheda **Server registrato** , scegliere la posizione desiderata per il nuovo server e quindi completare la connessione.  
  
> [!NOTE]  
>  Usare la pagina **Parametri aggiuntivi per la connessione** per aggiungere più parametri di connessione alla stringa di connessione. Per altre informazioni, vedere [Connetti al server & #40; pagina Parametri aggiuntivi per la connessione & #41;](../../database-engine/connect-to-server-additional-connection-parameters-page.md).  
  
  
