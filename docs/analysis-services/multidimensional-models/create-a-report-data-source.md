---
title: Creare un'origine dati Report | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b6e811f9114a484f7b0b68ca9782b9b60e366383
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866887"
---
# <a name="create-a-report-data-source"></a>Creare un'origine dati per il report
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Per connettere Power View a un modello multidimensionale, è necessario creare una definizione condivisa di origine dati del report (file con estensione rsds) in una raccolta di SharePoint. Il file con estensione rsds specifica il nome di un'istanza del server Analysis Services, un tipo di connessione, una stringa di connessione e le credenziali utilizzate per connettersi al modello multidimensionale. Quando un utente fa clic sul file con estensione rsds, viene visualizzato nel browser un nuovo report Power View (file con estensione rdlx) vuoto.  
  
 Per creare una connessione rsds, è necessario disporre di Reporting Services di SQL Server 2012 o versione successiva e il componente aggiuntivo Reporting Services per SharePoint 2010 o SharePoint 2013 installato.  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>Creare una connessione rsds dell'origine dati del report al modello multidimensionale  
 Prima di iniziare, è necessario conoscere:  
  
-   Il nome dell'istanza del server Analysis Services in esecuzione in modalità multidimensionale.  
  
-   Il nome del database multidimensionale a cui si desidera connettersi.  
  
-   Il nome del cubo, se ne è disponibile più di uno.  
  
-   (Facoltativo) Il nome della prospettiva.  
  
-   (Facoltativo) L'identificatore delle impostazioni locali.  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>Per creare un file con estensione rsds condiviso dell'origine dati del report (SharePoint 2010)  
  
1.  Nella barra multifunzione della libreria fare clic sulla scheda **Documenti** .  
  
2.  Fare clic su **Nuovo documento** > **Origine dati report**.  
  
    > [!NOTE]  
    >  Se la voce **Origine dati report** non compare nel menu, il tipo di contenuto dell'origine dati del report non è stato abilitato per questa libreria. Per altre informazioni, vedere [Aggiungere i tipi di contenuto di Reporting Services a una raccolta di SharePoint](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  Nella pagina **Proprietà origine dati** , in **Nome**, digitare un nome per il file di connessione con estensione rsds.  
  
4.  In **Tipo di origine dati**selezionare **Microsoft BI Semantic Model for Power View**.  
  
5.  In **Stringa di connessione**, specificare il nome del server Analysis Services, il nome del database, il nome del cubo e le impostazioni facoltative.  
  
     Stringa di connessione: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'`  
  
    > [!NOTE]  
    >  Se è presente più di un cubo, è necessario specificare il nome di un cubo.  
  
     (Facoltativo) I cubi possono avere prospettive che forniscono agli utenti una vista di selezione in cui sono visibili solo determinate dimensioni e/o gruppi di misure nel client. Per specificare una prospettiva, immettere il nome di prospettiva come valore per la proprietà Cube: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>'`  
  
     (Facoltativo) I cubi possono presentare metadati e traduzioni di dati specificati per varie lingue all'interno del modello. Per visualizzare le traduzioni (dati e metadati) è necessario aggiungere la proprietà "Locale Identifier" alla stringa di connessione: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'; Locale Identifier=<identifier number>`  
  
6.  In **Credenziali**specificare la modalità con cui il server di report ottiene le credenziali per l'accesso all'origine dati esterna.  
  
    -   Selezionare **Autenticazione di Windows (integrata)** se si desidera accedere ai dati usando le credenziali dell'utente che ha aperto il report. Non selezionare questa opzione se il sito o la farm di SharePoint utilizza l'autenticazione basata su form o si connette al server di report tramite un account attendibile. Non selezionare questa opzione se si desidera pianificare una sottoscrizione o l'elaborazione di dati per il report. È consigliabile utilizzare questa opzione quando per il dominio è abilitata l'autenticazione Kerberos oppure quando l'origine dei dati si trova nello stesso computer del server di report. Se l'autenticazione Kerberos non è attivata, le credenziali di Windows possono essere passate a un solo altro computer. Ciò significa che se l'origine dei dati esterna è in un altro computer, e richiede pertanto una connessione aggiuntiva, al posto dei previsti verrà restituito un errore.  
  
    -   Selezionare **Richiedi credenziali** se si vuole che l'utente immetta le proprie credenziali ogni volta che esegue il report. Non selezionare questa opzione se si desidera pianificare una sottoscrizione o l'elaborazione di dati per il report.  
  
    -   Selezionare **Credenziali archiviate** se si preferisce accedere ai dati usando un unico set di credenziali. Le credenziali vengono crittografate prima dell'archiviazione. È possibile selezionare opzioni che determinano la modalità di autenticazione delle credenziali archiviate. Selezionare Usa come credenziali di Windows se le credenziali archiviate appartengono all'account utente di Windows. Selezionare **Imposta contesto di esecuzione sull'account seguente** se si desidera impostare il contesto di esecuzione sul server di database.  
  
    -   Selezionare **Credenziali non necessarie** per specificare le credenziali nella stringa di connessione o eseguire il report usando un account con privilegi minimi.  
  
7.  Fare clic su **Test connessione** per convalidare.  
  
8.  Selezionare **Abilita questa origine dati** se si desidera che l'origine dati sia attiva. Se l'origine dati è configurata, ma non attiva, verrà visualizzato un messaggio di errore quando si tenta di creare un report.  
  
  
