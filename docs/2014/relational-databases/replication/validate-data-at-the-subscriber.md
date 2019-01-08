---
title: Convalidare i dati nel Sottoscrittore | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b8829bb1a585c61bfa1a8ad0a088d23e8573bace
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816883"
---
# <a name="validate-data-at-the-subscriber"></a>Convalida dei dati nel Sottoscrittore
  In questo argomento viene descritto come convalidare i dati nel Sottoscrittore in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o RMO (Replication Management Objects).  
  
 La convalida dei dati è un processo suddiviso in tre parti:  
  
1.  Una sottoscrizione o tutte le sottoscrizioni di una pubblicazione vengono *contrassegnate* per la convalida. \Contrassegnare le sottoscrizioni per la convalida nelle finestre di dialogo **Convalida sottoscrizione**, **Convalida sottoscrizioni**e **Convalida tutte le sottoscrizioni** , disponibili dalle cartelle **Pubblicazioni locali** e **Sottoscrizioni locali** in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. È inoltre possibile contrassegnare le sottoscrizioni nella scheda **Tutte le sottoscrizioni** , nella scheda **Elenco verifica sottoscrizioni** e nel nodo delle pubblicazioni in Monitoraggio replica. Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](monitor/start-the-replication-monitor.md).  
  
2.  La sottoscrizione viene convalidata alla successiva sincronizzazione eseguita dall'agente di distribuzione, nel caso della replica transazionale, o dall'agente di merge nella replica di tipo merge. L'agente di distribuzione in genere viene eseguito in modo continuativo, pertanto la convalida viene eseguita immediatamente, mentre l'agente di merge in genere viene eseguito su richiesta, pertanto la convalida viene eseguita solo dopo l'esecuzione dell'agente.  
  
3.  I risultati della convalida possono essere visualizzati nelle finestre seguenti:  
  
    -   Nella finestra dei dettagli in Monitoraggio replica, all'interno della scheda **Cronologia database di distribuzione - Sottoscrittore** per la replica transazionale e nella scheda **Cronologia sincronizzazione** per la replica di tipo merge.  
  
    -   Nella finestra di dialogo **Visualizza stato sincronizzazione** in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
-   **Per convalida i dati nel Sottoscrittore tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Oggetti RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le procedure relative a Monitoraggio replica riguardano solo le sottoscrizioni push in quanto le sottoscrizioni pull non possono essere sincronizzate in Monitoraggio replica. È tuttavia possibile contrassegnare una sottoscrizione per la convalida e visualizzare i risultati della convalida per le sottoscrizioni pull in Monitoraggio replica.  
  
-   I risultati della convalida consentono di stabilire se la convalida è stata completata correttamente o meno, ma in caso di errore non indicano quali righe non hanno superato la convalida. Per confrontare i dati nel server di pubblicazione e nel Sottoscrittore, utilizzare la [tablediff Utility](../../tools/tablediff-utility.md). Per ulteriori informazioni sull'uso di questa utilità con i dati replicati, vedere [Confrontare tabelle replicate al fine di individuare le differenze &#40;programmazione della replica&#41;](administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-validate-data-for-subscriptions-to-a-transactional-publication-management-studio"></a>Per convalidare i dati per le sottoscrizioni di una pubblicazione transazionale (Management Studio)  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione di cui si desidera convalidare le sottoscrizioni e quindi scegliere **Convalida sottoscrizioni**.  
  
4.  Nella finestra di dialogo **Convalida sottoscrizioni** selezionare le sottoscrizioni da convalidare:  
  
    -   Selezionare **Convalida tutte le sottoscrizioni SQL Server**.  
  
    -   Selezionare **Convalida le sottoscrizioni seguenti**e quindi scegliere una o più sottoscrizioni.  
  
5.  Per specificare il tipo di convalida da eseguire (solo conteggio delle righe o conteggio delle righe e valori di checksum), fare clic su **Opzioni di convalida**e quindi specificare le opzioni nella finestra di dialogo **Opzioni di convalida delle sottoscrizioni** .  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  I risultati della convalida possono essere visualizzati in Monitoraggio replica o nella finestra di dialogo **Visualizza stato sincronizzazione** . Eseguire la procedura seguente per ogni sottoscrizione:  
  
    1.  Espandere la pubblicazione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza stato sincronizzazione**.  
  
    2.  Se l'agente non è in esecuzione, fare clic su **Avvia** nella finestra di dialogo **Visualizza stato sincronizzazione** . Nella finestra di dialogo verranno visualizzati messaggi informativi relativi alla convalida.  
  
     Se non viene visualizzato alcun messaggio attinente, l'agente deve aver già registrato un messaggio successivo. In questo caso, visualizzare i risultati della convalida in Monitoraggio replica. Per ulteriori informazioni, vedere le procedure per Monitoraggio replica in questo argomento.  
  
