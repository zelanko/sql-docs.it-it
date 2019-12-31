---
title: Creazione di un server e di un gruppo di gestione centrale
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- configuration server
ms.assetid: da265482-3953-440a-ac23-0ab7e42a55eb
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: 17c1e63789e9c2069d8fdecd8bd62b64bf8a886d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244663"
---
# <a name="create-a-central-management-server-and-server-group-sql-server-management-studio"></a>Creazione di un server di gestione centrale e di un gruppo di server (SQL Server Management Studio)
  In questo argomento viene illustrato come designare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come server di gestione centrale in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Nei server di gestione centrale è archiviato un elenco di istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] organizzato in uno o più gruppi di server di gestione centrale. Le azioni effettuate utilizzando un gruppo di server di gestione centrale hanno effetto su tutti i server inclusi nel gruppo. Tali azioni includono la connessione ai server tramite Esplora oggetti e l'esecuzione di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] e criteri della gestione basata su criteri in più server contemporaneamente.  
  
> [!NOTE]  
>  Le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] non possono essere definite come server di gestione centrale.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per creare un server di gestione centrale e un gruppo di server utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Due ruoli del database nel database msdb concedono l'accesso ai server di gestione centrale. Solo i membri del ruolo ServerGroupAdministratorRole possono gestire il server di gestione centrale. Per connettersi a un server di gestione centrale, è necessario appartenere a un ruolo ServerGroupReaderRole.  
  
 Poiché le connessioni gestite da un server di gestione centrale vengono eseguite nel contesto dell'utente, l'utilizzo dell'autenticazione di Windows comporta la possibile variazione delle autorizzazioni effettive per i server registrati. L'utente, ad esempio, potrebbe essere un membro del ruolo predefinito del server sysadmin nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A, ma disporre di autorizzazioni limitate per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B.  
  
##  <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
 Nelle procedure indicate di seguito viene descritto come eseguire i passaggi seguenti.  
  
1.  Creare un server di gestione centrale.  
  
2.  Aggiungere uno o più gruppi di server al server di gestione centrale e aggiungere uno o più server registrati ai gruppi di server.  
  
#### <a name="create-a-central-management-server"></a>Creare un server di gestione centrale  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Server registrati** dal menu **Visualizza**.  
  
2.  In Server registrati espandere **Motore di database**, fare clic con il pulsante destro del mouse su **Server di gestione centrale**e quindi scegliere **Registra server di gestione centrale**.  
  
3.  Nella finestra di dialogo **Nuova registrazione server** selezionare dall'elenco a discesa di server l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si desidera impostare come server di gestione centrale. È necessario utilizzare l'autenticazione di Windows per il server di gestione centrale.  
  
4.  In **Server registrato**immettere un nome del server e una descrizione facoltativa.  
  
5.  Nella scheda **Proprietà connessione** rivedere o modificare le proprietà di connessione e della rete. Per altre informazioni, vedere [Connettersi al server &#40;pagina Proprietà connessione&#41; Motore di database](../f1-help/connect-to-server-connection-properties-page-database-engine.md)  
  
6.  Fare clic su **Test**per verificare la connessione.  
  
7.  Fare clic su **Save**. L'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà visualizzata nella cartella **Server di gestione centrale** .  
  
#### <a name="create-a-new-server-group-and-add-servers-to-the-group"></a>Creare un gruppo di server e aggiungere server al gruppo  
  
1.  Da **Server registrati**espandere **Server di gestione centrale**. Fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aggiunta nella procedura precedente e scegliere **Nuovo gruppo di server**.  
  
2.  In **Proprietà nuovo gruppo di server**immettere un nome di gruppo e una descrizione facoltativa.  
  
3.  In **Server registrati**fare clic con il pulsante destro del mouse sul gruppo di server di gestione centrale, quindi scegliere **Nuova registrazione server**.  
  
4.  In Nuova registrazione server selezionare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Creare un nuovo server registrato &#40;SQL Server Management Studio&#41;](create-a-new-registered-server-sql-server-management-studio.md). Aggiungere più server in base alle esigenze.  
  
#### <a name="to-execute-queries-against-several-configuration-targets-at-the-same-time"></a>Per eseguire query su più destinazioni di configurazione contemporaneamente  
  
-   Dopo avere creato un server di gestione centrale, uno o più gruppi di server e uno o più server registrati, è possibile eseguire query su un intero gruppo simultaneamente. Per altre informazioni su come eseguire istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] sui server di un gruppo di server contemporaneamente, vedere [Eseguire istruzioni su più server contemporaneamente &#40;SQL Server Management Studio&#41;](execute-statements-against-multiple-servers-simultaneously.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare più server tramite server di gestione centrale](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
