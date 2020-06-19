---
title: Aggiunta, eliminazione o condivisione di una gestione connessione in un pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], adding
- adding connection managers
ms.assetid: 6f2ba4ea-10be-4c40-9e80-7efcf6ee9655
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 4c132bc1715292a1dbd88d84813cefb3ca8616a4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926222"
---
# <a name="add-delete-or-share-a-connection-manager-in-a-package"></a>Aggiunta, eliminazione o condivisione di una gestione connessione in un pacchetto
  In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sono disponibili diverse gestioni connessioni per la connessione a origini dati diverse, ad esempio database relazionali, database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e file in formato CSV e XML. Una gestione connessione può essere creata al livello del pacchetto o al livello del progetto. La gestione connessione creata al livello del progetto è disponibile per tutti i pacchetti nel progetto. La gestione connessione creata al livello del pacchetto è invece disponibile per quel pacchetto specifico.  
  
 È possibile utilizzare le gestioni connessioni create a livello di progetto al posto delle origini dati per condividere le connessioni alle origini. Per aggiungere una gestione connessione a livello del progetto, nel progetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] deve essere utilizzato il modello di distribuzione del progetto. Quando un progetto viene configurato per usare questo modello, in **Esplora soluzioni** viene aggiunta la cartella **Gestioni connessioni** e rimossa la cartella **Origini dati** dal **Esplora soluzioni**.  
  