#### <a name="to-validate-data-for-a-single-subscription-to-a-merge-publication-management-studio"></a>Per convalidare i dati di una singola sottoscrizione di una pubblicazione di tipo merge (Management Studio)  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Espandere la pubblicazione di cui si desidera convalidare le sottoscrizioni, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Convalida sottoscrizione**.  
  
4.  Nella finestra di dialogo **Convalida sottoscrizione** selezionare **Convalida la sottoscrizione**.  
  
5.  Per specificare il tipo di convalida da eseguire (solo conteggio delle righe o conteggio delle righe e valori di checksum), fare clic su **Opzioni**e quindi specificare le opzioni nella finestra di dialogo **Opzioni di convalida delle sottoscrizioni** .  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  I risultati della convalida possono essere visualizzati in Monitoraggio replica o nella finestra di dialogo **Visualizza stato sincronizzazione** .  
  
    1.  Espandere la pubblicazione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza stato sincronizzazione**.  
  
    2.  Se l'agente non è in esecuzione, fare clic su **Avvia** nella finestra di dialogo **Visualizza stato sincronizzazione** . Nella finestra di dialogo verranno visualizzati messaggi informativi relativi alla convalida.  
  
     Se non viene visualizzato alcun messaggio attinente, l'agente deve aver già registrato un messaggio successivo. In questo caso, visualizzare i risultati della convalida in Monitoraggio replica. Per ulteriori informazioni, vedere le procedure per Monitoraggio replica in questo argomento.  
  
#### <a name="to-validate-data-for-all-subscriptions-to-a-merge-publication-management-studio"></a>Per convalidare i dati per tutte le sottoscrizioni di una pubblicazione di tipo merge (Management Studio)  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione di cui si desidera convalidare le sottoscrizioni e quindi scegliere **Convalida tutte le sottoscrizioni**.  
  
4.  Nella finestra di dialogo **Convalida tutte le sottoscrizioni** specificare il tipo di convalida da eseguire (solo conteggio delle righe o conteggio delle righe e valori di checksum).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  I risultati della convalida possono essere visualizzati in Monitoraggio replica o nella finestra di dialogo **Visualizza stato sincronizzazione** . Eseguire la procedura seguente per ogni sottoscrizione:  
  
    1.  Espandere la pubblicazione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza stato sincronizzazione**.  
  
    2.  Se l'agente non è in esecuzione, fare clic su **Avvia** nella finestra di dialogo **Visualizza stato sincronizzazione** . Nella finestra di dialogo verranno visualizzati messaggi informativi relativi alla convalida.  
  
     Se non viene visualizzato alcun messaggio attinente, l'agente deve aver già registrato un messaggio successivo. In questo caso, visualizzare i risultati della convalida in Monitoraggio replica. Per ulteriori informazioni, vedere le procedure per Monitoraggio replica in questo argomento.  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-transactional-publication-replication-monitor"></a>Per convalidare i dati per tutte le sottoscrizioni push di una pubblicazione transazionale (Monitoraggio replica)  
  
1.  In Monitoraggio replica espandere un gruppo di server di pubblicazione nel riquadro di sinistra e quindi espandere un server di pubblicazione.  
  
2.  Fare clic con il pulsante destro del mouse sulla pubblicazione di cui si desidera convalidare le sottoscrizioni e quindi scegliere **Convalida sottoscrizioni**.  
  
3.  Nella finestra di dialogo **Convalida sottoscrizioni** selezionare le sottoscrizioni da convalidare:  
  
    -   Selezionare **Convalida tutte le sottoscrizioni SQL Server**.  
  
    -   Selezionare **Convalida le sottoscrizioni seguenti**e quindi scegliere una o più sottoscrizioni.  
  
