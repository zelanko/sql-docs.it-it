---
title: Impostare le opzioni di rappresentazione (SSAS-multidimensionale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.impersonationinfo.f1
helpviewer_keywords:
- Impersonation Information dialog box
ms.assetid: 8e127f72-ef23-44ad-81e6-3dd58981770e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3bd6de297f4b5b677db10861e594afc36f74bb5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072954"
---
# <a name="set-impersonation-options-ssas---multidimensional"></a>Impostare opzioni di rappresentazione (SSAS - Multidimensionale)
  Quando si crea un oggetto `data source` in un modello di Analysis Services, una delle impostazioni da configurare è l'opzione di rappresentazione. Con questa opzione è possibile determinare se in Analysis Services viene acquisita l'identità di uno specifico account utente di Windows quando si eseguono operazioni locali correlate alla connessione, ad esempio il caricamento di un provider di dati OLE DB o la risoluzione di informazioni sul profilo utente in ambienti che supportano profili mobili.  
  
 Per le connessioni in cui viene utilizzata l'autenticazione di Windows, con l'opzione di rappresentazione è possibile inoltre determinare l'identità utente con cui vengono eseguite le query nell'origine dati esterna. Ad esempio, se l'opzione di rappresentazione viene impostata su **contoso\dbuser**, le query usate per recuperare i dati durante l'elaborazione saranno eseguite come **contoso\dbuser** nel server di database.  
  
 Questo argomento illustra come impostare le opzioni di rappresentazione nella finestra di dialogo **Impostazioni di rappresentazione** quando si configura un oggetto origine dati.  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>Impostare le opzioni di rappresentazione in SQL Server Data Tools  
  
1.  Fare doppio clic su un'origine dati in Esplora soluzioni per aprire Progettazione origine dati.  
  
2.  Fare clic sulla scheda **Impostazioni di rappresentazione** in Progettazione origine dati.  
  
3.  Scegliere un'opzione descritta nella sezione [Opzioni di rappresentazione](#bkmk_options) di questo argomento.  
  
## <a name="set-impersonation-options-in-management-studio"></a>Impostare le opzioni di rappresentazione in Management Studio  
 In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]aprire la finestra di dialogo **Impostazioni di rappresentazione** facendo clic sul pulsante con i puntini di sospensione (**...**) per le proprietà seguenti di queste finestre di dialogo:  
  
-   Finestra di dialogo**Proprietà database** , attraverso la proprietà Impostazioni di rappresentazione origine dati.  
  
-   Finestra di dialogo**Proprietà origine dati** , attraverso la proprietà Impostazioni di rappresentazione.  
  
-   Finestra di dialogo**Proprietà assembly** , attraverso la proprietà Impostazioni di rappresentazione.  
  
##  <a name="impersonation-options"></a><a name="bkmk_options"></a> Opzioni di rappresentazione  
 Nella finestra di dialogo sono disponibili tutte le opzioni, ma solo alcune sono appropriate per ogni scenario. Utilizzare le informazioni seguenti per determinare l'opzione più adatta per il proprio scenario.  
  
 **Usa nome utente e password specifici**  
 Selezionare questa opzione per fare in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modo che l'oggetto usi le credenziali di sicurezza di un account utente di Windows specificato nel formato seguente: * \<nome dominio>***\\*** \<nome account utente>*.  
  
 Scegliere questa opzione per utilizzare un'identità utente di Windows dedicata e con privilegi minimi, creata specificamente a scopo di accesso ai dati. Se, ad esempio, si crea regolarmente un account di uso generale per il recupero dei dati utilizzati nei report, è possibile specificarlo qui.  
  
 Per i database multidimensionali, le credenziali specificate verranno utilizzate per l'elaborazione, le query ROLAP, le associazioni out-of-line, i cubi locali, i modelli di data mining, le partizioni remote, gli oggetti collegati e la sincronizzazione tra un'origine e una destinazione.  
  
 Per i database tabulari, le credenziali specificate verranno utilizzate per l'elaborazione, le query eseguite su un archivio dati relazionale (tramite DirectQuery), le associazioni out-of-line, le partizioni remote e la sincronizzazione tra un'origine e una destinazione.  
  
 Per le istruzioni DMX OPENQUERY questa opzione viene ignorata e anziché le credenziali dell'account utente specificato verranno usate quelle dell'utente corrente.  
  
 **Usa account del servizio**  
 Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzi le credenziali di sicurezza associate al servizio di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che gestisce l'oggetto. Questa è l'opzione predefinita. Nelle versioni precedenti questa è la sola opzione che è possibile utilizzare. Questa opzione può essere preferibile per monitorare l'accesso ai dati a livello di servizio, anziché di singoli account utente.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a seconda del sistema operativo in uso, l'account del servizio potrebbe essere NetworkService o un account virtuale predefinito creato per un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specifica. Se si sceglie l'account del servizio per una connessione in cui viene utilizzata l'autenticazione di Windows, è necessario ricordarsi di creare un account di accesso al database per questo account e di concedere autorizzazioni di lettura, poiché verrà utilizzato per recuperare i dati durante l'elaborazione. Per altre informazioni sull'account del servizio, vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!NOTE]  
