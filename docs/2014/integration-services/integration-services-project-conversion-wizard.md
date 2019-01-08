---
title: Conversione guidata di progetto di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.migrationwizard.f1
ms.assetid: a192b094-4d0f-4c21-b911-460ec844a49f
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 252d8c44921db82cc634e17e1628f72f18a066e1
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52396365"
---
# <a name="integration-services-project-conversion-wizard"></a>Conversione guidata progetto di Integration Services
  Con la **Conversione guidata progetto di Integration Services** è possibile convertire un progetto nel modello di distribuzione del progetto.  
  
> [!NOTE]  
>  Se nel progetto sono incluse una o più origini dati, queste ultime vengono rimosse al completamento della conversione del progetto. Per creare una connessione a un'origine dati che può essere condivisa dai pacchetti nel progetto, aggiungere una gestione connessione al livello del progetto. Per altre informazioni, vedere [aggiungere, eliminare o condividere una gestione connessione in un pacchetto](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md).  
  
 **Per saperne di più**  
  
-   [Aprire la Conversione guidata progetti di Integration Services](#open_dialog)  
  
-   [Impostare le opzioni nella pagina Individua pacchetti](#locate)  
  
-   [Impostare le opzioni nella pagina Seleziona pacchetti](#selectPackages)  
  
-   [Impostare le opzioni nella pagina Seleziona destinazione](#destination)  
  
-   [Impostare le opzioni nella pagina Specificare le proprietà del progetto](#projectProperties)  
  
-   [Impostare le opzioni nella pagina Aggiorna attività Esegui pacchetto](#executePackage)  
  
-   [Impostare le opzioni nella pagina Seleziona configurazioni](#configurations)  
  
-   [Impostare le opzioni nella pagina Crea parametri](#createParameters)  
  
-   [Impostare le opzioni nella pagina Configura parametri](#configureParameters)  
  
-   [Impostare le opzioni nella pagina Verifica](#review)  
  
-   [Impostare le opzioni nella pagina Esegui conversione](#conversion)  
  
##  <a name="open_dialog"></a> Aprire la Conversione guidata progetti di Integration Services  
 Eseguire una delle operazioni seguenti per aprire la **Conversione guidata progetto di Integration Services** .  
  
-   Aprire il progetto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], quindi in Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Converti nel modello di distribuzione del progetto**.  
  
-   Da Esplora oggetti di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]fare clic con il pulsante destro del mouse sul nodo **Progetti** e selezionare **Importa pacchetto**.  
  
 Le diverse attività di conversione eseguite dalla **Conversione guidata progetto di Integration Services** variano a seconda che la procedura guidata venga eseguita da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o da [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
##  <a name="locate"></a> Impostare le opzioni nella pagina Individua pacchetti  
  
> [!NOTE]  
>  La pagina **Individua pacchetti** è disponibile solo quando si esegue la procedura guidata da [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 L'opzione seguente viene visualizzata nella pagina quando si seleziona **File system** nell'elenco a discesa **Origine** . Selezionare questa opzione se il pacchetto si trova nel file system.  
  
 **Cartella**  
 Digitare il percorso del pacchetto o passare al pacchetto facendo clic su **Sfoglia**.  
  
 Le opzioni seguenti vengono visualizzate nella pagina quando si seleziona **Archivio pacchetti SSIS** nell'elenco a discesa **Origine**. Per altre informazioni sull'archiviazione dei pacchetti, vedere [Gestione dei pacchetti &#40;servizio SSIS&#41;](service/package-management-ssis-service.md).  
  
 **Server**  
 Digitare il nome del server o selezionare il server.  
  
 **Cartella**  
 Digitare il percorso del pacchetto o passare al pacchetto facendo clic su **Sfoglia**.  
  
 Le opzioni seguenti vengono visualizzate nella pagina quando si seleziona **Microsoft SQL Server** nell'elenco a discesa **Origine** . Selezionare questa opzione se il pacchetto si trova in Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Server**  
 Digitare il nome del server o selezionare il server.  
  
 **Usa autenticazione di Windows**  
 Tale modalità consente di connettersi tramite un account utente di Windows. Se si utilizza l'autenticazione di Windows non è necessario specificare un nome utente o una password.  
  
 **Usa autenticazione di SQL Server**  
 Quando un utente si connette da una connessione non trusted con un nome di account di accesso e una password specificati, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autentica la connessione controllando se è stato impostato un account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e se la password specificata corrisponde a quella registrata in precedenza. Se non è stato impostato alcun account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , l'autenticazione non viene completata e viene segnalato un errore all'utente.  
  
 **Nome utente**  
 Specificare un nome utente quando si utilizza l'autenticazione di SQL Server.  
  
 **Password**  
 Specificare una password quando si utilizza l'autenticazione di SQL Server.  
  
 **Cartella**  
 Digitare il percorso del pacchetto o passare al pacchetto facendo clic su **Sfoglia**.  
  
##  <a name="selectPackages"></a> Impostare le opzioni nella pagina Seleziona pacchetti  
 **Nome pacchetto**  
 Viene elencato il file del pacchetto.  
  
 **Stato**  
 Viene indicato se un pacchetto è pronto per la conversione nel modello di distribuzione del progetto.  
  
 **Message**  
 Viene visualizzato un messaggio associato al pacchetto.  
  
 **Password**  
 Viene visualizzata una password associata al pacchetto. Il testo della password è nascosto.  
  
 **Applica a selezione**  
 Fare clic per applicare la password nella casella di testo **Password** ai pacchetti selezionati.  
  
 **Aggiorna**  
 Viene aggiornato l'elenco dei pacchetti.  
  
##  <a name="destination"></a> Impostare le opzioni nella pagina Seleziona destinazione  
 In questa pagina specificare il nome e il percorso di un nuovo file di distribuzione progetto (con estensione ispac) o selezionare un file esistente.  
  
> [!NOTE]  
>  La pagina **Seleziona destinazione** è disponibile solo quando si esegue la procedura guidata da [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 **Percorso di output**  
 Digitare il percorso del file di distribuzione o passare al file facendo clic su **Sfoglia**.  
  
 **Nome del progetto**  
 Digitare il nome del progetto.  
  
 **Livello di protezione**  
 Selezionare il livello di protezione. Per altre informazioni, vedere [Access Control for Sensitive Data in Packages](security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descrizione progetto**  
 Digitare una descrizione facoltativa per il progetto.  
  
##  <a name="projectProperties"></a> Impostare le opzioni nella pagina Specificare le proprietà del progetto  
  
> [!NOTE]  
>  La pagina **Specifica proprietà del progetto** è disponibile solo quando si esegue la procedura guidata da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Nome del progetto**  
 Viene elencato il nome del progetto.  
  
 **Livello di protezione**  
 Selezionare un livello di protezione per i pacchetti contenuti nel progetto. Per altre informazioni sui livelli di protezione, vedere [Controllo dell'accesso per dati sensibili nei pacchetti](security/access-control-for-sensitive-data-in-packages.md).  
  
 **Descrizione progetto**  
 Digitare una descrizione facoltativa del progetto.  
  
##  <a name="executePackage"></a> Impostare le opzioni nella pagina Aggiorna attività Esegui pacchetto  
 Aggiornare le attività Esegui pacchetto contenute nei pacchetti al fine di utilizzare un riferimento basato sul progetto. Per altre informazioni, vedere [Editor attività Esegui pacchetto](../../2014/integration-services/execute-package-task-editor.md).  
  
 **Pacchetto padre**  
 Viene elencato il nome del pacchetto tramite cui viene eseguito il pacchetto figlio utilizzando l'attività Esegui pacchetto.  
  
 **Nome attività**  
 Viene elencato il nome dell'attività Esegui pacchetto.  
  
 **Riferimento originale**  
 Viene elencato il percorso corrente del pacchetto figlio.  
  
 **Assegna riferimento**  
 Selezionare un pacchetto figlio archiviato nel progetto.  
  
##  <a name="configurations"></a> Impostare le opzioni nella pagina Seleziona configurazioni  
 Selezionare le configurazioni del pacchetto che si desidera sostituire con i parametri.  
  
 **Pacchetto**  
 Viene elencato il file del pacchetto.  
  
 **Tipo**  
 Viene elencato il tipo di configurazione, ad esempio un file di configurazione XML.  
  
 **Stringa di configurazione**  
 Viene elencato il percorso del file di configurazione.  
  
 **Stato**  
 Viene visualizzato un messaggio di stato per la configurazione. Fare clic sul messaggio per visualizzare il relativo testo completo.  
  
 **Aggiungi configurazioni**  
 Aggiungere le configurazioni del pacchetto contenute in altri progetti all'elenco delle configurazioni disponibili che si desidera sostituire con i parametri. È possibile selezionare le configurazioni archiviate in un file system o in SQL Server.  
  
 **Aggiorna**  
 Fare clic su questa opzione per aggiornare l'elenco delle configurazioni.  
  
 **Rimuovi configurazioni da tutti i pacchetti dopo la conversione**  
 È consigliabile rimuovere tutte le configurazioni dal progetto selezionando questa opzione.  
  
 Se non si seleziona questa opzione, vengono rimosse solo le configurazioni selezionate per la sostituzione con i parametri.  
  
##  <a name="createParameters"></a> Impostare le opzioni nella pagina Crea parametri  
 Selezionare il nome e l'ambito del parametro per ogni proprietà di configurazione.  
  
 **Pacchetto**  
 Viene elencato il file del pacchetto.  
  
 **Nome parametro**  
 Viene elencato il nome del parametro.  
  
 **Ambito**  
 Selezionare l'ambito del parametro, vale a dire pacchetto o progetto.  
  
##  <a name="configureParameters"></a> Impostare le opzioni nella pagina Configura parametri  
 **Name**  
 Viene elencato il nome del parametro.  
  
 **Ambito**  
 Viene elencato l'ambito del parametro.  
  
 **Valore**  
 Viene elencato il valore del parametro.  
  
 Fare clic sul pulsante con i puntini di sospensione accanto al campo del valore per configurare le proprietà del parametro.  
  
 Nella finestra di dialogo **Imposta dettagli parametri** è possibile modificare il valore del parametro. È anche possibile specificare se il valore del parametro deve essere fornito quando si esegue il pacchetto.  
  
 È possibile modificare il valore nella pagina **Parametri** della finestra di dialogo **Configura** in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]facendo clic sul pulsante Sfoglia accanto al parametro. Viene visualizzata la finestra di dialogo **Imposta valore parametro** .  
  
 Nella finestra di dialogo **Imposta dettagli parametri** sono inoltre elencati il tipo di dati del valore del parametro e l'origine del parametro.  
  
##  <a name="review"></a> Impostare le opzioni nella pagina Verifica  
 Usare la pagina **Verifica** per confermare le opzioni selezionate per la conversione del progetto.  
  
 **Precedente**  
 Fare clic su questo pulsante per modificare un'opzione.  
  
 **Converti**  
 Fare clic su questa opzione per convertire il progetto nel modello di distribuzione del progetto.  
  
##  <a name="conversion"></a> Impostare le opzioni nella pagina Esegui conversione  
 Nella pagina Esegui conversione viene mostrato lo stato della conversione del progetto.  
  
 **Azione**  
 Viene elencato un passaggio specifico della conversione.  
  
 **Risultato**  
 Viene elencato lo stato di ogni passaggio della conversione. Fare clic sul messaggio di stato per ulteriori informazioni.  
  
 La conversione del progetto non viene salvata fino al salvataggio del progetto in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 **Salva report**  
 Fare clic su questa opzione per salvare un riepilogo della conversione del progetto in un file con estensione xml.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md)  
  
  
