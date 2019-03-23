---
title: 'Passaggio 4: Aggiunta delle configurazioni dei pacchetti | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e04a5321-63d5-4ec5-85b9-cb4eaf6c87f6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1d98187fbe76e726dadfe163d75a27c51fd60e9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388335"
---
# <a name="step-4-adding-package-configurations"></a>Passaggio 4: Aggiunta di configurazioni pacchetto
  In questa attività si procederà all'aggiunta di una configurazione a ogni pacchetto. Le configurazioni consentono di aggiornare i valori delle proprietà dei pacchetti e gli oggetti dei pacchetti in fase di esecuzione.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include diversi tipi di configurazioni. È possibile archiviare le configurazioni in variabili di ambiente, voci del Registro di sistema, variabili definite dall'utente, tabelle di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e file XML. Per offrire maggiore flessibilità, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] supporta l'utilizzo di configurazioni indirette, ovvero l'utilizzo di una variabile di ambiente per specificare il percorso della configurazione nella quale sono specificati i valori effettivi. I pacchetti del progetto Deployment Tutorial utilizzano una combinazione di file di configurazione XML e configurazioni indirette. In un file di configurazione XML è possibile includere configurazioni per più proprietà e, quando opportuno, farvi riferimento con più pacchetti. In questa esercitazione verrà utilizzato un file di configurazione separato per ogni pacchetto.  
  
 Nei file di configurazione sono spesso contenute informazioni riservate, ad esempio le stringhe di connessione. È pertanto consigliabile utilizzare un elenco di controllo di accesso per limitare l'accesso al percorso o alla cartella in cui vengono archiviati i file e concederlo solo a utenti o account autorizzati a eseguire i pacchetti. Per altre informazioni, vedere [Accesso ai file utilizzati dai pacchetti](../../2014/integration-services/access-to-files-used-by-packages.md).  
  
 Le configurazioni sono necessarie per eseguire correttamente dopo la distribuzione nel server di destinazione i pacchetti DataTransfer e LoadXMLData aggiunti al progetto Deployment Tutorial nell'attività precedente. Per implementare le configurazioni, verranno innanzitutto create le configurazioni indirette per i file di configurazione XML che verranno successivamente creati.  
  
 Si creeranno due file di configurazione, DataTransferConfig.dtsConfig e LoadXMLData.dtsConfig. Questi file contengono coppie nome/valore che aggiornano le proprietà in pacchetti che specificano il percorso dei dati e i file di log utilizzati dal pacchetto. Nell'ambito del successivo processo di distribuzione si procederà all'aggiornamento dei valori nei file di configurazione affinché riflettano il nuovo percorso dei file nel computer di destinazione.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] riconosce DataTransferConfig.dtsConfig e LoadXMLData.dtsConfig come dipendenze dei pacchetti DataTransfer e LoadXMLData e include automaticamente i file di configurazione nel pacchetto di distribuzione che verrà creato nella lezione successiva.  
  
### <a name="to-create-indirect-configuration-for-the-datatransfer-package"></a>Per creare la configurazione indiretta per il pacchetto DataTransfer  
  
1.  In Esplora soluzioni fare doppio clic su DataTransfer.dtsx.  
  
2.  Nella finestra di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo.  
  
3.  Scegliere **Configurazioni pacchetto** dal menu **SSIS**.  
  
4.  Nella finestra di dialogo **Libreria configurazioni pacchetto**selezionare **Abilita configurazioni pacchetto** , se non è già selezionata, e quindi fare clic su **Aggiungi**.  
  
5.  Nella pagina iniziale di Configurazione guidata pacchetto fare clic su **Avanti**.  
  
6.  Nella pagina Selezione tipo di configurazione, selezionare **file di configurazione XML** nel **tipo di configurazione** , selezionare il **percorso della configurazione memorizzato in una variabile di ambiente** opzione e digitare `DataTransfer,` oppure selezionare la **DataTransfer** variabile di ambiente nell'elenco.  
  
    > [!NOTE]  
    >  Dopo aver aggiunto la variabile di ambiente, potrebbe essere necessario riavviare il computer affinché risulti disponibile nell'elenco. Se non si desidera riavviare il computer, è possibile digitare il nome della variabile di ambiente.  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina Completamento procedura guidata digitare **DataTransfer EV Configuration** nella casella **Nome configurazione** , esaminare il contenuto della configurazione nel riquadro **Anteprima** e quindi fare clic su **Fine**.  
  
9. Chiudere la finestra di dialogo **Libreria configurazioni pacchetto**.  
  
### <a name="to-create-the-xml-configuration-for-the-datatransfer-package"></a>Per creare il file di configurazione XML per il pacchetto DataTransfer  
  
1.  In Esplora soluzioni fare doppio clic su DataTransfer.dtsx.  
  
2.  Nella finestra di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo.  
  
3.  Scegliere **Configurazioni pacchetto** dal menu **SSIS**.  
  
4.  Nella finestra di dialogo Libreria configurazioni pacchetto selezionare **Abilita configurazioni pacchetto** e quindi fare clic su **Aggiungi**.  
  
5.  Nella pagina iniziale di Configurazione guidata pacchetto fare clic su **Avanti**.  
  
