---
title: Impostare le proprietà dell'origine dati (SSAS multidimensionale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.datasourceproperties.f1
helpviewer_keywords:
- Data Source Properties dialog box
ms.assetid: bf8b600f-5b99-4f7d-908b-8a391721e9dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 76d25aabd5b24cdbcc72d3c356168a040a83081a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073045"
---
# <a name="set-data-source-properties-ssas-multidimensional"></a>Impostare proprietà origine dati (SSAS multidimensionale)
  In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]un'origine dati consente di specificare una connessione a un data warehouse esterno o a un database relazionale che fornisce dati a un modello multidimensionale. Le proprietà sull'origine dati determinano la stringa di connessione, un intervallo di timeout, il numero massimo di connessioni e il livello di isolamento delle transazioni.  
  
## <a name="set-data-source-properties-in-sql-server-data-tools"></a>Impostare le proprietà dell'origine dati in SQL Server Data Tools  
  
1.  Fare doppio clic su un'origine dati in Esplora soluzioni per aprire Progettazione origine dati.  
  
2.  Fare clic sulla scheda **Impostazioni di rappresentazione** in Progettazione origine dati. Per altre informazioni sulla creazione di un'origine dati, vedere [Creare un'origine dati &#40;SSAS multidimensionale&#41;](create-a-data-source-ssas-multidimensional.md).  
  
## <a name="set-data-source-properties-in-management-studio"></a>Impostare le proprietà dell'origine dati in Management Studio  
  
1.  Espandere la cartella del database, aprire la cartella **Origine dati** sotto il nome del database, fare clic con il pulsante destro del mouse su un'origine dati in **Esplora oggetti** e selezionare **Proprietà**.  
  
2.  Facoltativamente, modificare il nome, la descrizione o l'opzione di rappresentazione. Per altre informazioni, vedere [Impostare opzioni di rappresentazione &#40;SSAS - Multidimensionale&#41;](set-impersonation-options-ssas-multidimensional.md).  
  
## <a name="data-source-properties"></a>Proprietà dell'origine dati  
  
