---
title: Connettersi a un database modello tabulare di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 239559dc7d5bfdabe3a3f9060bc92059982c8dae
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072418"
---
# <a name="connect-to-a-tabular-model-database"></a>Connettersi a un database modello tabulare  
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Dopo aver compilato un modello tabulare e averlo distribuito in un server modello tabulare di Analysis Services, è necessario impostare le autorizzazioni per renderlo disponibile ad applicazioni client. Questo articolo illustra come le autorizzazioni e come connettersi a un database da applicazioni client.  
  
> [!NOTE]  
>  Per impostazione predefinita, le connessioni remote ad Analysis Services non sono disponibili finché non viene configurato il firewall. Accertarsi che sia aperta la porta appropriata se si configura un'istanza denominata o predefinita per connessioni client. Per altre informazioni, vedere [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
##  <a name="bkmk_userpermissions"></a> Autorizzazioni utente sul database  
 Gli utenti che si connettono a database tabulari devono disporre dell'appartenenza a un ruolo del database tramite cui viene specificato l'accesso in lettura.  
  
 I ruoli e talvolta l'appartenenza ai ruoli sono definiti quando si crea un modello in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]o, per i modelli distribuiti, tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sulla creazione dei ruoli tramite Gestione ruoli in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], vedere [creare e gestire ruoli](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md). Per altre informazioni sulla creazione e gestione dei ruoli per un modello distribuito, vedere [ruoli nei modelli tabulari](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md).  
  
> [!CAUTION]  
>  La ridistribuzione di un progetto di modello tabulare con i ruoli definiti tramite Gestione ruoli in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] sovrascriverà i ruoli definiti in un modello tabulare distribuito.  
  
##  <a name="bkmk_admin"></a> Autorizzazioni amministrative sul server  
 Per le organizzazioni in cui si utilizza SharePoint per ospitare cartelle di lavoro di Excel o report di Reporting Services, è necessaria una configurazione aggiuntiva per rendere disponibili i dati di modello tabulare agli utenti di SharePoint. Se non si utilizza SharePoint, ignorare questa sezione.  
  
 Per la visualizzazione delle cartelle di lavoro di Excel o dei report [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] in cui sono contenuti i dati tabulari, è necessario che l'account utilizzato per eseguire Excel Services o Reporting Services disponga di autorizzazioni di amministratore sull'istanza di Analysis Services. Le autorizzazioni amministrative sono necessarie affinché tali servizi siano considerati attendibili dall'istanza di Analysis Services.  
  
#### <a name="grant-administrative-access-on-the-server"></a>Concedere accesso come amministratore sul server  
  
1.  Aprire la pagina Configura account di servizio in Amministrazione centrale.  
  
2.  Selezionare il pool di applicazioni del servizio utilizzato da Excel Services. Potrebbe trattarsi **Pool di applicazioni di servizio - sistema dei servizi Web SharePoint** o un pool di applicazioni personalizzate. L'account gestito utilizzato da Excel Services sarà visualizzato nella pagina.  
  
     Per le farm di SharePoint in cui è incluso Reporting Services in modalità SharePoint, ottenere anche le informazioni sull'account per l'applicazione di servizio Reporting Services.  
  
     Nei passaggi seguenti si aggiungeranno questi account al ruolo server nell'istanza di Analysis Services.  
  
3.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], fare clic con il pulsante destro del mouse sull'istanza del server e selezionare **Proprietà**. Fare clic con il pulsante destro del mouse su **Ruoli** in Esplora oggetti e scegliere **Nuovo ruolo**.  
  
4.  Nella pagina Proprietà di Analysis Services fare clic su **Sicurezza**.  
  
5.  Fare clic su **Aggiungi**, quindi immettere l'account utilizzato da Excel Services, seguito dall'account utilizzato da Reporting Services.  
  
##  <a name="bkmk_excelconn"></a> Connessione da Excel o SharePoint  
 Per la connessione ai database modello eseguiti su un server in modalità tabulare, si possono utilizzare le librerie client tramite cui viene fornito accesso ai database di Analysis Services. Nelle librerie sono inclusi il provider OLE DB di Analysis Services, ADOMD.NET e AMO.  
  
 Il provider OLE DB viene utilizzato in Excel. Se è disponibile MSOLAP.4 da SQL Server 2008 R2 (nome file msolap100.dll, versione 10.50.1600.1) o MSOLAP.5 (nome file msolap110.dll) installato con la versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per Excel, si ha una versione che si connetterà ai database tabulari.  
  
 Per connettersi ai database modello da Excel, scegliere uno degli approcci seguenti:  
  
-   Creare una connessione dati da Excel, utilizzando le istruzioni fornite nella sezione successiva.  
  