6.  Nella pagina Selezione tipo di configurazione selezionare **File di configurazione XML** nell'elenco **Tipo di configurazione** e quindi fare clic su **Sfoglia**.  
  
7.  Nella finestra di dialogo **Selezionare il percorso del file di configurazione** passare a C:\DeploymentTutorial e digitare **DataTransferConfig** nella casella **Nome file** e quindi fare clic su **Salva**.  
  
8.  Nella pagina Selezione tipo di configurazione fare clic su **Avanti**.  
  
9. Nella pagina Selezione proprietà da esportare espandere DataTransfer, Gestioni connessioni, Deployment Tutorial Log e Properties e quindi selezionare la casella di controllo **Stringa di connessione** .  
  
10. In Gestioni connessioni espandere NewCustomers e quindi selezionare la casella di controllo **Stringa di connessione** .  
  
11. Scegliere **Avanti**.  
  
12. Nella pagina Completamento procedura guidata digitare **DataTransfer Configuration** nella casella **Nome configurazione** , esaminare il contenuto della configurazione e quindi fare clic su **Fine**.  
  
13. Nella finestra di dialogo **Libreria configurazioni pacchetto** verificare che DataTransfer EV Configuration sia elencata per prima e DataTransfer Configuration per seconda e quindi fare clic su **Chiudi**.  
  
### <a name="to-create-indirect-configuration-for-the-loadxmldata-package"></a>Per creare la configurazione indiretta per il pacchetto LoadXMLData  
  
1.  In Esplora soluzioni fare doppio clic sul pacchetto LoadXMLData.dtsx.  
  
2.  Nella finestra di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo.  
  
3.  Scegliere **Configurazioni pacchetto** dal menu **SSIS**.  
  
4.  Nella finestra di dialogo **Libreria configurazioni pacchetto**fare clic su **Aggiungi**.  
  
5.  Nella pagina iniziale di Configurazione guidata pacchetto fare clic su **Avanti**.  
  
6.  Nella pagina Selezione tipo di configurazione, selezionare **file di configurazione XML** nel **tipo di configurazione** , selezionare il **percorso della configurazione memorizzato in una variabile di ambiente** opzione, digitare `LoadXMLData` oppure selezionare il `LoadXMLData` variabile di ambiente nell'elenco.  
  
    > [!NOTE]  
    >  Dopo aver aggiunto la variabile di ambiente, potrebbe essere necessario riavviare il computer affinché risulti disponibile nell'elenco.  
  
7.  Scegliere **Avanti**.  
  
8.  Nella pagina Completamento procedura guidata digitare **LoadXMLData EV Configuration** nella casella **Nome configurazione** , esaminare il contenuto della configurazione e quindi fare clic su **Fine**.  
  
### <a name="to-create-the-xml-configuration-for-the-loadxmldata-package"></a>Per creare il file di configurazione XML per il pacchetto LoadXMLData  
  
1.  In Esplora soluzioni fare doppio clic sul pacchetto LoadXMLData.dtsx.  
  
2.  Nella finestra di Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic in un punto qualsiasi dello sfondo dell'area di progettazione del flusso di controllo.  
  
3.  Scegliere **Configurazioni pacchetto** dal menu **SSIS**.  
  
4.  Nella finestra di dialogo Libreria configurazioni pacchetto selezionare **Abilita configurazioni pacchetto** e quindi fare clic su **Aggiungi**.  
  
5.  Nella pagina iniziale di Configurazione guidata pacchetto fare clic su **Avanti**.  
  
6.  Nella pagina Selezione tipo di configurazione selezionare **File di configurazione XML** nell'elenco **Tipo di configurazione** e quindi fare clic su **Sfoglia**.  
  
7.  Nella finestra di dialogo **Selezionare il percorso del file di configurazione** passare a C:\DeploymentTutorial e digitare **LoadXMLDataConfig** nella casella **Nome file** e quindi fare clic su **Salva**.  
  
8.  Nella pagina Selezione tipo di configurazione fare clic su **Avanti**.  
  
9. Nella pagina Selezione proprietà da esportare espandere LoadXMLData, File eseguibili, Load XML Data e Properties, quindi selezionare le caselle di controllo **[XMLSource].[XMLData]** e **[XMLSource].[XMLSchemaDefinition]** .  
  
10. Scegliere **Avanti**.  
  
11. Nella pagina Completamento procedura guidata digitare **LoadXMLData Configuration** nella casella **Nome configurazione** , esaminare il contenuto della configurazione e quindi fare clic su **Fine**.  
  
12. Nella finestra di dialogo **Libreria configurazioni pacchetto** verificare che LoadXMLData EV Configuration sia elencata per prima e LoadXMLData Configuration per seconda e quindi fare clic su **Chiudi**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Passaggio 5: Test dei pacchetti aggiornati](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
![Icona di Integration Services (piccola)](media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [SSIS](../../2014/integration-services/package-configurations.md)   
 [Creazione di configurazioni dei pacchetti](../../2014/integration-services/create-package-configurations.md)   
 [Accesso ai file utilizzati dai pacchetti](../../2014/integration-services/access-to-files-used-by-packages.md)  
  
  
