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
ms.openlocfilehash: a25a9c376b7443bb23520c26be545c027da0bde6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067363"
---
# <a name="connect-to-an-instance-from-object-explorer"></a>Connettersi a un'istanza da Esplora oggetti
  Per gestire oggetti tramite Esplora oggetti, è necessario connettere Esplora oggetti all'istanza che contiene gli oggetti. È possibile connettere Esplora oggetti a più istanze contemporaneamente.  
  
## <a name="connecting-object-explorer-to-a-server"></a>Connessione di Esplora oggetti a un server  
 Per utilizzare Esplora oggetti, è necessario connettersi innanzitutto a un server. Fare clic su **Connetti** sulla barra degli strumenti Esplora oggetti e selezionare il tipo di server desiderato dall'elenco a discesa. Viene visualizzata la finestra di dialogo **Connetti al server** . Per eseguire la connessione è necessario specificare almeno il nome del server e le informazioni di autenticazione corrette.  
  
## <a name="optional-object-explorer-connection-settings"></a>Impostazioni di connessione facoltative di Esplora oggetti  
 Quando ci si collega a un server è possibile specificare altre informazioni nella finestra di dialogo **Connetti al server**. In **Connetti al server**questa finestra verranno mantenute le ultime impostazioni, che saranno utilizzate per le nuove connessioni, ad esempio per le nuove finestre dell'editor del codice.  
  
 Per specificare impostazioni di connessione facoltative, eseguire la procedura seguente:  
  
1.  Fare clic su **Connetti** sulla barra degli strumenti Esplora oggetti e quindi sul tipo di server al quale collegarsi. Viene visualizzata la finestra di dialogo **Connetti al server** .  
  
2.  Nella casella **Nome server** digitare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Fare clic su **Opzioni**. Nella finestra di dialogo **Connetti al server** verranno visualizzate opzioni aggiuntive.  
  
4.  Fare clic sulla scheda **Proprietà connessione** per configurare le impostazioni aggiuntive. Le impostazioni disponibili variano in base al tipo di server. Per [!INCLUDE[ssDE](../../includes/ssde-md.md)]sono disponibili le opzioni seguenti.  
  
    |Impostazione|Descrizione|  
    |-------------|-----------------|  
    |**Connettersi al database**|Consente di eseguire selezioni dall'elenco dei database disponibili sul server. Questo elenco contiene solo i database che l'utente è autorizzato a visualizzare.|  
    |**Protocollo di rete**|Consente di selezionare tra Shared Memory, TCP/IP o Named pipe.|  
    |**Dimensioni del pacchetto di rete**|La configurazione deve essere espressa in byte. L'impostazione predefinita è 4096 byte.|  
    |**Timeout connessione**|La configurazione deve essere espressa in secondi. L'impostazione predefinita è 15 secondi.|  
    |**Timeout esecuzione**|La configurazione deve essere espressa in secondi. L'impostazione predefinita (0) indica che l'esecuzione non andrà mai in timeout.|  
    |**Crittografa connessione**|Forza la crittografia.|  
  
5.  Per aggiungere il server specificato all'elenco dei server registrati, fare clic sulla scheda **Server registrato** , scegliere la posizione desiderata per il nuovo server e quindi completare la connessione.  
  
> [!NOTE]  
>  Usare la pagina **Parametri aggiuntivi per la connessione** per aggiungere più parametri di connessione alla stringa di connessione. Per altre informazioni, vedere [Connetti al server & #40; pagina Parametri aggiuntivi per la connessione & #41;](../../database-engine/connect-to-server-additional-connection-parameters-page.md).  
  
  