-   Creare un file di connessione BISM (con estensione bism) in SharePoint tramite cui viene fornito il reindirizzamento a un database in esecuzione su un server in modalità tabulare di Analysis Services. Un file di connessione BISM dispone di un comando che con il pulsante destro del mouse consente di avviare Excel utilizzando il database modello specificato nella connessione. Se Reporting Services è installato, verrà inoltre avviato [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] . Per altre informazioni sulla creazione e l'uso di file di connessione BI Semantic Model, vedere [Creare una connessione BI Semantic Model a un database modello tabulare](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
-   Creare un'origine dati condivisa di Reporting Services che fa riferimento a un database tabulare come origine dati. È possibile creare l'origine dati condivisa in SharePoint e utilizzarla per avviare [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
#### <a name="connect-from-excel"></a>Connessione da Excel  
  
1.  In **Carica dati esterni** nella scheda **Dati**di Excel fare clic su **Da altre origini**.  
  
2.  Selezionare **Da Analysis Services**.  
  
3.  In **Nome server**specificare l'istanza di Analysis Services in cui viene ospitato il database. Il nome del server è spesso il nome del computer in cui è in esecuzione il software del server. Se il server è stato installato come istanza denominata, è necessario specificare il nome nel formato seguente: \<servername >\\< NomeIstanza\>.  
  
     L'istanza del server deve essere configurata per la distribuzione tabulare autonoma e deve disporre di una regola in ingresso che consenta l'accesso. Per altre informazioni, vedere [Determinare la modalità server di un'istanza di Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md) e [Configurare Windows Firewall per consentire l'accesso ad Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
4.  Per accedere alle credenziali, scegliere **Usa autenticazione di Windows** se si dispone di autorizzazioni di lettura al database. In caso contrario, scegliere **Usa nome utente e password seguenti**e immettere il nome utente e la password di un account di Windows che dispone di autorizzazioni di database. Scegliere **Avanti**.  
  
5.  Selezionare il database. Una selezione valida sarà quella in cui verrà mostrato un solo cubo **Modello** per il database. Fare clic su **Avanti** , quindi su **Fine**.  
  
 Dopo aver stabilito la connessione, è possibile utilizzare i dati per creare una tabella pivot o un grafico pivot. Per altre informazioni, vedere [analizza in Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_sharepoint"></a> Connessione da SharePoint  
 Se si usa [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, è possibile creare un file di connessione BI Semantic Model in SharePoint che fornisce il reindirizzamento a un database in esecuzione in un server in modalità tabulare di Analysis Services. Tramite una connessione BISM viene fornito un endpoint HTTP a un database. Inoltre viene semplificato l'accesso al modello tabulare per i knowledge worker che utilizzano regolarmente documenti su un sito di SharePoint. I knowledge worker devono conoscere solo il percorso del file di connessione BISM o del relativo URL per accedere ai database modello tabulare. I dettagli sul percorso server o sul nome del database sono incapsulati nella connessione BISM. Per altre informazioni sulla creazione e l'uso di file connessione BI Semantic Model, vedere [Connessione BI Semantic Model di PowerPivot &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md) e [Creare una connessione BI Semantic Model a un database modello tabulare](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_Tshoot"></a> Risoluzione dei problemi di connessione  
 In questa sezione vengono fornite informazioni sulla causa e sui passaggi per la risoluzione di problemi che si verificano durante la connessione a un database modello tabulare.  
  
 **Impossibile ottenere un elenco di database dall'origine dati specificata tramite la Connessione guidata dati.**  
  
 Quando si importano dati, si verifica questo errore di Microsoft Excel quando si prova a usare la procedura guidata per connettersi a un database modello tabulare in un server Analysis Services remoto e non si dispone delle autorizzazioni sufficienti. Per risolvere l'errore, è necessario disporre di diritti di accesso utente sul database. Fare riferimento alle istruzioni fornite precedentemente in questo argomento per concedere accesso utente ai dati.  
  
 **Errore durante il tentativo di stabilire una connessione all'origine dati esterna. Impossibile aggiornare le connessioni seguenti: \<nome modello > Sandbox**  
  
 In SharePoint questo errore di Microsoft Excel si verifica quando si tenta l'interazione dei dati, ad esempio l'applicazione di filtri a dati, in una tabella pivot in cui vengono utilizzati dati del modello. L'errore si verifica perché non si dispone di autorizzazioni sufficienti sul server Analysis Services remoto. Per risolvere l'errore, è necessario disporre di diritti di accesso utente sul database. Fare riferimento alle istruzioni fornite precedentemente in questo argomento per concedere accesso utente ai dati.  
  
 **Errore durante l'operazione. Ricaricare la cartella di lavoro e quindi provare a eseguire nuovamente l'operazione.**  
  
 In SharePoint questo errore di Microsoft Excel si verifica quando si tenta l'interazione dei dati, ad esempio l'applicazione di filtri a dati, in una tabella pivot in cui vengono utilizzati dati del modello. L'errore si verifica perché Excel Services non è considerato attendibile dall'istanza di Analysis Services nella quale vengono distribuiti i dati del modello. Per risolvere l'errore, concedere autorizzazioni amministrative di Excel Services sull'istanza di Analysis Services. Per concedere autorizzazioni di amministratore, fare riferimento alle istruzioni fornite precedentemente in questo argomento. Se l'errore persiste, riciclare il pool di applicazioni di Excel Services.  
  
 **Errore durante il tentativo di stabilire una connessione all'origine dati esterna utilizzata nella cartella di lavoro.**  
  
 In SharePoint questo errore di Microsoft Excel si verifica quando si tenta l'interazione dei dati, ad esempio l'applicazione di filtri a dati, in una tabella pivot in cui vengono utilizzati dati del modello. L'errore si verifica perché l'utente non dispone di autorizzazioni di SharePoint sufficienti sulla cartella di lavoro. L'utente deve disporre di autorizzazioni **Lettura** o superiori. Le autorizzazioni**Sola visualizzazione** non sono sufficienti per l'accesso ai dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di una soluzione del modello tabulare](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
