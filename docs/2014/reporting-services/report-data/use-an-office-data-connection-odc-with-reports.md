---
title: Usare una connessione Office Data Connection (ODC) con i report (Reporting Services in modalità integrata SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Office Data Connection (.odc) files
- SharePoint integration [Reporting Services], shared data sources
- .odc files
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 983f60396f48e488b20e25f18751f615ded799ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106957"
---
# <a name="use-an-office-data-connection-odc-with-reports-reporting-services-in-sharepoint-integrated-mode"></a>Utilizzare una connessione Office Data Connection (odc) ai report (Reporting Services in modalità integrata SharePoint)
  In particolari scenari è possibile utilizzare un file Office Data Connection (odc) esistente per fornire informazioni di connessione a un report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Quando si vuole creare un'origine dati condivisa, è possibile usare un file con estensione odc al posto di un file con estensione rsds. Nel server di report il file con estensione odc viene infatti utilizzato in modo analogo del file con estensione rsds, ovvero per il recupero del tipo dell'origine dati, della stringa di connessione e delle informazioni relative alle credenziali.  
  
 Non tutti i file odc possono essere usati con un report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La possibilità di utilizzare o meno un file con estensione odc è determinata dall'estensione per l'elaborazione dei dati nonché dalle caratteristiche del report e del file stesso:  
  
-   Il report deve essere progettato per l'utilizzo con un provider di dati OLE DB o ODBC. Se per la creazione del report era stata utilizzata un'altra estensione per l'elaborazione dati, è possibile che il report o le relative query includano funzionalità non supportate dal provider di dati OLE DB o ODBC.  
  
-   Il file odc deve presentare la struttura e gli elementi previsti. Le impostazioni relative alle credenziali e al provider di dati devono essere impostate esplicitamente nel file in modo che possano essere lette dal server di report. Il modo migliore per impostare tali valori consiste nell'esportare il file odc prima di caricarlo nella raccolta di SharePoint.  
  
-   Il file odc deve specificare una connessione di tipo OLE DB o ODBC.  
  
-   Nel file odc deve essere specificata una stringa di connessione.  
  
-   Le credenziali possono essere impostate su `None`, `Stored` o `Integrated`. Se per le credenziali è selezionata l'opzione `Stored`, anziché utilizzare le credenziali archiviate il server di report visualizzerà un messaggio per richiederle all'utente, perché non è in grado di utilizzare credenziali archiviate definite nel file con estensioni odc.  
  
-   Lo schema dell'origine dati deve essere identico a quello utilizzato per creare il report. Se le strutture di dati sono diverse, il report non verrà eseguito.  
  
-   Il file con estensione odc deve essere creato in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007. Le versioni precedenti di tale file non sono compatibili con i file di definizione del report.  
  
 Non è possibile utilizzare file odc che specificano connessioni a origini dati che non possono essere elaborate in un server di report, anche se i tipi di origini dati specificati nei file odc sono simili ai tipi di origini dati supportati. In particolare, se si crea in Microsoft Excel 2007 un file con estensione odc che recupera dati da Microsoft Access, dal Web o da un file di testo, non sarà possibile utilizzarlo per fornire dati a un report.  
  
 I report e i modelli di Generatore report non supportano i file con estensione odc. Non è possibile utilizzare un file odc per generare un modello, né configurare un modello per l'utilizzo di un'origine dati condivisa collegata a un file odc.  
  
 Se non si ha alcuna familiarità con i file odc, è possibile seguire le istruzioni seguenti per creare ed esportare un file odc. Uno dei metodi più semplici per creare un file odc per un'origine dati OLE DB consiste nell'utilizzare Excel 2007 e la Connessione guidata dati. Si noti che tale procedura guidata non consente di creare un'origine dati. È pertanto necessario disporre di un'origine dati esterna definita in precedenza.  
  
 È possibile utilizzare un file odc esistente solo se è completamente compatibile con il report e le query. Se vengono generati errori che richiedono una modifica significativa del report o del file odc, sarà necessario creare un nuovo file rsds per il report. Per altre informazioni sulla creazione di un'origine dati condivisa che usa un file rsds, vedere [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-and-export-an-odc-file"></a>Per creare ed esportare un file odc  
  
1.  Avviare Excel 2007.  
  
2.  Nel gruppo **Carica dati esterni** della scheda **Dati** fare clic su **Da altre origini**e quindi su **Da Connessione guidata dati**.  
  
3.  Selezionare **Altri server/Opzioni avanzate**e quindi fare clic su **Avanti**.  
  
4.  Selezionare **Provider Microsoft OLE DB per SQL Server**e quindi fare clic su **Avanti**.  
  
5.  Specificare il nome del server, che per impostazione predefinita è il nome di rete del computer, e un account utente dotato di un account di accesso valido e autorizzazioni per il database. Fare clic su **Avanti**.  
  
6.  Selezionare un database e quindi fare clic su **OK** per chiudere la finestra di dialogo **Collegamento dati** .  
  
7.  La casella di controllo **Connetti a una tabella specifica** è selezionata per impostazione predefinita e consente di recuperare dati da una tabella specifica. Poiché il server di report ignora tutte le query presenti in un file odc, lo stato di selezione di tale casella di controllo non influisce sui risultati. Le query che recuperano i dati per un report sono incluse nel file di definizione del report e non nei file esterni.  
  
8.  Mentre la connessione è aperta è possibile modificarne le proprietà ed esportare il file di connessione. Nel gruppo **Connessioni** della scheda **Dati** fare clic su **Proprietà**e quindi sul pulsante **Proprietà connessione** accanto al nome della connessione.  
  
9. Nella scheda **Definizione** fare clic su **Esporta file di connessione**.  
  
10. Immettere un nome per il file e quindi fare clic su **Salva**. Chiudere l'applicazione e tutti i file aperti.  
  
### <a name="to-upload-and-use-an-odc-file"></a>Per caricare e utilizzare un file odc  
  
1.  Aprire la libreria in cui si desidera caricare il file di connessione.  
  
2.  Scegliere **Carica documento** dal menu **Carica**.  
  
3.  Fare clic su **Sfoglia**.  
  
4.  Selezionare il file odc creato in precedenza. Per impostazione predefinita, il file odc si trova in Origini dati utente nella cartella Documenti.  
  
5.  Fare clic su **Apri** per selezionare il file e quindi fare clic su **OK** per salvare la selezione. Viene automaticamente aperta la pagina delle proprietà per il nuovo elemento.  
  
6.  In Tipo contenuto selezionare **Origine dati report**e quindi fare clic su **OK**.  
  
7.  Selezionare un report.  
  
8.  Fare clic sulla freccia in giù e selezionare **Gestisci origini dati**.  
  
9. Fare clic sul nome dell'origine dati.  
  
10. Se il report usa informazioni di un'origine dati personalizzata, fare clic su **Condivisa**.  
  
11. In **Collegamento origine dati**fare clic sul pulsante con i puntini di sospensione ( **...** ).  
  
12. Selezionare il file odc caricato in precedenza.  
  
13. Fare clic su **OK** per selezionare il file e quindi su **OK** per salvare le modifiche.  
  
     Se si sta provando questa procedura con il database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e i report di esempio, tenere presente che solo il report Company Sales funziona con un file odc incluso. Gli altri report di esempio contengono funzionalità e parametri di query che non supportano il provider OLE DB. È tuttavia possibile fare in modo che i report supportino il provider OLE DB modificandoli innanzitutto in Progettazione report.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  