|Termine|Definizione|  
|----------|----------------|  
|**Nome, ID, Descrizione**|Nome, ID e Descrizione vengono utilizzati per identificare e descrivere l'oggetto origine dati nel modello multidimensionale.<br /><br /> Nome e Descrizione possono essere specificati in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] dopo la distribuzione o l'elaborazione della soluzione.<br /><br /> L'ID viene generato durante la creazione dell'oggetto. Sebbene sia possibile modificare in modo semplice il nome e la descrizione, gli ID sono di sola lettura e non devono essere modificati. Un ID oggetto fisso consente di mantenere le dipendenze tra gli oggetti e i riferimenti agli oggetti nel modello.|  
|**Timestamp creazione**|Questa proprietà di sola lettura viene visualizzata in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Consente di visualizzare la data e l'ora di creazione dell'origine dati.|  
|**Ultimo aggiornamento schema**|Questa proprietà di sola lettura viene visualizzata in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Consente di visualizzare la data e l'ora dell'ultimo aggiornamento dei metadati relativi all'origine dati. Questo valore viene aggiornato quando si distribuisce la soluzione.|  
|**Timeout query**|Consente di specificare per quanto tempo si tenterà di eseguire una richiesta di connessione prima che venga eliminata.<br /><br /> Digitare il timeout delle query nel formato seguente:<br /><br /> Ore>:*\<minuti>*:*\<secondi>* * \< *<br /><br /> Questa proprietà può essere sostituita dalla proprietà del server `DatabaseConnectionPoolTimeoutConnection`. Se il valore della proprietà del server è inferiore, verrà usato al posto di **Timeout query**.<br /><br /> Per altre informazioni sulla proprietà **Timeout query** , vedere <xref:Microsoft.AnalysisServices.DataSource.Timeout%2A>. Per altre informazioni sulla proprietà del server, vedere [Proprietà OLAP](../server-properties/olap-properties.md).|  
|**Stringa di connessione**|Consente di specificare la posizione fisica di un database che fornisce dati a un modello multidimensionale, nonché il provider di dati utilizzato per la connessione. Queste informazioni vengono fornite a una libreria client che effettua la richiesta di connessione. Il provider determina le proprietà del server che è possibile impostare nella stringa di connessione.<br /><br /> La stringa di connessione viene compilata con le informazioni fornite nella finestra di dialogo **Gestione connessione** . È inoltre possibile visualizzare e modificare la stringa di connessione nella pagina delle proprietà dell'origine dati in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] .<br /><br /> Per un database di SQL Server, una stringa di connessione che contiene `user ID` indica l'autenticazione del database; una stringa di connessione contenente `Integrated Security=SSPI` indica l'autenticazione di Windows.<br /><br /> Se il database è stato spostato in una nuova posizione, è possibile modificare il nome del server o del database. Verificare che per le credenziali attualmente specificate per la connessione venga eseguito il mapping a un account di accesso al database.|  
|**Numero massimo di connessioni**|Consente di specificare il numero massimo di connessioni consentito da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per la connessione all'origine dati. Se sono richieste più connessioni, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rimane in attesa finché una connessione non diventa disponibile. Il valore predefinito è 10. L'impostazione di un vincolo al numero di connessioni impedisce l'overload dell'origine dati esterna con richieste di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Isolamento**|Consente di specificare il funzionamento relativo ai blocchi e al controllo delle versioni delle righe per i comandi SQL eseguiti da una connessione a un database relazionale. I valori validi sono ReadCommitted o Snapshot. L'impostazione predefinita è ReadCommitted, che indica la necessità di eseguire il commit dei dati prima della relativa lettura, al fine di evitare letture dirty. Snapshot indica che le letture provengono da uno snapshot di dati di cui è stato eseguito in precedenza il commit. Per altre informazioni sul livello di isolamento in SQL Server, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).|  
|**Provider gestito**|Consente di visualizzare il nome del provider gestito, ad esempio System.Data.SqlClient o System.Data.OracleClient, se l'origine dati ne utilizza uno.<br /><br /> Se l'origine dati non utilizza un provider gestito, per questa proprietà verrà visualizzata una stringa vuota.<br /><br /> Questa proprietà è di sola lettura in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Per modificare il provider utilizzato per la connessione, modificare la stringa di connessione.|  
|**Impostazioni di rappresentazione**|Consente di specificare l'identità di Windows usata per l'esecuzione di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante la connessione a un'origine dati che usa l'autenticazione di Windows. Le opzioni includono l'utilizzo di un set predefinito di credenziali di Windows, l'account del servizio, l'identità dell'utente corrente o un'opzione di ereditarietà che può essere utile se il modello contiene più oggetti origine dati. Per altre informazioni, vedere [Impostare opzioni di rappresentazione &#40;SSAS - Multidimensionale&#41;](set-impersonation-options-ssas-multidimensional.md).<br /><br /> Nell'elenco di valori validi in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]sono inclusi i seguenti:<br /><br /> **ImpersonateAccount** (usare un nome utente e una password specifici di Windows per connettersi all'origine dati).<br /><br /> **ImpersonateServiceAccount** (usare l'identità di sicurezza dell'account del servizio per connettersi all'origine dati). Questo è il valore predefinito.<br /><br /> **ImpersonateCurrentUser** (usare l'identità di sicurezza dell'utente corrente per connettersi all'origine dati). Questa opzione è valida solo per query di data mining che recuperano dati da un data warehouse o database esterno; non sceglierla per connessioni dati utilizzate per l'elaborazione, il caricamento o l'esecuzione del writeback in un database multidimensionale.<br /><br /> **Eredita** o **Predefinito** (usare le impostazioni di rappresentazione del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che contiene questo oggetto origine dati). Le proprietà del database includono opzioni di rappresentazione.|  
  
## <a name="see-also"></a>Vedi anche  
 [Origini dati nei modelli multidimensionali](data-sources-in-multidimensional-models.md)   
 [Creare un'origine dati &#40;SSAS multidimensionale&#41;](create-a-data-source-ssas-multidimensional.md)  
  
  