>  Quando si usa l'autenticazione del database, è consigliabile scegliere l'opzione di rappresentazione **Usa account del servizio** se il servizio è in esecuzione nell'account virtuale dedicato per Analysis Services. A questo account saranno concesse le autorizzazioni per accedere ai file locali. Se il servizio viene eseguito come NetworkService, un'alternativa migliore consiste nell'usare un account utente di Windows con privilegi minimi a cui siano concesse le autorizzazioni **Consenti accesso locale** . A seconda dell'account fornito, potrebbe anche essere necessario concedere le autorizzazioni di accesso ai file nella cartella dei programmi di Analysis Services.  
  
 Per i database multidimensionali, le credenziali dell'account del servizio verranno utilizzate per l'elaborazione, le query ROLAP, le partizioni remote, gli oggetti collegati e la sincronizzazione tra un'origine e una destinazione.  
  
 Per i database tabulari, le credenziali specificate verranno utilizzate per l'elaborazione, le query eseguite su un archivio dati relazionale (tramite DirectQuery), le partizioni remote e la sincronizzazione tra un'origine e una destinazione.  
  
 Per le istruzioni DMX OPENQUERY, i cubi locali e i modelli di data mining, verranno utilizzate invece le credenziali dell'utente corrente, anche se si sceglie l'opzione relativa all'account del servizio. Questa opzione non è supportata per le associazioni out-of-line.  
  
> [!NOTE]  
>  Si possono verificare degli errori durante l'elaborazione di un modello di data mining da un cubo se all'account del servizio non sono associate autorizzazioni di amministratore nell'istanza di Analysis Services. Per altre informazioni, vedere [Mining Structure: Issue while Processing when DataSource is OLAP Cube (Problemi di elaborazione nella struttura di data mining quando DataSource è un cubo OLAP)](https://go.microsoft.com/fwlink/?LinkId=251610).  
  
 **Usa credenziali dell'utente corrente**  
 Selezionare questa opzione per fare in modo che l'oggetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizzi le credenziali di sicurezza dell'utente corrente per le associazioni out-of-line, le istruzioni DMX OPENQUERY, i cubi locali e i modelli di data mining.  
  
 Questa opzione non è supportata per i database tabulari.  
  
 Fatta eccezione per i cubi locali e l'elaborazione in cui vengono utilizzate le associazioni out-of-line, questa opzione non è supportata per database multidimensionali.  
  
 **Predefinito** o **Eredita**  
 Nella finestra di dialogo si usa **Predefinito** per le opzioni di rappresentazione impostate a livello di database ed **Eredita** per le opzioni di rappresentazione impostate a livello di origine dati.  
  
 **Origini dati-opzione di ereditarietà**  
  
 A livello di origine dati, con **Eredita** è possibile specificare che in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è consigliabile usare l'opzione di rappresentazione dell'oggetto padre. In un modello multidimensionale, l'oggetto padre è il database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se si sceglie l'opzione **Eredita** , è possibile gestire a livello centrale le impostazioni di rappresentazione per questa e altre origini dati che fanno parte dello stesso database. Affinché l'opzione sia significativa, scegliere un nome utente e una password specifici di Windows a livello di database. In caso contrario, la combinazione di **Eredita** nell'origine dati e di **Predefinito** nel database equivale all'uso dell'opzione relativa all'account del servizio.  
  
 Per specificare un nome utente e una password di Windows a livello di database, effettuare le operazioni seguenti:  
  
1.  Fare clic con il pulsante destro del mouse sul database in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e selezionare **Proprietà**.  
  
2.  In **Impostazioni di rappresentazione origine dati**specificare un nome utente e una password di Windows.  
  
3.  Fare clic con il pulsante destro del mouse su ogni origine dati e visualizzare le relative proprietà per assicurarsi che per ognuna sia in uso l'opzione **Eredita** .  
  
 Per altre informazioni sulle impostazioni predefinite a livello di database, vedere [Impostare le proprietà dei database multidimensionali &#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md).  
  
 **Database-opzione predefinita**  
  
 Per i database tabulari, l' **impostazione predefinita** prevede l'utilizzo dell'account del servizio.  
  
 Per i database multidimensionali, l'opzione **Predefinito** comporta l'uso dell'account del servizio e dell'utente corrente per le operazioni di data mining.  
  
## <a name="see-also"></a>Vedi anche  
 [Creare un'origine dati &#40;SSAS multidimensionale&#41;](create-a-data-source-ssas-multidimensional.md)   
 [Impostare le proprietà dell'origine dati &#40;SSAS multidimensionale&#41;](set-data-source-properties-ssas-multidimensional.md)   
 [Scenari di distribuzione DirectQuery &#40;SSAS tabulare&#41;](../directquery-deployment-scenarios-ssas-tabular.md)  
  
  
