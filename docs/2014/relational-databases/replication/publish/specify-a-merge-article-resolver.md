---
title: Specificare un sistema di risoluzione dei conflitti dell'articolo di merge | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ca32ef4936f31ca5c75dfc2df1eb965d17f7b039
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060393"
---
# <a name="specify-a-merge-article-resolver"></a>Impostazione di un sistema di risoluzione dei conflitti dell'articolo di merge
  In questo argomento viene descritto come specificare un sistema di risoluzione dell'articolo di merge in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
-   **Per specificare un sistema di risoluzione dell'articolo di merge, utilizzando**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   La replica di tipo merge consente i tipi di sistemi di risoluzione dei conflitti dell'articolo indicati di seguito:  
  
    -   Il sistema di risoluzione dei conflitti predefinito. Il comportamento del sistema di risoluzione dei conflitti predefinito dipende dal tipo di sottoscrizione, ovvero se si tratta di una sottoscrizione client o server. Per altre informazioni sulla specifica del tipo di sottoscrizione, vedere [Specificare una sottoscrizione di tipo merge e la priorità per la risoluzione dei conflitti &#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
    -   Un sistema di risoluzione dei conflitti personalizzato, che può essere un gestore della logica di business (scritto in codice gestito) oppure un sistema di risoluzione dei conflitti personalizzato basato su COM. Per ulteriori informazioni, vedere [rilevamento e risoluzione dei conflitti di replica di tipo merge avanzati](../merge/advanced-merge-replication-conflict-detection-and-resolution.md). Se è necessario implementare logica personalizzata che viene eseguita per ogni riga replicata e non solo per quelle in conflitto, vedere [Implementare un gestore della logica di business per un articolo di merge](../implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Un sistema di risoluzione dei conflitti standard basato su COM, incluso in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Per utilizzare un sistema di risoluzione dei conflitti diverso da quello predefinito, è necessario copiare il sistema desiderato nel computer in cui è in esecuzione l'agente di merge e registrarlo. Se si utilizza un gestore della logica di business, è necessario eseguire la registrazione anche nel server di pubblicazione. L'agente di merge viene eseguito nei sistemi seguenti:  
  
    -   Server di distribuzione per una sottoscrizione push  
  
    -   Sottoscrittore per una sottoscrizione pull  
  
    -   Server [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) per una sottoscrizione pull che utilizza la sincronizzazione Web  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 Una volta registrato il sistema di risoluzione dei conflitti, specificare che un articolo deve utilizzare il sistema di risoluzione **nella scheda sistema di risoluzione della** finestra di dialogo **Proprietà articolo- \<Article> ** , disponibile nella creazione guidata nuova pubblicazione e nella finestra di dialogo **Proprietà pubblicazione- \<Publication> ** . Per altre informazioni sull'uso della creazione guidata e l'accesso alla finestra di dialogo, vedere [Creare una pubblicazione](create-a-publication.md) e [Visualizzare e modificare le proprietà della pubblicazione](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-a-resolver"></a>Per specificare un sistema di risoluzione dei conflitti  
  
1.  Selezionare una tabella nella pagina **articoli** della creazione guidata nuova pubblicazione o nella finestra di dialogo **Proprietà pubblicazione- \<Publication> ** .  
  
2.  Fare clic su **Proprietà articolo**e quindi su **Imposta proprietà dell'articolo di tabella evidenziato**.  
  
3.  Nella pagina **Proprietà articolo- \<Article> ** fare clic sulla scheda **resolver** .  
  
4.  Selezionare **Usa un sistema di risoluzione personalizzato (registrato nel server di distribuzione)** e quindi fare clic sul sistema di risoluzione nell'elenco.  
  
5.  Se il sistema di risoluzione dei conflitti richiede un input, ad esempio un nome di colonna, specificarlo nella casella di testo **Immettere le informazioni necessarie per il sistema di risoluzione** .  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  Ripetere questa procedura per ogni articolo che richiede un sistema di risoluzione dei conflitti.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>Per registrare un sistema di risoluzione dei conflitti personalizzato  
  
1.  Se si intende registrare un sistema di risoluzione dei conflitti personalizzato, creare uno dei tipi seguenti:  
  
    -   Sistema di risoluzione basato su codice gestito come gestore della logica di business. Per ulteriori informazioni, vedere [implementare un gestore della logica di business per un articolo di merge](../implement-a-business-logic-handler-for-a-merge-article.md).  
  
    -   Sistema di risoluzione basato sulla stored procedure e sistema di risoluzione basato su COM. Per ulteriori informazioni, vedere [implementare un sistema di risoluzione dei conflitti personalizzato per un articolo di merge](../implement-a-custom-conflict-resolver-for-a-merge-article.md).  
  
2.  Per determinare se il sistema di risoluzione desiderato è già registrato, eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) in qualsiasi database nel server di pubblicazione. Verrà visualizzata una descrizione del sistema di risoluzione personalizzato, nonché l'identificatore di classe (CLSID) di ogni sistema di risoluzione basato su COM registrato nel server di distribuzione oppure informazioni sull'assembly gestito per ogni gestore della logica di business registrato nel server di distribuzione.  
  
3.  Se il sistema di risoluzione desiderato non è già registrato, eseguire [sp_registercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql) nel database di distribuzione. Specificare un nome per il resolver per **@article_resolver** ; per un gestore della logica di business, si tratta del nome descrittivo dell'assembly. Per i resolver basati su COM, specificare il CLSID della DLL per **@resolver_clsid** e per un gestore della logica di business specificare il valore `true` per **@is_dotnet_assembly** , il nome dell'assembly per **@dotnet_assembly_name** e il nome completo della classe che esegue l'override di <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> per **@dotnet_class_name** .  
  
    > [!NOTE]  
    >  Se un assembly del gestore della logica di business non viene distribuito nella stessa directory del agente di merge eseguibile, nella stessa directory dell'applicazione che avvia in modo sincrono il agente di merge o nella Global Assembly Cache (GAC), è necessario specificare il percorso completo con il nome dell'assembly per **@dotnet_assembly_name** .  
  
4.  Se il sistema di risoluzione è basato su COM:  
  
    -   Copiare la DLL del sistema di risoluzione personalizzato nel server di distribuzione per le sottoscrizioni push o nel Sottoscrittore per le sottoscrizioni pull.  
  
        > [!NOTE]  
        >  I sistemi di risoluzione personalizzati[!INCLUDE[msCoName](../../../includes/msconame-md.md)] sono disponibili nella directory [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
    -   Utilizzare regsvr32.exe per registrare la DLL del sistema di risoluzione personalizzato con il sistema operativo. Ad esempio, eseguire il seguente comando dal prompt dei comandi per registrare il sistema di risoluzione dei conflitti aggiuntivi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  Se il sistema di risoluzione è un gestore della logica di business, distribuire l'assembly nella stessa cartella del agente di merge eseguibile (replmerg.exe), nella stessa cartella di un'applicazione che richiama il agente di merge o nella cartella specificata per il **@dotnet_assembly_name** parametro nel passaggio 3.  
  
    > [!NOTE]  
    >  Il percorso di installazione predefinito del file eseguibile dell'agente di merge è [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>Per specificare un sistema di risoluzione personalizzato durante la definizione di un articolo di merge  
  
1.  Se si intende utilizzare un sistema di risoluzione dei conflitti personalizzato, crearlo e registrarlo utilizzando la procedura sopra riportata.  
  
2.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e prendere nota del nome del sistema di risoluzione personalizzato desiderato nel campo **valore** del set di risultati.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Specificare il nome del sistema di risoluzione ottenuto al passaggio 2 per **@article_resolver** ed eventuali input necessari per il resolver personalizzato utilizzando il **@resolver_info** parametro. Per i resolver personalizzati basati su stored procedure, **@resolver_info** è il nome del stored procedure. Per altre informazioni sull'input richiesto per i sistemi di risoluzione dei conflitti forniti da [!INCLUDE[msCoName](../../../includes/msconame-md.md)], vedere [Sistemi di risoluzione dei conflitti basati su Microsoft COM](../merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>Per specificare o modificare un sistema di risoluzione personalizzato per un articolo di merge esistente  
  
1.  Per determinare se per un articolo è stato definito un sistema di risoluzione personalizzato oppure per ottenere il nome del sistema di risoluzione, eseguire [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Se per l'articolo è stato definito un sistema di risoluzione personalizzato, il relativo nome verrà visualizzato nel campo **article_resolver** . Eventuale input fornito al sistema di risoluzione verrà visualizzato nel campo **resolver_info** del set di risultati.  
  
2.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e prendere nota del nome del sistema di risoluzione personalizzato desiderato nel campo **value** del set di risultati.  
  
3.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore **article_resolver**, incluso il percorso completo dei gestori della logica di business, per **@property**, nonché il nome del sistema di risoluzione personalizzato desiderato ottenuto al passaggio 2 per **@value**.  
  
4.  Per modificare l'eventuale input richiesto per il sistema di risoluzione personalizzato, eseguire nuovamente [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Specificare il valore **resolver_info** per **@property** ed eventuale input obbligatorio per il sistema di risoluzione personalizzato per **@value**. Per i resolver personalizzati basati su stored procedure, **@resolver_info** è il nome del stored procedure. Per altre informazioni sull'input richiesto, vedere [Sistemi di risoluzione dei conflitti basati su Microsoft COM](../merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>Per annullare la registrazione di un sistema di risoluzione dei conflitti personalizzato  
  
1.  Nel server di pubblicazione eseguire [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) e prendere nota del nome del sistema di risoluzione personalizzato da rimuovere nel campo **value** del set di risultati.  
  
2.  Eseguire [sp_unregistercustomresolver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql) nel database di distribuzione. Specificare il nome completo del sistema di risoluzione personalizzato ottenuto al passaggio 1 per **@article_resolver** .  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> Esempi (Transact-SQL)  
 In questo esempio viene creato un nuovo articolo e viene impostato l'utilizzo del sistema di risoluzione dei conflitti medi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per calcolare la media della colonna **UnitPrice** in caso di conflitti.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_addmerge_resolver)]  
  
 In questo esempio un articolo viene impostato in modo da utilizzare il sistema di risoluzione dei conflitti aggiuntivi [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per calcolare la somma della colonna **UnitsOnOrder** in caso di conflitti.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_changemerge_resolver)]  
  
## <a name="see-also"></a>Vedere anche  
 [Rilevamento e risoluzione dei conflitti di replica di tipo merge avanzati](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Implementazione di un gestore della logica di business per un articolo di merge](../implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
