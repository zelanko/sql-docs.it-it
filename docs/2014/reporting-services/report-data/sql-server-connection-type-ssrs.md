---
title: Tipo di connessione SQL Server (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 957e7091-e08f-48d2-9506-872227ae8b20
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 27e4057ed11d2f7f0bab32faa3e4a19e9adb890b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106993"
---
# <a name="sql-server-connection-type-ssrs"></a>Tipo di connessione SQL Server (SSRS)
  Per includere dati da un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un report, è necessario disporre di un set di dati basato su un'origine dati del report di tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo tipo di origine dati predefinito è basato sull'estensione per i dati di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questo tipo di origine dati può essere utilizzata per stabilire la connessione e recuperare dati dalla versione corrente e da versioni precedenti di database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Questa estensione per i dati supporta parametri multivalore, aggregazioni server e credenziali gestiti separatamente dalla stringa di connessione.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore Report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Stringa di connessione  
 Quando si effettua la connessione a un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ci si connette all'oggetto di database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un server. Il database potrebbe disporre di più schemi aventi più tabelle, viste e stored procedure. L'oggetto di database viene specificato in Progettazione query. Se non si specifica un database nella stringa di connessione, la connessione viene eseguita al database predefinito assegnato dall'amministratore.  
  
 Contattare l'amministratore del database per ottenere le informazioni di connessione e le credenziali da utilizzare per connettersi all'origine dati. Nella stringa di connessione di esempio seguente viene specificato un database di esempio nel client locale:  
  
```  
Data Source=<server>;Initial Catalog=AdventureWorks  
```  
  
 Per altre informazioni ed esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Da un client di creazione di report sono disponibili le opzioni seguenti per la specifica delle credenziali:  
  
-   Utente di Windows corrente (nota anche come sicurezza integrata).  
  
-   Utilizzare un nome utente e una password archiviati.  
  
-   Richiedere all'utente le credenziali. Questa opzione supporta solo la sicurezza integrata di Windows.  
  
-   Non sono necessarie credenziali. Per utilizzare questa opzione, è necessario aver configurato l'account di esecuzione automatica sul server di report. Per altre informazioni, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) nella [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nel sito msdn.microsoft.com.  
  
 Per altre informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) oppure [specificare le credenziali in Generatore Report](../specify-credentials-in-report-builder.md).  
  
  
##  <a name="Query"></a> Query  
 Una query consente di specificare quali dati recuperare per un set di dati del report. Le colonne nel set di risultati per una query popolano la raccolta dei campi per un set di dati. In un report viene elaborato solo il primo set di risultati recuperato da una query.  
  
 Per impostazione predefinita, se si crea una nuova query o si apre una query esistente che può essere rappresentata nella finestra Progettazione query con interfaccia grafica, è disponibile la progettazione query relazionale. È possibile specificare una query nei modi seguenti:  
  
-   Compilare una query in modo interattivo. Utilizzare la finestra Progettazione query relazionale in cui è visualizzata una vista gerarchica di tabelle, viste, stored procedure e altri elementi del database organizzati in base allo schema del database. Selezionare le colonne dalle tabelle o dalle viste o specificare le stored procedure o le funzioni con valori di tabella. Limitare il numero di righe di dati da recuperare specificando i criteri di filtro. Personalizzare il filtro quando il report viene eseguito impostando l'opzione del parametro.  
  
-   Digitare o incollare una query. Usare questa finestra per immettere direttamente testo [!INCLUDE[tsql](../../includes/tsql-md.md)] , per incollare testo di query da un'altra origine, per immettere query complesse che non è possibile compilare usando la progettazione query relazionale o per immettere espressioni basate su query.  
  
