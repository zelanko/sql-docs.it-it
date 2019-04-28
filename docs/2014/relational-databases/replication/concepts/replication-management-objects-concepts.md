---
title: Concetti di base relativi a RMO (Replication Management Objects) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- replication [SQL Server], RMO
- programming interfaces [SQL Server replication]
- replication [SQL Server], how-to topics
- RMO [SQL Server]
- Replication Management Objects
- programming [SQL Server replication], RMO
ms.assetid: 37476d50-fb47-49e3-9504-3b163ac381d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2cbc3571aa26728fa94957bb0c2f207ff769f4c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721793"
---
# <a name="replication-management-objects-concepts"></a>Replication Management Objects Concepts
  RMO (Replication Management Objects) è un assembly di codice gestito che incapsula le funzionalità di replica per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. RMO viene implementato dallo spazio dei nomi <xref:Microsoft.SqlServer.Replication>.  
  
 Negli argomenti seguenti viene descritto come utilizzare RMO a livello di programmazione per controllare le attività di replica:  
  
 [Configurare la distribuzione](../configure-distribution.md)  
 Negli argomenti inclusi in questa sezione viene illustrato come utilizzare RMO per configurare la pubblicazione e la distribuzione.  
  
 [Create a Publication](../publish/create-a-publication.md)  
 Negli argomenti inclusi in questa sezione viene illustrato come utilizzare RMO per creare, eliminare e modificare pubblicazioni e articoli.  
  
 [Sottoscrizione delle pubblicazioni](../subscribe-to-publications.md)  
 Negli argomenti inclusi in questa sezione viene illustrato come utilizzare RMO per creare, eliminare e modificare sottoscrizioni.  
  
 [Proteggere una topologia di replica](../security/view-and-modify-replication-security-settings.md)  
 Negli argomenti inclusi in questa sezione viene illustrato come utilizzare RMO per visualizzare e modificare le impostazioni di sicurezza.  
  
 [Sincronizzare le sottoscrizioni &#40;replica&#41;](../synchronize-data.md)  
 Negli argomenti inclusi in questa sezione viene illustrato come sincronizzare le sottoscrizioni.  
  
 [Monitoraggio della replica](../monitoring-replication.md)  
 Negli argomenti inclusi in questa sezione viene illustrato come monitorare a livello di codice una topologia di replica.  
  
## <a name="introduction-to-rmo-programming"></a>Introduzione alla programmazione RMO  
 RMO è progettato per consentire la programmazione di tutti gli aspetti della replica di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Lo spazio dei nomi di RMO è <xref:Microsoft.SqlServer.Replication> e viene implementato da Microsoft.SqlServer.Rmo.dll, un assembly di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. L'assembly Microsoft.SqlServer.Replication.dll, che appartiene allo spazio dei nomi <xref:Microsoft.SqlServer.Replication>, implementa un'interfaccia di codice gestito per la programmazione dei vari agenti di replica (Agente snapshot, Agente di distribuzione e Agente di merge). È possibile accedere alle classi corrispondenti da RMO per sincronizzare le sottoscrizioni. Le classi nello spazio dei nomi <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>, implementato dall'assembly Microsoft.SqlServer.Replication.BusinessLogicSupport.dll, vengono utilizzate per creare la logica di business personalizzata per la replica di tipo merge. Questo assembly è indipendente da RMO.  
  
## <a name="deploying-applications-based-on-rmo"></a>Distribuzione di applicazioni basate su RMO  
 RMO dipende dai componenti di replica e dai componenti di connettività del client inclusi in tutte le versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], tranne SQL Server Compact. Per distribuire un'applicazione basata su RMO, è necessario installare una versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che includa componenti di replica e componenti di connettività del client nel computer in cui verrà eseguita l'applicazione.  
  
## <a name="getting-started-with-rmo"></a>Introduzione a RMO  
 In questa sezione viene descritto come creare un progetto RMO semplice utilizzando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio.  
  
#### <a name="to-create-a-new-microsoft-visual-c-project"></a>Per creare un nuovo progetto di Microsoft Visual C#  
  
1.  Avviare Visual Studio.  
  
2.  Scegliere **Nuovo progetto** dal menu **File**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nella finestra di dialogo **Tipi progetto** selezionare **Progetti di Visual C#**. Nel riquadro **Modelli** selezionare **Applicazione Windows**.  
  
4.  (Facoltativo) In **Nome** digitare il nome della nuova applicazione.  
  
5.  Fare clic su **OK** per caricare il modello di Windows per Visual C#.  
  
