---
title: Risolvere i problemi di recupero dei dati con i report di Reporting Services | Microsoft Docs
ms.date: 02/27/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 7680946a-1660-4b59-a03a-c4d474cd8ed3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 86f1b8bda63cf8e6436e0dd3d5823fdada53a9f3
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65574430"
---
# <a name="troubleshoot-data-retrieval-issues-with-reporting-services-reports"></a>Risolvere i problemi di recupero dei dati con i report di Reporting Services
Il primo passaggio dell'elaborazione del report consiste nel recuperare i dati del report per ogni set di dati tramite la query del set di dati. Quando si visualizza in anteprima un report in locale, è necessario che le connessioni all'origine dati e le credenziali dispongano delle autorizzazioni sufficienti per recuperare i dati nel computer. Quando si esegue un report nel server di report, è necessario che le connessioni all'origine dati e le credenziali dispongano delle autorizzazioni sufficienti per recuperare i dati nel server di report. Utilizzare questo argomento per risolvere i problemi relativi al recupero dei dati del report.   
  
## <a name="i-cannot-create-a-connection-to-a-data-source"></a>Non è possibile creare una connessione a un'origine dati  
Quando si crea un'origine dati, si esegue una query del set di dati o si visualizza in anteprima un report, è possibile che venga visualizzato il messaggio seguente: Impossibile creare una connessione all'origine dati `<data source name>`.   
    
### <a name="data-source-is-not-available"></a>L'origine dati non è disponibile.  
L'origine dati è offline o non è disponibile per altri motivi.   
  
Verificare di poter accedere all'origine dati e che questa sia disponibile. Ad esempio, utilizzare SQL Server Management Studio per connettersi all'origine dati. Per i database relazionali e multidimensionali, usare il pulsante **Test** nella finestra di dialogo **Proprietà connessione** per verificare la connessione e le autorizzazioni per l'origine dati.   
  
### <a name="data-source-credentials-are-not-valid"></a>Le credenziali dell'origine dati non sono valide.  
Le autorizzazioni delle credenziali che si utilizzano per connettersi all'origine dati non sono sufficienti per recuperare i dati specificati nella query.  
  
Verificare che le credenziali utilizzate siano corrette. Ad esempio, è possibile disporre delle autorizzazioni per recuperare i dati da una tabella o una vista, ma non da una colonna specifica oppure potrebbero non essere disponibili autorizzazioni sufficienti per eseguire una stored procedure che popola una vista.   
  
> [!NOTE]  
> Le autorizzazioni che si utilizzano per recuperare i dati per la visualizzazione in anteprima di un report potrebbero essere diverse dalle autorizzazioni necessarie per recuperare i dati dopo che un report viene pubblicato in un server di report.   
  
### <a name="not-a-valid-password"></a>La password non è valida  
Per le origini dati con le credenziali richieste oppure specificate nella stringa di connessione, i caratteri della password vengono passati ai driver dell'origine dati sottostante. Se la password o la stringa contiene caratteri speciali, ad esempio i segni di punteggiatura, tali caratteri non vengono convalidati dai driver dell'origine dati.   
  
Verificare che la password non includa caratteri speciali. Se la modifica della password costituisce un'operazione complessa, rivolgersi all'amministratore del database per fare in modo che le credenziali appropriate vengano archiviate in locale e sul server come parte del nome di un'origine dei dati (DSN) ODBC del sistema. Per altre informazioni, vedere "OdbcConnection.ConnectionString" nella documentazione di .NET Framework SDK in MSDN.   
  
> [!NOTE]  
>È consigliabile non aggiungere le informazioni di accesso, ad esempio la password, alla stringa di connessione. Progettazione report include una pagina **Credenziali** nella finestra di dialogo **Proprietà origine dati** o **Proprietà origine dati condivisa** che può essere usata per immettere le credenziali. Tali credenziali vengono archiviate in modo protetto nel computer utilizzato per creare il report.  
  
## <a name="why-do-i-see-no-data-when-i-run-my-query-in-the-query-designer"></a>Perché non vengono visualizzati i dati quando si esegue la query nella finestra Progettazione query?  
Quando si crea un set di dati, la raccolta dei campi del set di dati viene visualizzata nel riquadro Dati report. Qualche volta la raccolta dei campi del set di dati non viene visualizzata come previsto.   
  
### <a name="import-query-does-not-import-calculated-fields"></a>L'importazione della query non include i campi calcolati  
  
Sebbene vengano salvati in una definizione del report, i campi calcolati non vengono inclusi quando si importa una query del set di dati da un altro report. Solo i campi specificati dalla query del set di dati vengono visualizzati nel riquadro Dati report dopo aver creato un set di dati importando una query da un altro report.   
  
Per visualizzare i campi calcolati nel riquadro Dati report, è necessario definirli per ogni report nel quale vengono utilizzati.   
  
### <a name="some-data-providers-do-not-support-automatic-population-of-the-dataset-field-collection"></a>Alcuni provider di dati non supportano il popolamento automatico della raccolta dei campi del set di dati  
Quando si definisce una query nella finestra di dialogo Proprietà set di dati e quindi si chiude la finestra di dialogo, la raccolta dei campi del set di dati viene di solito visualizzata nel riquadro Dati report. Per alcune origini dati, la raccolta dei campi del set di dati non viene popolata automaticamente.   
  
Per popolare la raccolta dei campi del set di dati, effettuare le operazioni seguenti:  
* Verificare di disporre delle autorizzazioni necessarie per recuperare le informazioni dei campi dal database. Per alcune origini dati, è possibile che si abbiano le autorizzazioni necessarie per accedere all'origine dati, ma non alla tabella o alla colonna. È possibile disporre delle autorizzazioni per accedere a una vista ma non per eseguire le stored procedure che creano la vista. Per convalidare l'accesso a tabelle o colonne specifiche in un database, verificare i risultati della query in un'applicazione distinta, ad esempio SQL Server Management Studio, usando le stesse autorizzazioni del report. Se non è possibile visualizzare i risultati desiderati per la query, richiedere il supporto dell'amministratore di sistema per modificare le autorizzazioni per i dati.   
* Eseguire la query nel riquadro Query della finestra di dialogo **Proprietà set di dati** . Per altre informazioni, vedere [Set di dati del report (Generatore report 3.0 e SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md).  
* Aggiungere manualmente i campi. Per altre informazioni, vedere [Procedura: Aggiungere, modificare e aggiornare i campi nel riquadro dei dati del report (Generatore report 3.0 e SSRS)](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).   
  
## <a name="see-also"></a>Vedere anche  
[Errori ed eventi (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]



