---
title: Tipo di connessione OLE DB (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1cb3c7e8f9be785a93b29e453b5dfc727d747569
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53369573"
---
# <a name="ole-db-connection-type-ssrs"></a>Tipo di connessione OLE DB (SSRS)
  Per includere dati da un provider di dati OLE DB, è necessario disporre di un set di dati basato su un'origine dati del report di tipo OLE DB. Questo tipo di origine dati predefinito è basato sull'estensione per l'elaborazione dati OLE DB di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 OLE DB è una tecnologia di accesso ai dati che consente ai client di connettersi a una varietà di provider di dati. Dopo avere selezionato l'origine dati di tipo OLE DB, è necessario selezionare un provider di dati specifico. Il supporto per le caratteristiche quali i parametri e le credenziali dipende dal provider di dati selezionato.  
  
 Usare le informazioni presenti in questo argomento per compilare un'origine dati. Per istruzioni dettagliate, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore Report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Stringa di connessione  
 La stringa di connessione per l'estensione per l'elaborazione dati OLE DB dipende dal provider di dati scelto. Una stringa di connessione tipica contiene coppie nome/valore supportate dal provider di dati. Nella stringa di connessione seguente, ad esempio, viene specificato il provider OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e il database AdventureWorks:  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 La stringa di connessione utilizzata dipende dall'origine dati esterna alla quale si esegue la connessione. Per impostare le proprietà della stringa di connessione specifiche per un provider di dati, nella pagina **Generale** della finestra di dialogo **Proprietà origine dati** fare clic sul pulsante **Compila** per aprire la finestra di dialogo **Proprietà connessione** . Impostare le proprietà dell'origine dati estese tramite la finestra di dialogo **Proprietà di Data Link** .  
  
 Per esempi di stringhe di connessione, vedere [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a> Credenziali  
 Le credenziali sono necessarie per eseguire query, nonché per visualizzare l'anteprima del report in locale e dal server di report.  
  
 Dopo aver pubblicato il report, potrebbe essere necessario modificare le credenziali per l'origine dati affinché quando il report viene eseguito nel server di report, le autorizzazioni per il recupero dei dati risultino valide.  
  
 Per altre informazioni, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) oppure [specificare le credenziali in Generatore Report](../specify-credentials-in-report-builder.md).  
  
###### <a name="special-characters-in-a-password"></a>Caratteri speciali in una password  
 Se si configura l'origine dati OLE DB per la richiesta di una password o l'inclusione della password nella stringa di connessione e un utente immette la password con caratteri speciali, ad esempio segni di punteggiatura, è possibile che alcuni driver dell'origine dati sottostante non supportino la convalida dei caratteri speciali. In tal caso, quando si elabora il report verrà visualizzato un messaggio che indica che la password non è valida.  
  
> [!NOTE]  
>  È consigliabile non aggiungere le informazioni di accesso, ad esempio la password, alla stringa di connessione. In Generatore report è presente una scheda separata nella finestra di dialogo **Origine dati** che può essere utilizzata per immettere le credenziali.  
  
  
  
##  <a name="Parameters"></a> Parametri  
 Alcuni provider OLE DB supportano parametri senza nome e non i parametri denominati. I parametri sono passati dalla posizione tramite un segnaposto nella query. Il carattere del segnaposto è determinato dalla sintassi supportata dal provider di dati.  
  
 
  
##  <a name="Remarks"></a> Osservazioni  
 OLE DB è una tecnologia nativa per la compilazione di provider di dati per le origini dati specifiche. OLE DB si basa su interfacce COM (Component Object Model). OLE DB è una tecnologia più recente rispetto a ODBC e precedente ai provider di dati ADO.NET. I provider di dati OLE DB sono registrati con il sistema operativo come qualsiasi altro componente COM. I provider di dati OLE DB sono disponibili da Microsoft e fornitori di terze parti. Microsoft fornisce anche MSDASQL, un provider di dati OLE DB che funge da ponte per la comunicazione ai driver ODBC. Per altre informazioni, vedere [Tipo di connessione ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md).  
  
 Per recuperare correttamente i dati desiderati, è necessario fornire la sintassi della query supportata dal provider di dati. Il supporto dei parametri varia in base al provider di dati. Per ulteriori informazioni, vedere gli argomenti specifici del provider di dati selezionato. Ad esempio:  
  
-   [Provider OLE DB per Analysis Services &#40;Analysis Services - Dati multidimensionali&#41;](../../analysis-services/dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md)  
  
-   [Utilizzo del provider di dati .NET Framework per Oracle](https://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 Per altre informazioni sui provider dati OLE DB specifici, vedere [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
  
##  <a name="HowTo"></a> Procedure  
 In questa sezione sono contenute istruzioni dettagliate per l'utilizzo di connessioni dati, origini dati e set di dati.  
  
 [Aggiungere e verificare una connessione dati o un'origine dati &#40;Report e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Aggiungere un filtro a un set di dati &#40;Generatore report e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a> Sezioni correlate  
 In queste sezioni della documentazione sono incluse informazioni concettuali approfondite sui dati dei report, nonché le informazioni necessarie sulle procedure per definire, personalizzare e usare parti di un report correlate ai dati.  
  
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](report-datasets-ssrs.md)  
 Viene fornita una panoramica sull'accesso ai dati del report.  
  
 [Connessioni dati, origini dati e stringhe di connessione in Generatore report](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Vengono fornite informazioni sulle connessioni dati e sulle origini dati.  
  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sui set di dati incorporati e condivisi.  
  
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Vengono fornite informazioni sulla raccolta di campi di set di dati generata dalla query.  
  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) nella documentazione relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclusa nella [documentazione online](https://go.microsoft.com/fwlink/?linkid=121312) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Vengono fornite informazioni dettagliate sul supporto delle piattaforme e delle versioni per ogni estensione per i dati.  
  
 
  
## <a name="see-also"></a>Vedere anche  
 [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
