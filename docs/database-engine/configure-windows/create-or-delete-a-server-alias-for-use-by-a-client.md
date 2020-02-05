---
title: Creare o eliminare un alias server per l'uso da parte di un client | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- server alias
helpviewer_keywords:
- aliases [SQL Server], deleting
- aliases [SQL Server], creating
ms.assetid: b687e376-ee33-470d-b65a-87246bfefe6f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a0a678d3b5df450377517bc9c94d3771c45f22e0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012076"
---
# <a name="create-or-delete-a-server-alias-for-use-by-a-client"></a>Creare o eliminare un alias server per l'uso da parte di un client
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come creare o eliminare un alias del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando Gestione configurazione SQL Server. Un alias rappresenta un nome alternativo che può essere utilizzato per stabilire una connessione. L'alias incapsula gli elementi necessari di una stringa di connessione e li espone con un nome scelto dall'utente. Gli alias possono essere utilizzati con qualsiasi applicazione client. Grazie alla creazione di alias server, il computer client può connettersi a più server utilizzando protocolli di rete diversi, senza dover specificare ogni volta i dettagli relativi al protocollo e alla connessione. È inoltre possibile disporre di più protocolli di rete abilitati simultaneamente, anche se è necessario utilizzarli solo occasionalmente. Se il server è stato configurato per restare in attesa su una named pipe o un numero di porta non predefinito ed è stato disabilitato il servizio SQL Server Browser, creare un alias per specificare il nuovo numero di porta o la nuova named pipe.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di Gestione configurazione SQL Server  
  
#### <a name="to-create-an-alias"></a>Per creare un alias  
  
1.  In Gestione configurazione SQL Server espandere **Configurazione SQL Server Native Client**, fare clic con il pulsante destro del mouse su **Alias**e quindi scegliere **Nuovo alias**.  
  
2.  Nella casella **Nome alias** digitare il nome dell'alias. Le applicazioni client utilizzeranno questo nome durante la connessione.  
  
3.  Nella casella **Server** digitare il nome o l'indirizzo IP di un server. Per un'istanza denominata, aggiungere il nome dell'istanza.  
  
4.  Nella casella **Protocollo** selezionare il protocollo usato per questo alias. La selezione di un protocollo comporta la modifica del titolo della casella delle proprietà facoltative in Numero porta, Nome pipe o Stringa di connessione.  
  
 Le stringhe di connessione descritte nella guida di Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere utili per i programmatori nella creazione di stringhe di connessione personalizzate. Per accedere a queste informazioni, nella finestra di dialogo **Nuovo alias** premere F1 o fare clic su **Guida**.  
  
> [!NOTE]  
>  Se un alias configurato si connette a un'istanza o a un server non valido, disabilitare e quindi riabilitare il protocollo di rete associato. In questo modo, vengono eliminate tutte le informazioni memorizzate nella cache relative alla connessione e il client può connettersi in modo corretto.  
  
#### <a name="to-delete-an-alias"></a>Per eliminare un alias  
  
1.  In Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espandere **Configurazione SQL Server Native Client**e quindi fare clic su **Alias**.  
  
2.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse sulla tabella da eliminare, quindi scegliere **Elimina**.  
  
  