4.  Per specificare il tipo di convalida da eseguire (solo conteggio delle righe o conteggio delle righe e valori di checksum), fare clic su **Opzioni di convalida**e quindi specificare le opzioni nella finestra di dialogo **Opzioni di convalida delle sottoscrizioni** .  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
7.  Visualizzare i risultati della convalida. Eseguire la procedura seguente per ogni sottoscrizione push:  
  
    1.  Se l'agente non è in esecuzione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.  
  
    2.  Fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
    3.  Visualizzare le informazioni nella scheda **Cronologia server di distribuzione - Sottoscrittore** all'interno dell'area di testo **Azioni nella sessione selezionata** .  
  
#### <a name="to-validate-data-for-a-single-push-subscription-to-a-merge-publication-replication-monitor"></a>Per convalidare i dati di una singola sottoscrizione push di una pubblicazione di tipo merge (Monitoraggio replica)  
  
1.  In Monitoraggio replica espandere un gruppo di server di pubblicazione nel riquadro di sinistra, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
3.  Fare clic con il pulsante destro del mouse sulla sottoscrizione che si desidera convalidare e quindi scegliere **Convalida sottoscrizione**.  
  
4.  Nella finestra di dialogo **Convalida sottoscrizione** selezionare **Convalida la sottoscrizione**.  
  
5.  Per specificare il tipo di convalida da eseguire (solo conteggio delle righe o conteggio delle righe e valori di checksum), fare clic su **Opzioni**e quindi specificare le opzioni nella finestra di dialogo **Opzioni di convalida delle sottoscrizioni** .  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
8.  Visualizzare i risultati della convalida:  
  
    1.  Se l'agente non è in esecuzione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.  
  
    2.  Fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
    3.  Visualizzare le informazioni nella scheda **Cronologia sincronizzazione** all'interno dell'area di testo **Ultimo messaggio della sessione selezionata** .  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-merge-publication-replication-monitor"></a>Per convalidare i dati per tutte le sottoscrizioni push di una pubblicazione di tipo merge (Monitoraggio replica)  
  
1.  In Monitoraggio replica espandere un gruppo di server di pubblicazione nel riquadro di sinistra e quindi espandere un server di pubblicazione.  
  
2.  Fare clic con il pulsante destro del mouse sulla pubblicazione di cui si desidera convalidare le sottoscrizioni e quindi scegliere **Convalida tutte le sottoscrizioni**.  
  
3.  Nella finestra di dialogo **Convalida tutte le sottoscrizioni** specificare il tipo di convalida da eseguire (solo conteggio delle righe o conteggio delle righe e valori di checksum).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
6.  Visualizzare i risultati della convalida. Eseguire la procedura seguente per ogni sottoscrizione push:  
  
    1.  Se l'agente non è in esecuzione, fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Avvia sincronizzazione**.  
  
    2.  Fare clic con il pulsante destro del mouse sulla sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
    3.  Visualizzare le informazioni nella scheda **Cronologia sincronizzazione** all'interno dell'area di testo **Ultimo messaggio della sessione selezionata** .  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>Per convalidare i dati per tutti gli articoli in una pubblicazione transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_publication_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql). Specificare **@publication** e uno dei valori riportati di seguito per **@rowcount_only**.  
  
    -   **1** : convalida solo mediante conteggio delle righe (impostazione predefinita).  
  
    -   **2** : convalida mediante conteggio delle righe e checksum binario.  
  
    > [!NOTE]  
    >  Quando si esegue [sp_publication_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql), [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql) viene eseguito per ogni articolo nella pubblicazione. Per eseguire correttamente [sp_publication_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql) è necessario disporre delle autorizzazioni SELECT per tutte le colonne nelle tabelle di base pubblicate.  
  
2.  (Facoltativo) Avviare l'agente di distribuzione per ogni sottoscrizione, se non è già in esecuzione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
3.  Verificare l'output dell'agente per il risultato della convalida. Per altre informazioni, vedere [Convalidare i dati replicati](validate-replicated-data.md).  
  
#### <a name="to-validate-data-for-a-single-article-in-a-transactional-publication"></a>Per convalidare i dati per un singolo articolo in una pubblicazione transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql). Specificare **@publication**, il nome dell'articolo per **@article**e uno dei valori riportati di seguito per **@rowcount_only**.  
  
    -   **1** : convalida solo mediante conteggio delle righe (impostazione predefinita).  
  
    -   **2** : convalida mediante conteggio delle righe e checksum binario.  
  
    > [!NOTE]  
    >  Per eseguire correttamente [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql), è necessario disporre delle autorizzazioni SELECT per tutte le colonne nella tabella di base pubblicata.  
  
