---
title: Creare una connessione BI Semantic Model a un Database modello tabulare | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 69b306f6-ee8a-44d2-8f51-0cad2c0bc135
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f058516059c0cadf92b9d558a47990af0a54725f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071656"
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>Creare una connessione BISM a un database modello tabulare
  Utilizzare le informazioni fornite in questo argomento per impostare una connessione BISM che esegue il reindirizzamento a un database modello tabulare in esecuzione in un'istanza di Analysis Services esterna alla farm di SharePoint.  
  
 Dopo avere creato una connessione BISM e configurato le autorizzazioni di SharePoint e Analysis Services, sarà possibile utilizzare la connessione come origine dati per i report di Excel o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 In questo argomento sono incluse le sezioni seguenti. Eseguire ogni attività nell'ordine indicato.  
  
 [Verificare i prerequisiti](#bkmk_prereq)  
  
 [Concedere autorizzazioni amministrative di Analysis Services alle applicazioni di servizi condivisi](#bkmk_ssas)  
  
 [Concedere autorizzazioni di lettura per il database modello tabulare](#bkmk_BISM)  
  
 [Creare una connessione BISM a un database modello tabulare](#bkmk_connect)  
  
 [Configurare autorizzazioni di SharePoint sulla connessione BISM](#bkmk_permissions)  
  
 [Passaggi successivi](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> Verificare i prerequisiti  
 Per creare un file di connessione BISM, è necessario disporre delle autorizzazioni di collaborazione.  
  
 È necessario disporre di una raccolta che supporta il tipo di contenuto della connessione BISM. Per altre informazioni, vedere [aggiungere una BI Semantic Model tipo di contenuto connessione a una raccolta &#40;PowerPivot per SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md).  
  
 È necessario conoscere il nome del server e del database per il quale si imposta una connessione BISM. È necessario configurare Analysis Services per la modalità tabulare. I database in esecuzione nel server devono essere database modello tabulare. Per istruzioni su come controllare la modalità server, vedere [Determinare la modalità server di un'istanza di Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 In scenari determinati, i servizi condivisi in un ambiente SharePoint devono disporre di autorizzazioni amministrative sull'istanza di Analysis Services. I servizi includono le applicazioni del servizio PowerPivot, le applicazioni del servizio Reporting Services e le applicazioni del servizio PerformancePoint. Prima di poter concedere autorizzazioni amministrative, è necessario conoscere l'identità di queste applicazioni di servizio. È possibile utilizzare Amministrazione centrale per determinare l'identità.  
  
 È necessario essere un amministratore del servizio SharePoint per visualizzare informazioni sulla sicurezza in Amministrazione centrale.  
  
 È necessario essere un amministratore di sistema di Analysis Services per concedere diritti amministrativi in Management Studio.  
  
 È necessario accedere a PowerPivot per SharePoint tramite applicazioni Web che utilizzano la modalità di autenticazione classica. Le connessioni BISM alle origini dati esterne dispongono di una dipendenza sull'accesso in modalità classica. Per altre informazioni, vedere [PowerPivot Authentication and Authorization](power-pivot-authentication-and-authorization.md).  
  
 Tutti i computer e gli utenti che partecipano nella sequenza di connessione devono essere nello stesso dominio o nel dominio attendibile (attendibilità bidirezionale).  
  
##  <a name="bkmk_ssas"></a> Concedere autorizzazioni amministrative di Analysis Services alle applicazioni di servizi condivisi  
 Le connessioni provenienti da SharePoint a un database modello tabulare su un server Analysis Services vengono talvolta effettuate da un servizio condiviso per conto dell'utente che richiede i dati. Il servizio che effettua la richiesta potrebbe essere un'applicazione del servizio PowerPivot, un'applicazione del servizio Reporting Services o un'applicazione del servizio PerformancePoint. Affinché la connessione abbia esito positivo, è necessario che il servizio disponga delle autorizzazioni amministrative sul server Analysis Services. In Analysis Services solo un amministratore può effettuare una connessione rappresentata per conto di un altro utente.  
  
 Le autorizzazioni amministrative sono necessarie quando la connessione viene utilizzata in presenza delle condizioni indicate di seguito.  
  
-   Quando si verificano le informazioni di connessione durante la configurazione di un file di connessione BISM.  
  
-   Quando si avvia un report di Power View utilizzando una connessione BISM.  
  
-   Quando si popola una Web part di PerformancePoint utilizzando una connessione BISM.  
  
 Per assicurarsi che questi comportamenti vengano eseguiti come previsto, concedere ciascuna autorizzazione amministrativa di identità di servizio sull'istanza di Analysis Services. Utilizzare le istruzioni seguenti per la concessione dell'autorizzazione necessaria.  
  
 **Aggiungere le identità del servizio al ruolo di amministratore del server**  
  
1.  In SQL Server Management Studio connettersi all'istanza di Analysis Services.  
  
2.  Fare clic con il pulsante destro del mouse sul nome del server e scegliere **Proprietà**.  
  
3.  Fare clic su **Sicurezza**, quindi su **Aggiungi**. Immettere l'account utente di Windows utilizzato per eseguire l'applicazione del servizio.  
  
     È possibile utilizzare Amministrazione centrale per determinare l'identità. Aprire la pagina **Configura account di servizio** nella sezione Sicurezza per visualizzare l'account di Windows associato ai pool di applicazioni di servizio usato per ogni applicazione, quindi seguire le istruzioni fornite nell'argomento per concedere le autorizzazioni amministrative dell'account.  
  
##  <a name="bkmk_BISM"></a> Concedere autorizzazioni di lettura per il database modello tabulare  
 Poiché il database è in esecuzione in un server esterno alla farm, parte dell'impostazione delle connessioni includerà la concessione di autorizzazioni dell'utente di database sul server Analysis Services di back-end. In Analysis Services viene utilizzato un modello di autorizzazione basato sui ruoli. Gli utenti che si connettono ai database modello devono eseguire questa operazione con le autorizzazioni di lettura, o superiori, tramite un ruolo che concede accesso in lettura ai relativi membri.  
  
 I ruoli e talvolta l'appartenenza ai ruoli sono definiti quando si crea il modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Non è possibile utilizzare SQL Server Management Studio per creare ruoli, ma è possibile utilizzarlo per aggiungere membri a un ruolo già definito. Per altre informazioni sulla creazione di ruoli, vedere [Creare e gestire ruoli &#40; SSAS tabulare&#41;](../tabular-models/roles-ssas-tabular.md).  
  
#### <a name="assign-role-membership"></a>Assegnare le appartenenze a ruoli  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il database in Esplora oggetti, quindi espandere **Ruoli**. Sarà visualizzato un ruolo già definito. Se un ruolo non esiste, contattare l'autore del modello e richiedere l'aggiunta o un ruolo. È necessario ridistribuire il modello per rendere visibile il ruolo in Management Studio.  
  
2.  Fare clic con il pulsante destro del mouse sul ruolo, quindi scegliere **Proprietà**.  
  
3.  Nella pagina Appartenenza aggiungere gli account utenti e gruppi di Windows che richiedono l'accesso.  
  
##  <a name="bkmk_connect"></a> Creare una connessione BISM a un database modello tabulare  
 Dopo avere impostato le autorizzazioni in Analysis Services, è possibile tornare a SharePoint e creare una connessione BISM.  
  
1.  Nella raccolta che conterrà la connessione BISM, fare clic su **Documenti** sulla barra multifunzione di SharePoint.  
  
2.  Fare clic sulla freccia in giù su Nuovo documento e selezionare **File di connessione BI Semantic Model** per aprire la pagina Nuova connessione BI Semantic Model.  
  
3.  Impostare le proprietà **Server** e **Database** . In caso di dubbi sul nome del database, utilizzare SQL Server Management Studio per visualizzare un elenco dei database distribuiti nel server.  
  
     **Nome server** è il nome di rete del server, l'indirizzo IP o il nome di dominio completo, ad esempio myserver.mydomain.corp.adventure-works.com. Se il server viene installato come istanza denominata, immettere il nome del server nel formato nomecomputer\nomeistanza.  
  
     **Database** deve essere un database tabulare attualmente disponibile sul server. Non specificare un altro file di connessione BISM, un file di connessione dati (con estensione odc), un database OLAP di Analysis Services o una cartella di lavoro di PowerPivot. Per ottenere il nome del database, è possibile utilizzare Management Studio per connettersi al server e visualizzare l'elenco dei database disponibili. Utilizzare la pagina delle proprietà del database per verificare che il nome sia corretto.  
  
4.  Fare clic su **OK** per salvare la pagina. In questa fase, l'applicazione del servizio PowerPivot verificherà la connessione.  
  
     La verifica riesce se le informazioni di connessione sono corrette e sono state concesse le autorizzazioni amministrative all'applicazione del servizio PowerPivot in modo che si possa connettere a Analysis Services come utente corrente.  
  
     La verifica non riesce se le informazioni di connessione sono errate o se all'applicazione di servizio mancano le autorizzazioni. Un messaggio di convalida sarà visualizzato sulla pagina con la richiesta di salvare il file. Se la connessione è valida, è necessario salvare in ogni modo il file perché l'errore è il risultato di autorizzazioni mancanti anziché informazioni di connessione non valide.  
  
     È possibile verificare la connessione utilizzando Excel o Power View per connettersi a database modello tabulare. Se la connessione all'origine dati riesce, la connessione è valida nonostante l'avviso della verifica.  
  
##  <a name="bkmk_permissions"></a> Configurare autorizzazioni di SharePoint sulla connessione BISM  
 Per utilizzare una connessione BISM come origine dati per una cartella di lavoro di Excel o un report di Reporting Services, sono necessarie autorizzazioni **Lettura** sull'elemento della connessione BISM in una raccolta di SharePoint. Nel livello di autorizzazione di lettura è inclusa l'autorizzazione **Apertura elementi** che consente di scaricare le informazioni sulla connessione BISM in un'applicazione desktop di Excel.  
  
 Sono disponibili diversi modi per concedere le autorizzazioni in SharePoint. Le istruzioni seguenti illustrano come creare un nuovo gruppo denominato **Utenti BISM** con il livello di autorizzazione di **lettura** .  
  
 Per modificare le autorizzazioni è necessario essere proprietari del sito.  
  
1.  In Azioni sito fare clic su **Autorizzazioni sito**.  
  
2.  Fare clic su **Crea gruppo** e assegnare al nuovo gruppo il nome **Utenti BISM**.  
  
3.  Scegliere il livello di autorizzazione **Lettura** e fare clic su **Crea**.  
  
4.  Selezionare **Utenti BISM** in Utenti e gruppi.  
  
5.  Scegliere Nuovo, fare clic su **Aggiungi utenti**, quindi aggiungere account utente o di gruppo.  
  
     Questi utenti e gruppi disporranno di autorizzazioni di lettura per tutto il sito, incluse tutte le raccolte e gli elenchi che ereditano le autorizzazioni dal livello del sito. Se tali autorizzazioni sono troppo elevate, è possibile rimuovere selettivamente il gruppo da raccolte, elenchi o elementi specifici.  
  
 Per rimuovere selettivamente le autorizzazioni al livello dell'elemento, effettuare le operazioni seguenti:  
  
1.  In una raccolta, selezionare un documento. Fare clic sulla freccia GIÙ a destra e scegliere **Gestisci autorizzazioni**.  
  
2.  Per impostazione predefinita, un elemento eredita le autorizzazioni. Per modificare le autorizzazioni di singoli documenti in questa raccolta, fare clic su **Interrompi ereditarietà autorizzazioni**.  
  
3.  Selezionare la casella di controllo accanto a **Utenti BISM**.  
  
4.  Fare clic su **Rimuovi autorizzazioni utente**.  
  
##  <a name="bkmk_next"></a> Passaggi successivi  
 Dopo avere creato e protetto una connessione BISM è possibile specificarla come origine dati. Per altre informazioni, vedere [Utilizzare una connessione BISM (BI Semantic Model) in Excel o Reporting Services](use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione BI Semantic Model di PowerPivot &#40;con estensione bism&#41;](power-pivot-bi-semantic-model-connection-bism.md)   
 [Creare una connessione BISM (BI Semantic Model) a una cartella di lavoro di PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