-   Consente di importare una query esistente da un file o un report. Utilizzare il pulsante **Importa** da una finestra Progettazione query per individuare un file con estensione sql o rdl e importare una query.  
  
 Per altre informazioni, vedere [Interfaccia utente di Progettazione query relazionale &#40;Generatore report&#41;](relational-query-designer-user-interface-report-builder.md) e [Interfaccia utente di Progettazione query basata su testo &#40;Generatore report&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 Sono supportate le modalità query seguenti:  
  
-   [Testo](#QueryText) Digitare nei comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   [Stored procedure](#QueryStoredProcedure) Scegliere da un elenco di stored procedure.  
  
###  <a name="QueryText"></a> Utilizzo di query di tipo Text  
 Nella finestra Progettazione query basata su testo è possibile digitare i comandi [!INCLUDE[tsql](../../includes/tsql-md.md)] per definire i dati in un set di dati. La query [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente, ad esempio, seleziona i nomi di tutti i dipendenti con mansioni di assistente marketing:  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 Fare clic sul pulsante **Esegui** ( **!** ) sulla barra degli strumenti per eseguire la query e visualizzare il set di risultati.  
  
 Per parametrizzare questa query, aggiungere un parametro di query. Modificare ad esempio la clausola WHERE nella stringa seguente:  
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 Quando si esegue la query, i parametri del report corrispondenti ai parametri di query verranno creati automaticamente. Per ulteriori informazioni, vedere [Parametri di query](#Parameters) di seguito in questo argomento.  
  
  
###  <a name="QueryStoredProcedure"></a> Utilizzo di query di tipo StoredProcedure  
 È possibile specificare una stored procedure per una query del set di dati in uno dei seguenti modi:  
  
-   Nella finestra di dialogo **Proprietà set di dati** , impostare l'opzione **Stored procedure** . Scegliere dall'elenco a discesa di stored procedure e funzioni con valori di tabella.  
  
-   Nel riquadro Vista di database della finestra Progettazione query relazionale, selezionare una stored procedure o una funzione con valori di tabella.  
  
-   Nella finestra Progettazione query basata su testo, selezionare **StoredProcedure** sulla barra degli strumenti.  
  
 Dopo aver selezionato una stored procedure o una funzione con valori di tabella, è possibile eseguire la query. Verranno richiesti i valori dei parametri di input. Quando si esegue la query, i parametri del report corrispondenti ai parametri di input verranno creati automaticamente. Per ulteriori informazioni, vedere [Parametri di query](#Parameters) di seguito in questo argomento.  
  
 È supportato solo il primo set di risultati recuperato per una stored procedure. Se una stored procedure restituisce più set di risultati, viene utilizzato solo il primo.  
  
 Se in una stored procedure è presente un parametro con un valore predefinito, è possibile accedere a tale valore utilizzando la parola chiave DEFAULT come valore per il parametro. Se il parametro di query è collegato a un parametro di report, l'utente può digitare o selezionare la parola DEFAULT nella casella di input del parametro di report.  
  
 Per altre informazioni, vedere "Stored procedure (Motore di database)" nella [documentazione online di SQL Server](https://go.microsoft.com/fwlink/?linkid=98335) nel sito msdn.microsoft.com.  
  
  
##  <a name="Parameters"></a> Parametri  
 Quando il testo della query contiene variabili di query o stored procedure con parametri di input, vengono generati automaticamente i parametri di query corrispondenti per il set di dati e i parametri di report per il report. Il testo della query non deve includere l'istruzione DECLARE per ogni variabile della query.  
  
 La query SQL seguente, ad esempio, crea un parametro di report denominato `EmpID`:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 I parametri di report vengono creati con valori di proprietà predefiniti che all'occorrenza possono essere modificati. Ad esempio:  
  
-   Per impostazione predefinita, i dati di ogni parametro di report sono di tipo **Text**. Se i dati sottostanti sono di un tipo diverso, è necessario modificare il tipo di dati del parametri.  
  
-   Se si seleziona l'opzione per i parametri multivalore, è necessario modificare manualmente la query per verificare se i valori fanno parte di un set tramite l'operatore `IN`, ad esempio `WHERE EmployeeID IN (@EmpID)`.  
  
 Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Osservazioni  
 È inoltre possibile recuperare dati da un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite un tipo di origine dati OLE DB o ODBC. Per altre informazioni, vedere [Tipo di connessione OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md) o [Tipo di connessione ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md).  
  
###### <a name="platform-and-version-information"></a>Informazioni sulla piattaforma e sulla versione  
 Per altre informazioni sul supporto della piattaforma e della versione, vedere [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
##  <a name="HowTo"></a> Procedure  
 In questa sezione sono contenute istruzioni dettagliate per l'utilizzo di connessioni dati, origini dati e set di dati.  
  
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le procedure per definire, personalizzare e utilizzare parti di un report correlate ai dati.  
  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi di set di dati generata dalla query.  
  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Vengono fornite informazioni dettagliate sul supporto delle piattaforme e delle versioni per ogni estensione per i dati.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