2.  (Facoltativo) Avviare l'agente di distribuzione per ogni sottoscrizione, se non è già in esecuzione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
3.  Verificare l'output dell'agente per il risultato della convalida. Per altre informazioni, vedere [Convalidare i dati replicati](validate-replicated-data.md).  
  
#### <a name="to-validate-data-for-a-single-subscriber-to-a-transactional-publication"></a>Per convalidare i dati per un singolo Sottoscrittore di una pubblicazione transazionale  
  
1.  Nel database di pubblicazione del server di pubblicazione aprire una transazione esplicita usando [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql).  
  
2.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql). Specificare la pubblicazione per **@publication**, il nome del Sottoscrittore per **@subscriber**e il nome del database di sottoscrizione per **@destination_db**.  
  
3.  (Facoltativo) Ripetere il passaggio 2 per ciascuna sottoscrizione da convalidare.  
  
4.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql). Specificare **@publication**, il nome dell'articolo per **@article**e uno dei valori riportati di seguito per **@rowcount_only**.  
  
    -   **1** : convalida solo mediante conteggio delle righe (impostazione predefinita).  
  
    -   **2** : convalida mediante conteggio delle righe e checksum binario.  
  
    > [!NOTE]  
    >  Per eseguire correttamente [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql), è necessario disporre delle autorizzazioni SELECT per tutte le colonne nella tabella di base pubblicata.  
  
5.  Nel database di pubblicazione del server di pubblicazione eseguire il commit della transazione usando [COMMIT TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql).  
  
6.  (Facoltativo) Ripetere i passaggi da 1 a 5 per ciascun articolo da convalidare.  
  
7.  (Facoltativo) Avviare l'agente di distribuzione, se non è già in esecuzione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
8.  Verificare l'output dell'agente per il risultato della convalida. Per altre informazioni, vedere [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>Per convalidare i dati in tutte le sottoscrizioni di una pubblicazione di tipo merge  
  
1.  (Facoltativo) Nel database di pubblicazione del server di pubblicazione eseguire [sp_validatemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql). Specificare **@publication** e uno dei valori riportati di seguito per **@level**.  
  
    -   **1** : convalida solo mediante conteggio delle righe.  
  
    -   **3** : convalida mediante conteggio delle righe e checksum binario.  
  
     Tutte le sottoscrizioni vengono contrassegnate per la convalida.  
  
2.  Avviare l'agente di merge per ciascuna sottoscrizione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
3.  Verificare l'output dell'agente per il risultato della convalida. Per altre informazioni, vedere [Validate Data at the Subscriber](validate-data-at-the-subscriber.md).  
  
#### <a name="to-validate-data-in-selected-subscriptions-to-a-merge-publication"></a>Per convalidare i dati nelle sottoscrizioni selezionate di una pubblicazione di tipo merge  
  
1.  Nel database di pubblicazione del server di pubblicazione eseguire [sp_validatemergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql). Specificare **@publication**, il nome del Sottoscrittore per **@subscriber**, il nome del database di sottoscrizione per **@subscriber_db**e uno dei valori riportati di seguito per **@level**.  
  
    -   **1** : convalida solo mediante conteggio delle righe.  
  
    -   **3** : convalida mediante conteggio delle righe e checksum binario.  
  
     La sottoscrizione selezionata viene contrassegnata per la convalida.  
  
2.  Avviare l'agente di merge per ciascuna sottoscrizione. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
3.  Verificare l'output dell'agente per il risultato della convalida.  
  
4.  Ripetere i passaggi da 1 a 3 per ciascuna sottoscrizione da convalidare.  
  
> [!NOTE]  
>  È inoltre possibile convalidare una sottoscrizione di una pubblicazione di tipo merge alla fine di una sincronizzazione, specificando il parametro **-Validate** al momento dell'esecuzione di [Replication Merge Agent](agents/replication-merge-agent.md).  
  
#### <a name="to-validate-data-in-a-subscription-using-merge-agent-parameters"></a>Per convalidare i dati in una sottoscrizione utilizzando i parametri dell'agente di merge  
  
1.  Avviare l'agente di merge nel Sottoscrittore (sottoscrizione pull) o nel server di distribuzione (sottoscrizione push) dal prompt dei comandi, mediante una delle modalità indicate di seguito.  
  
    -   Specificare il valore **1** (conteggio delle righe) o **3** (conteggio delle righe e checksum binario) per il parametro **-Validate** .  
  
    -   Specificare la **convalida mediante conteggio delle righe** o la **convalida mediante conteggio delle righe e checksum** per il parametro **-ProfileName** .  
  
     Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) o [Synchronize a Push Subscription](synchronize-a-push-subscription.md).  
  