6.  Scegliere **Aggiungi riferimento** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
7.  Selezionare gli assembly seguenti nell'elenco della scheda **.NET** e quindi fare clic su **OK**.  
  
    -   Interfaccia di programmazione .NET per Microsoft.SqlServer.Replication  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Libreria dell'agente di replica  
  
    > [!NOTE]  
    >  Per selezionare più file, utilizzare il tasto CTRL.  
  
8.  (Facoltativo) Ripetere il passaggio 6. Fare clic sulla scheda **Sfoglia**, passare a [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM, selezionare Microsoft.SqlServer.Replication.BusinessLogicSupport.dll e quindi fare clic su **OK**.  
  
9. Scegliere **Codice** dal menu **Visualizza**.  
  
10. Nel codice, prima dell'istruzione dello spazio dei nomi, digitare le istruzioni `using` seguenti per qualificare i tipi negli spazi dei nomi di RMO:  
  
    ```  
    // These namespaces are required.  
    using Microsoft.SqlServer.Replication;  
    using Microsoft.SqlServer.Management.Common;  
    // This namespace is only used when creating custom business  
    // logic for merge replication.  
    using Microsoft.SqlServer.Replication.BusinessLogicSupport;   
    ```  
  
#### <a name="to-create-a-new-microsoft-visual-basic-net-project"></a>Per creare un nuovo progetto di Microsoft Visual Basic .NET  
  
1.  Avviare Visual Studio.  
  
2.  Scegliere **Nuovo progetto** dal menu **File**. Verrà visualizzata la finestra di dialogo **Nuovo progetto** .  
  
3.  Nel riquadro Tipi progetto selezionare **Visual Basic**. Nel riquadro Modelli selezionare **Applicazione Windows**.  
  
4.  (Facoltativo) Nella casella **Nome** digitare il nome della nuova applicazione.  
  
5.  Fare clic su **OK** per caricare il modello di Windows per Visual Basic.  
  
6.  Scegliere **Aggiungi riferimento** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo **Aggiungi riferimento**.  
  
7.  Selezionare gli assembly seguenti nell'elenco della scheda **.NET** e quindi fare clic su **OK**.  
  
    -   Interfaccia di programmazione .NET per Microsoft.SqlServer.Replication  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Libreria dell'agente di replica  
  
    > [!NOTE]  
    >  Per selezionare più file, utilizzare il tasto CTRL.  
  
8.  (Facoltativo) Ripetere il passaggio 6. Fare clic sulla scheda **Sfoglia**, passare a [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM, selezionare Microsoft.SqlServer.Replication.BusinessLogicSupport.dll e quindi fare clic su **OK**.  
  
9. Scegliere **Codice** dal menu **Visualizza**.  
  
10. Nel codice, prima di qualsiasi dichiarazione, digitare le istruzioni `Imports` seguenti per qualificare i tipi negli spazi dei nomi di RMO:  
  
    ```  
    ' These namespaces are required.  
    Imports Microsoft.SqlServer.Replication  
    Imports Microsoft.SqlServer.Management.Common  
    ' This namespace is only used when creating custom business  
    ' logic for merge replication.  
    Imports Microsoft.SqlServer.Replication.BusinessLogicSupport   
    ```  
  
## <a name="connecting-to-a-replication-server"></a>Connessione a un server di replica  
 Gli oggetti di programmazione RMO richiedono che una connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] venga stabilita mediante un'istanza della classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Questa connessione al server viene stabilita indipendentemente da qualsiasi oggetto di programmazione RMO. Viene quindi passata all'oggetto RMO durante la creazione dell'istanza o mediante l'assegnazione alla proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> dell'oggetto. In questo modo, un oggetto di programmazione RMO e le istanze dell'oggetto connessione possono essere creati e gestiti separatamente e un singolo oggetto connessione può essere riutilizzato con più oggetti di programmazione RMO. Le regole seguenti sono valide per le connessioni a un server di replica:  
  
-   Tutte le proprietà per la connessione sono definite per un oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> specificato.  
  
-   La connessione a ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve disporre del relativo oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   L'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> è assegnato alla proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> dell'oggetto di programmazione RMO creato o a cui si accede nel server.  
  
-   Il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> apre la connessione al server. Questo metodo deve essere chiamato prima di chiamare i metodi che consentono di accedere al server su qualsiasi oggetto di programmazione RMO utilizzando la connessione.  
  
-   Poiché RMO e SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects) utilizzano entrambi la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> per le connessioni a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la stessa connessione può essere utilizzata sia da oggetti RMO che SMO. Per altre informazioni, vedere [Connessione a un'istanza di SQL Server](../../server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md).  
  
-   Tutte le informazioni di autenticazione che consentono di stabilire la connessione e accedere correttamente al server vengono fornite nell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   L'autenticazione di Windows rappresenta l'impostazione predefinita. Per utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> deve essere impostato su `false` e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> devono essere impostati su un accesso e una password di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Le credenziali di sicurezza devono essere sempre archiviate e gestite in modo protetto, nonché fornite in fase di esecuzione quando possibile.  
  
-   Per le applicazioni multithreading, in ogni thread è necessario utilizzare un oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> separato.  
  
 Chiamare il metodo <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> sull'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> per chiudere le connessioni al server attive utilizzate da oggetti RMO.  
  
## <a name="setting-rmo-properties"></a>Impostazione delle proprietà RMO  
 Le proprietà degli oggetti di programmazione RMO rappresentano le proprietà di tali oggetti di replica nel server. Quando si creano nuovi oggetti di replica nel server, le proprietà RMO vengono utilizzate per definire tali oggetti. Per gli oggetti esistenti, le proprietà RMO rappresentano le proprietà dell'oggetto esistente, che possono essere modificate solo per le proprietà scrivibili o configurabili. Le proprietà possono essere impostate su oggetti nuovi o esistenti.  
  
### <a name="setting-properties-for-new-replication-objects"></a>Impostazione delle proprietà per oggetti di replica nuovi  
 Quando si crea un nuovo oggetto di replica nel server, è necessario specificare tutte le proprietà obbligatorie prima di chiamare il metodo `Create` dell'oggetto. Per altre informazioni sull'impostazione delle proprietà per un nuovo oggetto di replica, vedere [Configurare la pubblicazione e la distribuzione](../configure-publishing-and-distribution.md).  
  
### <a name="setting-properties-for-existing-replication-objects"></a>Impostazione delle proprietà per oggetti di replica esistenti  
 Per gli oggetti di replica che esistono nel server, a seconda dell'oggetto, RMO potrebbe supportare la possibilità di modificare alcune o tutte le proprietà corrispondenti. Solo le proprietà scrivibili o configurabili possono essere modificate. Prima di poter modificare le proprietà, è necessario chiamare il metodo `Load` o <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per ottenere le proprietà correnti dal server. La chiamata di questi metodi indica che è in corso la modifica di un oggetto esistente.  
  
 Per impostazione predefinita, quando si modificano le proprietà degli oggetti, RMO esegue il commit di tali modifiche nel server in base alla modalità di esecuzione dell'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> in uso. Il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> può essere utilizzato per verificare che un oggetto esista nel server prima di tentare di recuperare o modificare le proprietà corrispondenti. Per altre informazioni sulla modifica delle proprietà di un oggetto di replica, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../view-and-modify-distributor-and-publisher-properties.md).  
  
> [!NOTE]  
>  Se più client RMO o più istanze di un oggetto di programmazione RMO stanno accedendo allo stesso oggetto di replica nel server, il metodo `Refresh` dell'oggetto RMO può essere chiamato per aggiornare le proprietà in base allo stato corrente dell'oggetto nel server.  
  
### <a name="caching-property-changes"></a>Memorizzazione nella cache delle modifiche alle proprietà  
 Quando la proprietà <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> è impostata su <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes.CaptureSql>, tutte le istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] generate da RMO vengono acquisite in modo che possano essere eseguite manualmente in un unico batch mediante uno dei metodo di esecuzione disponibili. RMO consente di memorizzare nella cache le modifiche alle proprietà e di eseguirne il commit contemporaneamente in un unico batch mediante il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> dell'oggetto. Per memorizzare nella cache le modifiche alle proprietà, la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> dell'oggetto deve essere impostata su `true`. Quando si memorizzano nella cache le modifiche alle proprietà apportate in RMO, l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> controlla comunque quando viene eseguito l'invio delle modifiche al server. Per altre informazioni sulla modifica delle proprietà di un oggetto di replica, vedere [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../view-and-modify-distributor-and-publisher-properties.md).  
  
> [!IMPORTANT]  
>  Sebbene la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> supporti la dichiarazione di transazioni esplicite durante l'impostazione delle proprietà, tali transazioni possono interferire con le transazioni di replica interne e produrre risultati inaspettati. Per questo motivo non devono essere utilizzate con RMO.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene illustrata la memorizzazione nella cache delle modifiche alle proprietà. Le modifiche apportate agli attributi di una pubblicazione transazionale rimangono memorizzate nella cache fino a quando non vengono inviate in modo esplicito al server.  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_ChangeTranPub_cached)]  
  
## <a name="see-also"></a>Vedere anche  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)   
 [Concetti di base relativi alla programmazione della replica](replication-programming-concepts.md)  
  
  