> [!NOTE]  
>  Se si desidera utilizzare le origini dati del pacchetto, è necessario convertire il progetto nel modello di distribuzione del pacchetto.  
>   
>  Per altre informazioni sui due modelli, vedere [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md). Per altre informazioni sulla conversione di un progetto nel modello di distribuzione del progetto, vedere [Distribuire progetti nel server Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 Le procedure riportate di seguito sono valide per tutti i tipi di gestioni connessioni e descrivono come eseguire le attività seguenti:  
  
-   [Per aggiungere una gestione connessione durante la creazione di un pacchetto](#wizard)  
  
-   [Per aggiungere una gestione connessione a un pacchetto esistente](#package)  
  
-   [Per aggiungere una gestione connessione al livello del progetto](#project)  
  
-   [Per creare un parametro per una proprietà della gestione connessione](#parameter)  
  
-   [Per eliminare una gestione connessione da un pacchetto](#DeletePackageLevel)  
  
-   [Per eliminare una gestione connessione condivisa (gestione connessione al livello del progetto)](#DeleteProjectLevel)  
  
##  <a name="to-add-a-connection-manager-when-creating-a-package"></a><a name="wizard"></a>Per aggiungere una gestione connessione durante la creazione di un pacchetto  
  
-   Utilizzare l'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
     Oltre a creare e configurare una gestione connessione, tramite la procedura guidata è anche possibile creare e configurare le origini e le destinazioni in cui è utilizzata la gestione connessione. Per altre informazioni, vedere [Creare pacchetti in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
##  <a name="to-add-a-connection-manager-to-an-existing-package"></a><a name="package"></a>Per aggiungere una gestione connessione a un pacchetto esistente  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Fare clic in un punto qualsiasi dell'area **Gestioni connessioni** , quindi eseguire una delle operazioni seguenti:  
  
    -   Fare clic sul tipo di gestione connessione da aggiungere al pacchetto.  
  
         -oppure-  
  
    -   Se il tipo desiderato non è incluso nell'elenco, fare clic su **Nuova connessione** . Verrà visualizzata la finestra di dialogo **Aggiungi gestione connessione SSIS** . Selezionare un tipo di gestione connessione, quindi fare clic su **OK**.  
  
     Verrà visualizzata la finestra di dialogo specifica per il tipo di gestione connessione selezionato. Per ulteriori informazioni sui tipi di gestione connessione e sulle opzioni disponibili, vedere la tabella seguente.  
  
    |Gestione connessione|Opzioni|  
    |------------------------|-------------|  
    |[Gestione connessione ADO](connection-manager/ado-connection-manager.md)|[Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gestione connessione ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configura gestione connessione ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Gestione connessione Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione Excel](connection-manager/excel-connection-manager.md)|[Editor gestione connessione Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Gestione connessione file](connection-manager/file-connection-manager.md)|[Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Gestione connessione per più file](connection-manager/multiple-files-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione file flat](connection-manager/flat-file-connection-manager.md)|[Editor gestione connessione file flat &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione per più file flat](connection-manager/multiple-flat-files-connection-manager.md)|[Editor gestione connessione per più file flat &#40;pagina Generale&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione FTP](connection-manager/ftp-connection-manager.md)|[Editor gestione connessione FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Gestione connessione HTTP](connection-manager/http-connection-manager.md)|[Editor gestione connessione HTTP &#40;pagina Server&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Gestione connessione MSMQ](connection-manager/msmq-connection-manager.md)|[Editor gestione connessione MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Gestione connessione ODBC](connection-manager/odbc-connection-manager.md)|[Riferimento all'interfaccia utente di Gestione connessione ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md)|[Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gestione connessione SMO](connection-manager/smo-connection-manager.md)|[Editor gestione connessione SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Gestione connessione SMTP](connection-manager/smtp-connection-manager.md)|[Editor gestione connessione SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Gestione connessione SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor gestione connessione SQL Server Compact Edition &#40;pagina Tutte&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gestione connessione WMI](connection-manager/wmi-connection-manager.md)|[Editor gestione connessione WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     Nell'area **Gestioni connessioni** è indicata la gestione connessione aggiunta.  
  
5.  Facoltativamente, fare clic con il pulsante destro del mouse sulla gestione connessione, scegliere **Rinomina**, quindi modificare il nome predefinito della gestione connessione.  
  
6.  Per salvare il pacchetto aggiornato scegliere **Salva elementi selezionati** dal menu **File** .  
  
##  <a name="to-add-a-connection-manager-at-the-project-level"></a><a name="project"></a>Per aggiungere una gestione connessione al livello del progetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  In **Esplora soluzioni**fare clic con il pulsante destro del mouse su **Gestioni connessioni**, quindi fare clic su **Nuova gestione connessione**.  
  
3.  Nella finestra di dialogo **Aggiungi gestione connessione SSIS** selezionare il tipo di gestione connessione, quindi scegliere **Aggiungi**.  
  
     Verrà visualizzata la finestra di dialogo specifica per il tipo di gestione connessione selezionato. Per ulteriori informazioni sui tipi di gestione connessione e sulle opzioni disponibili, vedere la tabella seguente.  
  
    |Gestione connessione|Opzioni|  
    |------------------------|-------------|  
    |[Gestione connessione ADO](connection-manager/ado-connection-manager.md)|[Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gestione connessione ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configura gestione connessione ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Gestione connessione Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione Excel](connection-manager/excel-connection-manager.md)|[Editor gestione connessione Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Gestione connessione file](connection-manager/file-connection-manager.md)|[Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Gestione connessione per più file](connection-manager/multiple-files-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione file flat](connection-manager/flat-file-connection-manager.md)|[Editor gestione connessione file flat &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione per più file flat](connection-manager/multiple-flat-files-connection-manager.md)|[Editor gestione connessione per più file flat &#40;pagina Generale&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione FTP](connection-manager/ftp-connection-manager.md)|[Editor gestione connessione FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Gestione connessione HTTP](connection-manager/http-connection-manager.md)|[Editor gestione connessione HTTP &#40;pagina Server&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Gestione connessione MSMQ](connection-manager/msmq-connection-manager.md)|[Editor gestione connessione MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Gestione connessione ODBC](connection-manager/odbc-connection-manager.md)|[Riferimento all'interfaccia utente di Gestione connessione ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md)|[Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gestione connessione SMO](connection-manager/smo-connection-manager.md)|[Editor gestione connessione SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Gestione connessione SMTP](connection-manager/smtp-connection-manager.md)|[Editor gestione connessione SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Gestione connessione SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor gestione connessione SQL Server Compact Edition &#40;pagina Tutte&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gestione connessione WMI](connection-manager/wmi-connection-manager.md)|[Editor gestione connessione WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
     La gestione connessione aggiunta verrà visualizzata sotto il nodo **Gestioni connessioni** in **Esplora soluzioni**. Verrà inoltre visualizzata nella scheda **Gestioni connessioni** nella finestra **Progettazione SSIS** per tutti i pacchetti nel progetto. Il nome della gestione connessione in questa scheda conterrà un prefisso **(progetto)** per differenziarla dalle gestioni connessioni al livello del pacchetto.  
  
4.  Facoltativamente, fare clic con il pulsante destro del mouse sulla gestione connessione nella finestra **Esplora soluzioni** sotto il nodo **Gestioni connessioni** (oppure) nella scheda **Gestioni connessioni** della finestra **Progettazione SSIS** , fare clic su **Rinomina**, quindi modificare il nome predefinito della gestione connessione.  
  
    > [!NOTE]  
    >  Nella scheda **gestioni connessioni** della finestra **Progettazione SSIS** non sarà possibile sovrascrivere il prefisso **(progetto)** dal nome della gestione connessione. Questo si verifica per motivi strutturali.  
  
##  <a name="to-create-a-parameter-for-a-connection-manager-property"></a><a name="parameter"></a>Per creare un parametro per una proprietà della gestione connessione  
  
1.  Nell'area **Gestioni connessioni** fare clic con il pulsante destro del mouse sulla gestione connessione per cui creare un parametro e scegliere **Imposta parametri**.  
  
2.  Configurare le impostazioni dei parametri nella finestra di dialogo **Imposta parametri** . Per altre informazioni, vedere [Finestra di dialogo Imposta parametri](../../2014/integration-services/parameterize-dialog-box.md).  
  
##  <a name="to-delete-a-connection-manager-from-a-package"></a><a name="DeletePackageLevel"></a>Per eliminare una gestione connessione da un pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Fare clic con il pulsante destro del mouse sulla gestione connessione da eliminare, quindi scegliere **Elimina**.  
  
     Se si elimina una gestione connessione utilizzata da un elemento del pacchetto, come un'attività Esegui SQL o un'origine OLE DB, si verificheranno i problemi seguenti:  
  
    -   Viene visualizzata un'icona di errore sull'elemento del pacchetto che utilizzava la gestione connessione eliminata.  
  
    -   La convalida del pacchetto non riesce.  
  
    -   Non è possibile eseguire il pacchetto.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
##  <a name="to-delete-a-shared-connection-manager-project-level-connection-manager"></a><a name="DeleteProjectLevel"></a>Per eliminare una gestione connessione condivisa (gestione connessione a livello di progetto)  
  
1.  Per eliminare una gestione connessione al livello del progetto, fare clic con il pulsante destro del mouse sotto il nodo **Gestioni connessioni** nella finestra **Esplora soluzioni** , quindi scegliere **Elimina**. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] visualizza il messaggio di avviso seguente:  
  
    > [!WARNING]  
    >  Quando si elimina una gestione connessione del progetto, è possibile che i pacchetti che utilizzano la gestione connessione non vengano eseguiti. Non è possibile annullare questa azione. Eliminare la gestione connessione?  
  
2.  Fare clic su OK per eliminare la gestione connessione o Annulla per mantenerla.  
  
    > [!NOTE]  
    >  È anche possibile eliminare una gestione connessione al livello del progetto dalla scheda **Gestione connessione** della finestra **Progettazione SSIS** aperta per i pacchetti del progetto. A tale scopo, fare clic con il pulsante destro del mouse sulla gestione connessione nella scheda, quindi scegliere **Elimina**.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;connessioni SSIS&#41;](connection-manager/integration-services-ssis-connections.md)   
 [Impostazione delle proprietà di una gestione connessione](../../2014/integration-services/set-the-properties-of-a-connection-manager.md)  
  
  