##  <a name="RMOProcedure"></a> Utilizzo di RMO (Replication Management Objects)  
 La replica consente di utilizzare gli oggetti RMO (Replication Management Objects) per convalidare a livello di programmazione la corrispondenza tra i dati nel Sottoscrittore e quelli nel server di pubblicazione. Gli oggetti utilizzati variano in base al tipo di topologia di replica. La replica transazionale richiede la convalida di tutte le sottoscrizioni di una pubblicazione.  
  
> [!NOTE]  
>  Ad esempio, vedere [Esempio (RMO)](#RMOExample)più avanti in questa sezione.  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>Per convalidare i dati per tutti gli articoli in una pubblicazione transazionale  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.TransPublication> . Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione. Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà rimanenti dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono state definite in modo non corretto nel passaggio 2 oppure la pubblicazione non esiste.  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A>. Passare quanto segue:  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   Un valore booleano che indica se l'agente di distribuzione deve essere arrestato al termine della convalida.  
  
     Gli articoli vengono contrassegnati per la convalida.  
  
5.  Se non è già in esecuzione, avviare l'agente di distribuzione per sincronizzare ciascuna sottoscrizione. Per ulteriori informazioni, vedere [Synchronize a Push Subscription](synchronize-a-push-subscription.md) o [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md). Il risultato dell'operazione di convalida viene scritto nella cronologia dell'agente. Per altre informazioni, vedere [Monitoring Replication](monitoring-replication.md).  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>Per convalidare i dati in tutte le sottoscrizioni di una pubblicazione di tipo merge  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione. Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà rimanenti dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono state definite in modo non corretto nel passaggio 2 oppure la pubblicazione non esiste.  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A>. Passare l'oggetto <xref:Microsoft.SqlServer.Replication.ValidationOption>desiderato.  
  
5.  Eseguire l'agente di merge per avviare la convalida in ciascuna sottoscrizione oppure attendere la successiva esecuzione pianificata dell'agente. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md). Il risultato dell'operazione di convalida viene scritto nella cronologia dell'agente, visualizzabile tramite Monitoraggio replica. Per altre informazioni, vedere [Monitoring Replication](monitoring-replication.md).  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>Per convalidare i dati in una singola sottoscrizione di una pubblicazione di tipo merge  
  
1.  Creare una connessione al server di pubblicazione tramite la classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Creare un'istanza della classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Impostare le proprietà <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> per la pubblicazione. Impostare la proprietà <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> sulla connessione creata nel passaggio 1.  
  
3.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> per recuperare le proprietà rimanenti dell'oggetto. Se questo metodo restituisce `false`, le proprietà della pubblicazione sono state definite in modo non corretto nel passaggio 2 oppure la pubblicazione non esiste.  
  
4.  Chiamare il metodo <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A>. Passare il nome del Sottoscrittore e il database di sottoscrizione da convalidare e l'oggetto <xref:Microsoft.SqlServer.Replication.ValidationOption>desiderato.  
  
5.  Eseguire l'agente di merge per avviare la convalida nella sottoscrizione oppure attendere la successiva esecuzione pianificata dell'agente. Per ulteriori informazioni, vedere [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](synchronize-a-push-subscription.md). Il risultato dell'operazione di convalida viene scritto nella cronologia dell'agente, visualizzabile tramite Monitoraggio replica. Per altre informazioni, vedere [Monitoring Replication](monitoring-replication.md).  
  
###  <a name="RMOExample"></a> Esempio (RMO)  
 In questo esempio tutte le sottoscrizioni di una pubblicazione transazionale vengono contrassegnate per la convalida mediante il conteggio delle righe.  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 In questo esempio una sottoscrizione specifica di una pubblicazione di tipo merge viene contrassegnata per la convalida mediante il conteggio delle righe.  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  
