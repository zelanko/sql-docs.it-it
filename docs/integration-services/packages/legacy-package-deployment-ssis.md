---
title: Distribuzione dei pacchetti legacy (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1ce860d112f171e4cc341c2b2e2b03149720e6b9
ms.sourcegitcommit: 4b775a3ce453b757c7435cc2a4c9b35d0c5a8a9e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2020
ms.locfileid: "87472501"
---
# <a name="legacy-package-deployment-ssis"></a>distribuzione del pacchetto legacy (SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include strumenti e procedure guidate per la distribuzione di pacchetti dal computer di sviluppo al server di produzione o ad altri computer.  
  
 La procedura per la distribuzione di pacchetti prevede quattro passaggi.  
  
1.  Il primo passaggio è facoltativo e riguarda la creazione delle configurazioni dei pacchetti che aggiornano le proprietà degli elementi dei pacchetti in fase di esecuzione. Le configurazioni vengono incluse automaticamente durante la distribuzione dei pacchetti.  
  
2.  Il secondo passaggio consiste nella compilazione del progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per creare un'utilità di distribuzione di pacchetti. L'utilità di distribuzione per il progetto contiene i pacchetti che si desidera distribuire.  
  
3.  Il terzo passaggio consiste nel copiare nel computer di destinazione la cartella di distribuzione creata in fase di compilazione del progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
4.  Il quarto passaggio consiste nell'eseguire nel computer di destinazione l'Installazione guidata pacchetti per installare i pacchetti nel file system o in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="package-configurations"></a>SSIS
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre configurazioni di pacchetto che è possibile usare per aggiornare i valori delle proprietà in fase di esecuzione.  
  
> **NOTA** Le configurazioni sono disponibili per il modello di distribuzione del pacchetto. I parametri vengono utilizzati al posto delle configurazioni per il modello di distribuzione del progetto. Con il modello di distribuzione del progetto è possibile distribuire i progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni sui modelli di distribuzione, vedere [Distribuzione di progetti e pacchetti](https://msdn.microsoft.com/library/hh213290.aspx).   
  
 Una configurazione è una coppia proprietà/valore che viene aggiunta a un pacchetto completo. In genere, si crea un pacchetto, si impostano le proprietà per gli oggetti di pacchetto durante lo sviluppo del pacchetto e quindi si aggiunge la configurazione al pacchetto. Quando il pacchetto viene eseguito, ottiene i nuovi valori della proprietà dalla configurazione. Utilizzando ad esempio una configurazione, è possibile modificare la stringa di connessione di una gestione connessione o aggiornare il valore di una variabile.  
  
 Le configurazioni di pacchetto offrono i vantaggi seguenti:  
  
-   Le configurazioni semplificano lo spostamento di pacchetti dall'ambiente di sviluppo all'ambiente di produzione. Tramite una configurazione è ad esempio possibile aggiornare il percorso di un file di origine o modificare il nome di un database o di un server.  
  
-   Le configurazioni risultano utili per la distribuzione di pacchetti in più server diversi. La configurazione di ogni pacchetto distribuito può ad esempio includere una variabile che specifica un diverso valore di spazio su disco. Se lo spazio su disco disponibile non soddisfa tale valore, il pacchetto non verrà eseguito.  
  
-   Le configurazioni rendono i pacchetti più flessibili. Una configurazione, ad esempio, può aggiornare il valore di una variabile utilizzata in un'espressione di proprietà.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supporta diversi metodi di archiviazione delle configurazioni di pacchetto, ad esempio file XML, tabelle di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e variabili di ambiente e di pacchetto.  
  
 Ogni configurazione corrisponde a una coppia proprietà/valore. Il file di configurazione XML e i tipi di configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono includere più configurazioni.  
  
 Le configurazioni vengono incluse quando si crea un'utilità di distribuzione per l'installazione di pacchetti. Quando si installano i pacchetti, le configurazioni possono venire aggiornate in un passaggio dell'installazione.  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>Informazioni sull'applicazione delle configurazioni dei pacchetti in fase di esecuzione  
 Quando si usa l'utilità del prompt dei comandi **dtexec** (dtexec.exe) per eseguire un pacchetto distribuito, le configurazioni di pacchetto vengono applicate due volte, ovvero prima e dopo l'applicazione delle opzioni specificate nella riga di comando.  
  
 Durante il caricamento e l'esecuzione del pacchetto da parte dell'utilità, gli eventi si verificano nel seguente ordine:  
  
1.  Il pacchetto viene caricato con l'utilità **dtexec** .  
  
2.  L'utilità consente di applicare le configurazioni specificate nel pacchetto in fase di progettazione, nell'ordine indicato nel pacchetto. L'unica eccezione è rappresentata dalle configurazioni Variabile pacchetto padre, le quali vengono applicate dall'utilità solo una volta e in una fase successiva del processo.  
  
3.  L'utilità applica quindi le opzioni specificate nella riga di comando.  
  
4.  A questo punto l'utilità ricarica le configurazioni specificate nel pacchetto in fase di progettazione, nell'ordine indicato nel pacchetto. L'unica eccezione a questa regola è di nuovo rappresentata dalle configurazioni Variabile pacchetto padre. L'utilità utilizza quindi le opzioni della riga di comando specificate per ricaricare le configurazioni. È pertanto possibile che vengano ricaricati valori diversi da posizioni differenti.  
  
5.  L'utilità consente di applicare le configurazioni Variabile pacchetto padre.  
  
6.  L'utilità consente l'esecuzione del pacchetto.  
  
 Il modo in cui l'utilità **dtexec** applica le configurazioni influisce sulle seguenti opzioni della riga di comando:  
  
-   È possibile usare l'opzione **/Connection** o **/Set** in fase di esecuzione per caricare le configurazioni di pacchetto da una posizione diversa da quella specificata in fase di progettazione.  
  
-   È possibile usare l'opzione **/ConfigFile** per caricare configurazioni aggiuntive non specificate in fase di progettazione.  
  
 Tali opzioni della riga di comando presentano tuttavia alcune restrizioni.  
  
-   Non è possibile usare l'opzione **/Set** o **/Connection** per ignorare valori singoli impostati anche da una configurazione.  
  
-   Non è possibile usare l'opzione **/ConfigFile** per caricare configurazioni che sostituiscono quelle specificate in fase di progettazione.  
  
 Per altre informazioni su queste opzioni e sulla differenza di comportamento di tali opzioni in [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] e versioni precedenti, vedere [Differenze di funzionamento delle funzionalità di Integration Services in SQL Server 2016](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
### <a name="package-configuration-types"></a>Tipi di configurazioni di pacchetto  
 Nella tabella seguente vengono descritti i tipi di configurazione di pacchetto.  
  
|Type|Descrizione|  
|----------|-----------------|  
|File di configurazione XML|Le configurazioni sono incluse in un file XML. Il file può includere più configurazioni.|  
|Variabile di ambiente|La configurazione è contenuta in una variabile di ambiente.|  
|Voce del Registro di sistema|La configurazione è inclusa in una voce del Registro di sistema.|  
|Variabile pacchetto padre|La configurazione è contenuta in una variabile del pacchetto. Questo tipo di configurazione viene in genere utilizzato per l'aggiornamento di proprietà in pacchetti figlio.|  
|Tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|La configurazione è inclusa in una tabella di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La tabella può includere più configurazioni.|  
  
#### <a name="xml-configuration-files"></a>File di configurazione XML  
 Se si seleziona il tipo di configurazione **File di configurazione XML** è possibile creare un nuovo file di configurazione, riusare un file esistente e aggiungere nuove configurazioni oppure riusare un file esistente sovrascrivendone il contenuto.  
  
 Un file di configurazione XML è suddiviso in due sezioni:  
  
-   Un'intestazione contenente informazioni sul file. Questa sezione include attributi quali la data di creazione del file e il nome dell'utente che ha generato il file.  
  
-   Elementi di configurazione contenenti informazioni su ogni configurazione. Questa sezione include attributi quali il percorso e il valore configurato di una proprietà.  
  
 Nel codice XML seguente viene illustrata la sintassi di un file di configurazione XML. Nell'esempio viene illustrata una configurazione per la proprietà Value di una variabile di tipo Integer denominata `MyVar`.  
  
```xml
\<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
#### <a name="registry-entry"></a>Voce del Registro di sistema  
 Se si desidera utilizzare una voce del Registro di sistema per archiviare la configurazione, è possibile utilizzare una chiave esistente oppure crearne una nuova in HKEY_CURRENT_USER. Nella chiave del Registro di sistema usata deve essere disponibile un valore denominato **Value**. Il valore può essere un DWORD o una stringa.  
  
 Se si seleziona il tipo di configurazione **Voce del Registro di sistema** , è necessario digitare il nome della chiave del Registro di sistema nella casella Voce del Registro di sistema. Il formato è \<registry key>. Se si vuole usare una chiave del Registro di sistema che non si trova nella radice HKEY_CURRENT_USER, per identificare la chiave usare il formato \<Registry key\registry key\\...>. Per usare la chiave MyPackage in SSISPackages, ad esempio, digitare **SSISPackages\MyPackage**.  
  
#### <a name="sql-server"></a>SQL Server  
 Se si seleziona il tipo di configurazione **SQL Server** , è necessario specificare la connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si desidera archiviare le configurazioni. È possibile salvare le configurazioni in una tabella esistente oppure creare una nuova tabella nel database specificato.  
  
 L'istruzione SQL seguente illustra l'istruzione CREATE TABLE predefinita della Configurazione guidata pacchetto.  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 Il nome specificato per la configurazione corrisponde al valore archiviato nella colonna **ConfigurationFilter** .  
  
### <a name="direct-and-indirect-configurations"></a>Configurazioni dirette e indirette  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dispone di configurazioni dirette e indirette. Se le configurazioni vengono specificate in modo diretto, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene creato un collegamento diretto tra l'elemento di configurazione e la proprietà dell'oggetto di pacchetto. È consigliabile utilizzare le configurazioni dirette quando la posizione dell'origine non cambia. Ad esempio, se per tutte le distribuzioni di pacchetto viene utilizzato sempre lo stesso percorso di file, è possibile specificare un file di configurazione XML.  
  
 Nelle configurazioni indirette vengono utilizzate variabili di ambiente. Anziché specificare l'impostazione di configurazione in modo diretto, la configurazione punta a una variabile di ambiente, la quale contiene il valore di configurazione. È consigliabile utilizzare le configurazioni indirette quando la posizione della configurazione può essere diversa nelle varie distribuzioni di un pacchetto.  

## <a name="create-package-configurations"></a>Creazione di configurazioni dei pacchetti
  Le configurazioni di pacchetto vengono create nella finestra di dialogo **Libreria configurazioni pacchetto** e con la Configurazione guidata pacchetto. Per accedere a questi strumenti, fare clic su **Configurazioni pacchetto** nel menu **SSIS** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  
 **NOTE**
> Per accedere a **Libreria configurazioni pacchetto** è anche possibile fare clic sul pulsante con i puntini di sospensione accanto alla proprietà **Configuration** . Quest'ultima viene visualizzata nella finestra delle proprietà del pacchetto.  
> 
> Le configurazioni sono disponibili per il modello di distribuzione del pacchetto. I parametri vengono utilizzati al posto delle configurazioni per il modello di distribuzione del progetto. Con il modello di distribuzione del progetto è possibile distribuire i progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni sui modelli di distribuzione, vedere [Distribuzione di progetti e pacchetti](https://msdn.microsoft.com/library/hh213290.aspx).    
> 
> Nella finestra di dialogo **Libreria configurazioni pacchetto** è possibile abilitare l'uso delle configurazione da parte dei pacchetti, aggiungere ed eliminare configurazioni, nonché impostare l'ordine preferito di caricamento delle configurazioni. 
> 
> Il caricamento delle configurazioni di pacchetto nell'ordine preferito avviene a partire dall'inizio dell'elenco visualizzato nella finestra di dialogo **Libreria configurazioni pacchetto** fino alla fine dell'elenco. In fase di esecuzione, tuttavia, tali configurazioni potrebbero non essere caricate nell'ordine preferito. In particolare, le configurazioni di pacchetto padre vengono caricate dopo quelle di altri tipi.  
> 
> Se più configurazioni impostano la stessa proprietà dell'oggetto, in fase di esecuzione viene utilizzato l'ultimo valore caricato.  
  
 Nella finestra di dialogo **Libreria configurazioni pacchetto** è possibile avviare la Configurazione guidata pacchetto tramite cui è possibile eseguire i vari passaggi necessari per la creazione di una configurazione. Per eseguire la Configurazione guidata pacchetto, aggiungere una nuova configurazione o modificarne una esistente nella finestra di dialogo **Libreria configurazioni pacchetto** . Nei passaggi della procedura guidata viene specificato il tipo di configurazione, viene impostato l'accesso alla configurazione in modo diretto o tramite variabili di ambiente e vengono selezionate le proprietà da salvare nella configurazione.  
  
 Nell'esempio seguente vengono illustrate le proprietà di destinazione di una variabile e di un pacchetto nel modo in cui vengono indicate nella pagina Completamento procedura guidata della Configurazione guidata pacchetto:  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 In questo esempio, tramite la configurazione vengono aggiornate le proprietà seguenti:  
  
-   Proprietà RaiseChangedEvent della variabile definita dall'utente `TodaysDate`.  
  
-   Proprietà MaximumErrorCount, LoggingMode e LocaleID del pacchetto.  
  
-   Proprietà Value della variabile definita dall'utente `varTableName`nell'ambito dell'attività My SQL Task.  
  
 "\Package" rappresenta la radice, mentre gli oggetti che definiscono il percorso della proprietà aggiornata dalla configurazione sono separati da punti (.). I nomi di variabili e proprietà sono racchiusi tra parentesi quadre. Il termine Package è sempre utilizzato nella configurazione, indipendentemente dal nome del pacchetto. Per tutti gli altri oggetti inclusi nel percorso vengono tuttavia utilizzati i relativi nomi definiti dall'utente.  
  
 Al completamento della procedura guidata la nuova configurazione viene aggiunta all'elenco delle configurazioni nella finestra di dialogo **Libreria configurazioni pacchetto** .  
  
> **NOTA** Nell'ultima pagina di Configurazione guidata pacchetto, Completamento procedura guidata, sono elencate le proprietà di destinazione presenti nella configurazione. Per aggiornare le proprietà quando i pacchetti vengono eseguiti con l'utilità del prompt dei comandi **dtexec** , è possibile eseguire la Configurazione guidata pacchetto per generare le stringhe che rappresentano i percorsi delle proprietà e quindi copiarle e incollarle nella finestra del prompt dei comandi per usarle con l'opzione set di **dtexec**.  
  
 Nella tabella seguente vengono descritte le colonne dell'elenco delle configurazioni visualizzato nella finestra di dialogo **Libreria configurazioni pacchetto** .  
  
|Colonna|Descrizione|  
|------------|-----------------|  
|**Nome configurazione**|Nome della configurazione.|  
|**Tipo configurazione**|Tipo di configurazione.|  
|**Stringa di configurazione**|Posizione della configurazione. La posizione può corrispondere a un percorso, a una variabile di ambiente, a una chiave del Registro di sistema, a un nome di variabile del pacchetto padre oppure a una tabella in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Oggetto di destinazione**|Nome dell'oggetto a cui è associata una proprietà con configurazione. Se la configurazione è un file di configurazione XML, la colonna è vuota in quanto questo tipo di configurazione può aggiornare più oggetti.|  
|**Proprietà di destinazione**|Nome della proprietà. Se tramite la configurazione si scrive in un file di configurazione XML o in una tabella di SQL Server, la colonna risulta vuota perché la configurazione può aggiornare più oggetti.|  
  
### <a name="to-create-a-package-configuration"></a>Per creare una configurazione di pacchetto  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo**, **Flusso di dati**, **Gestore evento**o **Esplora pacchetti** .  
  
4.  Scegliere **Configurazioni pacchetto** dal menu **SSIS**.  
  
5.  Nella finestra di dialogo **Libreria configurazioni pacchetto** selezionare **Abilita configurazioni pacchetto**, quindi fare clic su **Aggiungi**.  
  
6.  Nella pagina iniziale della Configurazione guidata pacchetto fare clic su **Avanti**.  
  
7.  Nel passaggio Selezione tipo di configurazione specificare il tipo di configurazione e impostare quindi le proprietà rilevanti per il tipo di configurazione specificato. Per altre informazioni, vedere [Riferimento all'interfaccia utente della Configurazione guidata pacchetti](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
8.  Nel passaggio Selezione proprietà da esportare selezionare le proprietà degli oggetti di pacchetto da includere nella configurazione. Se il tipo di configurazione selezionato supporta una sola proprietà, il titolo di questo passaggio della procedura guidata sarà Selezione proprietà di destinazione. Per altre informazioni, vedere [Riferimento all'interfaccia utente della Configurazione guidata pacchetti](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
    > **NOTA** Gli unici tipi di configurazione che supportano l'inserimento di più proprietà sono **File di configurazione XML** e **SQL Server**.  
  
9. Nel passaggio Completamento procedura guidata digitare il nome della configurazione, quindi fare clic su **Fine**.  
  
10. La configurazione sarà visibile nella finestra di dialogo **Libreria configurazioni pacchetto** .  
  
11. Fare clic su **Close**.  

## <a name="package-configurations-organizer"></a>Libreria configurazioni pacchetto
  Usare la finestra di dialogo **Libreria configurazioni pacchetto** per abilitare le configurazioni dei pacchetti, visualizzarne un elenco per il pacchetto corrente e specificare l'ordine desiderato in base a cui devono essere caricate.  
  
> **NOTA** Le configurazioni sono disponibili per il modello di distribuzione del pacchetto. I parametri vengono utilizzati al posto delle configurazioni per il modello di distribuzione del progetto. Con il modello di distribuzione del progetto è possibile distribuire i progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni sui modelli di distribuzione, vedere [Distribuzione di progetti e pacchetti](https://msdn.microsoft.com/library/hh213290.aspx).    
  
 Se più configurazioni aggiornano la stessa proprietà, i valori delle configurazioni che si trovano nella parte inferiore dell'elenco sostituiscono quelli delle configurazioni nelle posizioni superiori nell'elenco. L'ultimo valore caricato nella proprietà è quello utilizzato all'esecuzione del pacchetto. Se il pacchetto utilizza una combinazione di configurazione diretta, ad esempio un file di configurazione XML, e indiretta, ad esempio una variabile di ambiente, la configurazione indiretta che punta al percorso della configurazione diretta deve trovarsi in una posizione superiore nell'elenco.  
  
> **NOTA** Il caricamento delle configurazioni di pacchetto nell'ordine preferito avviene a partire dall'inizio dell'elenco visualizzato nella finestra di dialogo **Libreria configurazioni pacchetto** fino alla fine dell'elenco. In fase di esecuzione, tuttavia, tali configurazioni potrebbero non essere caricate nell'ordine preferito. In particolare, le configurazioni di pacchetto padre vengono caricate dopo quelle di altri tipi.  
  
 Le configurazioni di pacchetto aggiornano i valori delle proprietà degli oggetti pacchetto in fase di esecuzione. Quando viene caricato un pacchetto, i valori delle configurazioni sostituiscono quelli impostati durante lo sviluppo del pacchetto. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supporta diversi tipi di configurazione. È possibile, ad esempio, utilizzare un file XML che contiene più configurazioni o una variabile di ambiente che ne contiene una sola. Per altre informazioni, vedere [Configurazioni di pacchetto](../../integration-services/packages/package-configurations.md).  
  
### <a name="options"></a>Opzioni  
 **Abilita configurazioni pacchetto**  
 Selezionare questa opzione per utilizzare le configurazioni con il pacchetto.  
  
 **Nome configurazione**  
 Consente di visualizzare il nome della configurazione.  
  
 **Tipo configurazione**  
 Consente di visualizzare il tipo di percorso in cui sono archiviate le configurazioni.  
  
 **Stringa di configurazione**  
 Consente di visualizzare il percorso in cui sono archiviati i valori della configurazione, che può essere il percorso di un file, il nome di una variabile di ambiente, il nome di una variabile del pacchetto padre, una chiave del Registro di sistema o il nome di una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Oggetto di destinazione**  
 Consente di visualizzare il nome dell'oggetto aggiornato dalla configurazione. Se la configurazione è un file di configurazione XML o una tabella di SQL Server, la colonna sarà vuota perché questo tipo di configurazione può includere più oggetti.  
  
 **Proprietà di destinazione**  
 Consente di visualizzare il nome della proprietà modificata dalla configurazione. Se il tipo di configurazione supporta più configurazioni, questa colonna sarà vuota.  
  
 **Aggiungere**  
 Consente di aggiungere una configurazione tramite la Configurazione guidata pacchetto.  
  
 **Modifica**  
 Consente di modificare una configurazione esistente rieseguendo la Configurazione guidata pacchetto.  
  
 **Rimuovi**  
 Selezionare una configurazione e quindi fare clic su **Rimuovi**.  
  
 **Frecce**  
 Selezionare una configurazione e utilizzare le frecce in su o in giù per spostarla verso l'alto o il basso nell'elenco. Le configurazioni vengono caricate nella sequenza in base a cui sono ordinate nell'elenco.  

## <a name="package-configuration-wizard-ui-reference"></a>Riferimento all'interfaccia utente della Configurazione guidata pacchetti
  Usare la **Configurazione guidata pacchetto** per creare configurazioni tramite cui è possibile aggiornare le proprietà di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i relativi oggetti in fase di esecuzione. Questa procedura guidata viene eseguita quando si aggiunge una nuova configurazione o se ne modifica una esistente nella finestra di dialogo **Libreria configurazioni pacchetto** . Per aprire la finestra di dialogo **Libreria configurazioni pacchetto** , selezionare **Configurazioni pacchetto** nel menu **SSIS** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [Creazione di configurazioni dei pacchetti](../../integration-services/packages/create-package-configurations.md).  
  
> **NOTA** Le configurazioni sono disponibili per il modello di distribuzione del pacchetto. I parametri vengono utilizzati al posto delle configurazioni per il modello di distribuzione del progetto. Con il modello di distribuzione del progetto è possibile distribuire i progetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni sui modelli di distribuzione, vedere [Distribuzione di progetti e pacchetti](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 Nelle sezioni seguenti vengono descritte le pagine della procedura guidata.  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>Pagina della Configurazione guidata pacchetto  
 Usare la **Configurazione guidata SSIS** per creare configurazioni in grado di aggiornare le proprietà di un pacchetto e i relativi oggetti in fase di esecuzione.  
  
#### <a name="options"></a>Opzioni  
 **Non visualizzare più questa pagina**  
 Consente di evitare la visualizzazione della pagina di benvenuto alla successiva apertura della procedura guidata.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
### <a name="select-configuration-type-page"></a>Pagina Selezione tipo di configurazione  
 Usare la pagina **Selezione tipo di configurazione** per specificare il tipo di configurazione da creare.  
  
 Per altre informazioni sulla selezione del tipo di configurazione da usare, vedere [Configurazioni di pacchetto](../../integration-services/packages/package-configurations.md).  
  
#### <a name="static-options"></a>Opzioni statiche  
 **Tipo configurazione**  
 Selezionare una delle opzioni seguenti per impostare il tipo di origine in cui archiviare la configurazione:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**File di configurazione XML**|Consente di archiviare la configurazione come file in formato XML. Tramite la selezione di questo valore le opzioni dinamiche vengono visualizzate nella sezione **Tipo configurazione**.|  
|**Variabile di ambiente**|Consente di archiviare la configurazione in una delle variabili di ambiente. Tramite la selezione di questo valore le opzioni dinamiche vengono visualizzate nella sezione **Tipo configurazione**.|  
|**Voce del Registro di sistema**|Consente di archiviare la configurazione nel Registro di sistema. Tramite la selezione di questo valore le opzioni dinamiche vengono visualizzate nella sezione **Tipo configurazione**.|  
|**Variabile pacchetto padre**|Consente di archiviare la configurazione come variabile nel pacchetto contenente l'attività.  Tramite la selezione di questo valore le opzioni dinamiche vengono visualizzate nella sezione **Tipo configurazione**.|  
|**SQL Server**|Consente di archiviare la configurazione in una tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tramite la selezione di questo valore le opzioni dinamiche vengono visualizzate nella sezione **Tipo configurazione**.|  
  
 **Avanti**  
 Consente di visualizzare la pagina successiva della procedura guidata.  
  
#### <a name="dynamic-options"></a>Opzioni dinamiche  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>Opzione tipo di configurazione = File di configurazione XML  
 **Usa le impostazioni di configurazione specificate di seguito**  
 Consente di specificare le impostazioni da utilizzare.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Nome file di configurazione**|Consente di digitare il percorso del file di configurazione generato dalla procedura guidata.|  
|**Sfoglia**|Usare la finestra di dialogo **Selezionare il percorso del file di configurazione** per impostare il percorso del file di configurazione generato dalla procedura guidata. Se il file non esiste, verrà creato durante la procedura guidata.|  
  
 **Percorso della configurazione memorizzato in una variabile di ambiente**  
 Consente di specificare la variabile di ambiente in cui memorizzare la configurazione.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Variabile di ambiente**|Consente di selezionare una variabile di ambiente nell'elenco.|  
  
##### <a name="configuration-type-option--environment-variable"></a>Opzione tipo di configurazione = Variabile di ambiente  
 **Variabile di ambiente**  
 Consente di selezionare la variabile di ambiente contenente le informazioni di configurazione.  
  
##### <a name="configuration-type-option--registry-entry"></a>Opzione tipo di configurazione = Voce del Registro di sistema  
 **Usa le impostazioni di configurazione specificate di seguito**  
 Consente di specificare le impostazioni da utilizzare.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Voce del Registro di sistema**|Digitare la chiave del Registro di sistema contenente le informazioni di configurazione Il formato è \<registry key>.<br /><br /> È necessario che la chiave del Registro di sistema esista già in HKEY_CURRENT_USER e che il suo valore sia denominato Value. Il valore può essere un DWORD o una stringa.<br /><br /> Se si vuole usare una chiave del Registro di sistema che non si trova nella radice HKEY_CURRENT_USER, per identificare la chiave usare il formato \<Registry key\registry key\\...>.|  
  
 **Percorso della configurazione memorizzato in una variabile di ambiente**  
 Consente di specificare la variabile di ambiente in cui memorizzare la configurazione.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Variabile di ambiente**|Consente di selezionare una variabile di ambiente nell'elenco.|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>Opzione tipo di configurazione = Variabile pacchetto padre  
 **Usa le impostazioni di configurazione specificate di seguito**  
 Consente di specificare le impostazioni da utilizzare.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Variabile padre**|Consente di specificare la variabile inclusa nel pacchetto padre contenente le informazioni di configurazione.|  
  
 **Percorso della configurazione memorizzato in una variabile di ambiente**  
 Consente di specificare la variabile di ambiente in cui viene memorizzata la configurazione.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Variabile di ambiente**|Consente di selezionare una variabile di ambiente nell'elenco.|  
  
##### <a name="configuration-type-options--sql-server"></a>Opzione tipo di configurazione = SQL Server  
 **Usa le impostazioni di configurazione specificate di seguito**  
 Consente di specificare le impostazioni da utilizzare.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Connection**|Consente di selezionare una connessione nell'elenco o di creare una nuova connessione facendo clic su **Nuova** .|  
|**Tabella configurazione**|Consente di selezionare una tabella esistente o di creare una nuova tabella facendo clic su **Nuova** per scrivere un'apposita istruzione SQL.|  
|**Filtro configurazione**|Consente di selezionare un nome esistente o di digitarne uno nuovo per la configurazione.<br /><br /> È possibile memorizzare nella stessa tabella molteplici configurazioni di SQL Server, ciascuna delle quali può includere più elementi di configurazione.<br /><br /> Questo valore definito dall'utente è memorizzato nella tabella per identificare gli elementi della configurazione appartenenti a una configurazione specifica.|  
  
 **Percorso della configurazione memorizzato in una variabile di ambiente**  
 Consente di specificare la variabile di ambiente in cui è memorizzata la configurazione.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Variabile di ambiente**|Consente di selezionare una variabile di ambiente nell'elenco.|  
  
### <a name="select-objects-to-export-page"></a>Pagina Selezione oggetti da esportare  
 Usare la pagina **Selezione proprietà di destinazione o Selezione proprietà da esportare** per specificare le proprietà degli oggetti incluse nella configurazione. La possibilità di selezionare più impostazioni è disponibile solo se si seleziona il tipo di configurazione XML.  
  
#### <a name="options"></a>Opzioni  
 **Oggetti**  
 Consente di espandere la gerarchia del pacchetto e di selezionare le proprietà da esportare.  
  
 **Attributi proprietà**  
 Consente di visualizzare gli attributi di una proprietà.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
### <a name="completing-the-wizard-page"></a>Pagina Completamento procedura guidata  
 La pagina **Completamento procedura guidata** consente di assegnare un nome per le impostazioni di configurazione e visualizzazione usate dalla procedura guidata per creare la configurazione. Dopo il completamento della procedura guidata, verrà visualizzato **Libreria configurazioni pacchetto** in cui sono elencate tutte le configurazioni per il pacchetto.  
  
#### <a name="options"></a>Opzioni  
 **Nome configurazione**  
 Consente di digitare il nome della configurazione.  
  
 **Anteprima**  
 Consente di visualizzare le impostazioni utilizzate dalla procedura guidata per creare la configurazione.  
  
 **Fine**  
 Consente di creare la configurazione e uscire dalla **Configurazione guidata pacchetto**.  

## <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a><a name="child"></a> Usare i valori di variabili e parametri in un pacchetto figlio
  In questa procedura viene descritto come creare una configurazione di pacchetto in cui viene utilizzato il tipo di configurazione variabile padre. Questo tipo di configurazione consente a un pacchetto figlio eseguito da un pacchetto padre di accedere a una variabile del pacchetto padre.  
  
> [!NOTE]  
>  È inoltre possibile passare valori a un pacchetto figlio configurando l'attività Esegui pacchetto per eseguire il mapping delle variabili o dei parametri del pacchetto padre o dei parametri del progetto ai parametri del pacchetto figlio. Per altre informazioni, vedere [Attività Esegui pacchetto](../../integration-services/control-flow/execute-package-task.md).  
  
 Non è necessario creare la variabile nel pacchetto padre prima di creare la configurazione di pacchetto nel pacchetto figlio. La variabile può essere aggiunta al pacchetto padre in qualsiasi momento, ma nella configurazione di pacchetto è necessario utilizzare il nome esatto della variabile padre. Affinché sia possibile creare una configurazione che utilizza la variabile padre, tuttavia, nel pacchetto figlio deve essere presente una variabile che possa essere aggiornata dalla configurazione. Per altre informazioni sull'aggiunta e la configurazione di variabili, vedere [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
 Come ambito per la variabile del pacchetto padre utilizzata nella configurazione di tipo Variabile pacchetto padre è possibile impostare l'attività Esegui pacchetto, il contenitore che include l'attività o il pacchetto. Se in uno stesso pacchetto sono definite più variabili con lo stesso nome, verrà utilizzata quella con ambito più vicino all'attività Esegui pacchetto. L'ambito più vicino all'attività Esegui pacchetto è l'attività stessa.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>Per aggiungere una variabile a un pacchetto padre  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente il pacchetto a cui si desidera aggiungere una variabile da passare a un pacchetto figlio.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] eseguire una delle operazioni seguenti per definire l'ambito della variabile:  
  
    -   Per impostare il pacchetto come ambito, fare clic in un punto qualsiasi dell'area di progettazione della scheda **Flusso di controllo** .  
  
    -   Per impostare come ambito un contenitore padre dell'attività Esegui pacchetto, fare clic sul contenitore.  
  
    -   Per impostare l'ambito sull'attività Esegui pacchetto, fare clic sull'attività.  
  
4.  Aggiungere e configurare una variabile.  
  
    > [!NOTE]  
    >  Selezionare un tipo di dati compatibile con i dati che verranno memorizzati nella variabile.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-add-a-variable-to-a-child-package"></a>Per aggiungere una variabile a un pacchetto figlio  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente il pacchetto a cui si vuole aggiungere una configurazione di variabile padre.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , per impostare il pacchetto come ambito, fare clic in un punto qualsiasi dell'area di progettazione della scheda **Flusso di controllo** .  
  
4.  Aggiungere e configurare una variabile.  
  
    > [!NOTE]  
    >  Selezionare un tipo di dati compatibile con i dati che verranno memorizzati nella variabile.  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  

## <a name="create-a-deployment-utility"></a>Creazione di un'utilità di distribuzione
  Il primo passaggio della distribuzione di pacchetti consiste nel creare un'utilità di distribuzione per un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . L'utilità di distribuzione è una cartella contenente i file necessari per la distribuzione dei pacchetti di un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un altro server. L'utilità di distribuzione viene creata nel computer in cui è archiviato il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Per creare l'utilità di distribuzione di pacchetti per un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è innanzitutto necessario configurare il processo di compilazione dell'utilità e quindi compilare il progetto. Quando si compila il progetto, tutti i pacchetti e le configurazioni di pacchetto del progetto vengono inclusi automaticamente. Per distribuire file aggiuntivi, ad esempio un file Leggimi per il progetto, è necessario inserirli nella cartella **Varie** del progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando si compila il progetto, vengono inclusi automaticamente anche questi file.  
  
 È possibile configurare ogni utilità di distribuzione di progetto in modo diverso. Prima di compilare il progetto e creare l'utilità di distribuzione dei pacchetti, è possibile impostare le proprietà dell'utilità in modo da personalizzare la modalità di distribuzione dei pacchetti. È possibile, ad esempio, specificare se le configurazioni di pacchetto possono essere aggiornate in fase di distribuzione del progetto. Per accedere alle proprietà di un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Proprietà**.  
  
 Nella tabella seguente vengono descritte le proprietà dell'utilità di distribuzione.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|AllowConfigurationChange|Valore che specifica se le configurazioni possono essere aggiornate durante la distribuzione.|  
|CreateDeploymentUtility|Valore che specifica se in fase di compilazione del progetto viene creata un'utilità di distribuzione di pacchetti. Per creare un'utilità di distribuzione, la proprietà deve essere impostata su **True** .|  
|DeploymentOutputPath|Posizione relativa al progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dell'utilità di distribuzione.|  
  
 Quando si compila un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], viene creato un file manifesto, \<project name>.SSISDeploymentManifest.xml, il quale viene aggiunto insieme a copie dei pacchetti di progetto e delle dipendenze di pacchetto nella cartella bin\Deployment del progetto o nel percorso specificato nella proprietà DeploymentOutputPath. Nel file manifesto sono elencati i pacchetti, le configurazioni di pacchetto ed eventuali altri file del progetto.  
  
 Il contenuto della cartella di distribuzione viene aggiornato ogni volta che si compila il progetto. Tutti i file eventualmente salvati in tale cartella e che non vengono nuovamente copiati nella cartella dal processo di compilazione verranno pertanto eliminati. Ad esempio, i file di configurazione del pacchetto salvati nelle cartelle di distribuzione verranno eliminati.  
  
### <a name="to-create-a-package-deployment-utility"></a>Per creare un'utilità di distribuzione di pacchetti  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire la soluzione contenente il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per il quale si desidera creare un'utilità di distribuzione di pacchetti.  
  
2.  Fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Pagine delle proprietà di \<project name>** fare clic su **Utilità di distribuzione**.  
  
4.  Per aggiornare le configurazioni di pacchetto in fase di distribuzione del pacchetto, impostare **AllowConfigurationChanges** su **True**.  
  
5.  Impostare **CreateDeploymentUtility** su **True**.  
  
6.  Facoltativamente, aggiornare la posizione dell'utilità di distribuzione modificando la proprietà **DeploymentOutputPath** .  
  
7.  Fare clic su **OK**.  
  
8.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e quindi scegliere **Compila**.  
  
9. Nella finestra **Output** vengono visualizzati lo stato del processo di compilazione e gli eventuali errori di compilazione.  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>Distribuzione di pacchetti con l'utilità di distribuzione
  Se è stata compilata un'utilità di distribuzione per l'installazione di pacchetti di un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un computer diverso da quello in cui l'utilità è stata compilata, è prima necessario copiare la cartella di distribuzione nel computer di destinazione.  
  
 Il percorso di tale cartella è specificato nella proprietà DeploymentOutputPath del progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per il quale è stata creata l'utilità di distribuzione. Il percorso predefinito è bin\Deployment relativo al progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni, vedere [Creazione di un'utilità di distribuzione](../../integration-services/packages/create-a-deployment-utility.md).  
  
 Per installare i pacchetti è possibile utilizzare Installazione guidata pacchetti, che può essere avviata facendo doppio clic sul file dell'utilità di distribuzione, dopo aver copiato la cartella di distribuzione sul server. Il file è denominato \<project name>.SSISDeploymentManifest ed è disponibile nella cartella di distribuzione nel computer di destinazione.  
  
> [!NOTE]  
>  In base alla versione del pacchetto che si distribuisce, è possibile rilevare un errore se versioni diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono state installate in modalità side-by-side. Questo errore può verificarsi perché l'estensione del file SSISDeploymentManifest è uguale per tutte le versioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se si fa doppio clic sul file viene chiamato il programma di installazione (dtsinstall.exe) della versione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]installata più di recente, che potrebbe non corrispondere a quella del file dell'utilità di distribuzione. Per evitare tale problema, eseguire la versione corretta di dtsinstall.exe dalla riga di comando e specificare il percorso del file dell'utilità di distribuzione.  
  
 L'Installazione guidata pacchetti consente di eseguire in modo semplificato i passaggi necessari per l'installazione di pacchetti nel file system o in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile configurare l'installazione nei modi seguenti:  
  
-   Specificando il tipo di posizione e la posizione per l'installazione dei pacchetti.  
  
-   Specificando la posizione per l'installazione delle dipendenze dei pacchetti.  
  
-   Convalidando i pacchetti dopo l'installazione nel server di destinazione.  
  
 Le dipendenze basate su file per i pacchetti vengono sempre installate nel file system. Se si installa un pacchetto nel file system, le dipendenze vengono installate nella stessa cartella specificata per il pacchetto. Se si installa un pacchetto in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile specificare la cartella in cui archiviare le dipendenze basate su file.  
  
 Se il pacchetto include configurazioni che si desidera modificare per l'utilizzo nel computer di destinazione, è possibile aggiornare i valori delle proprietà tramite la procedura guidata.  
  
 Oltre a installare pacchetti eseguendo l'Installazione guidata pacchetti, è possibile copiare e spostare pacchetti tramite l'utilità del prompt dei comandi **dtutil** . Per altre informazioni, vedere [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>Per distribuire pacchetti in un'istanza di SQL Server  
  
1.  Aprire la cartella di distribuzione del computer di destinazione.  
  
2.  Fare doppio clic sul file di manifesto \<project name>.SSISDeploymentManifest per avviare l'Installazione guidata pacchetti.  
  
3.  Nella pagina **Distribuzione pacchetti SSIS** selezionare l'opzione **Distribuzione di SQL Server** .  
  
4.  Facoltativamente, selezionare **Convalida pacchetti dopo l'installazione** per convalidare i pacchetti dopo che sono stati installati nel server di destinazione.  
  
5.  Nella pagina **Impostazione istanza di SQL Server di destinazione** specificare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui installare i pacchetti e selezionare una modalità di autenticazione. Se si seleziona l'Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
6.  Nella pagina **Selezione cartella di installazione** specificare la cartella del file system in cui installare i pacchetti e le relative dipendenze.  
  
7.  Se il pacchetto include configurazioni, è possibile modificarle aggiornando i valori dell'elenco **Valore** nella pagina Configurazione pacchetti.  
  
8.  Se è stata impostata la convalida dei pacchetti dopo l'installazione, esaminare i risultati della convalida dei pacchetti distribuiti.  

## <a name="redeployment-of-packages"></a>Ridistribuzione di pacchetti
  Dopo la distribuzione di un progetto, potrebbe essere necessario aggiornare o estendere la funzionalità dei pacchetti e ridistribuire quindi il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] contenente i pacchetti aggiornati. Durante il processo di ridistribuzione di pacchetti, è consigliabile analizzare le proprietà di configurazione incluse nell'utilità di distribuzione. Potrebbe ad esempio essere utile non consentire alcuna modifica di configurazione dopo la ridistribuzione del pacchetto.  
  
### <a name="process-for-redeployment"></a>Ridistribuzione  
 Dopo avere completato l'aggiornamento di pacchetti, è necessario ricompilare il progetto, copiare la cartella di distribuzione nel computer di destinazione e rieseguire l'Installazione guidata pacchetti.  
  
 Se si aggiornano solo alcuni pacchetti di un progetto, potrebbe risultare utile ridistribuire solo i pacchetti aggiornati anziché l'intero progetto. Per distribuire solo alcuni pacchetti, è possibile creare un nuovo progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , aggiungervi i pacchetti aggiornati e quindi compilare e distribuire il progetto. Quando il pacchetto viene aggiunto a un altro progetto, le configurazioni di pacchetto vengono copiate automaticamente insieme al pacchetto.  

## <a name="package-installation-wizard-ui-reference"></a>Riferimento all'interfaccia utente dell'Installazione guidata pacchetti
  Usare l' **Installazione guidata pacchetti** per distribuire un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , inclusi i pacchetti, i file contenuti ed eventuali dipendenze dei pacchetti.  
  
 Prima di distribuire i pacchetti, è possibile creare configurazioni e distribuirle con i pacchetti. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa le configurazioni per aggiornare in modo dinamico le proprietà di pacchetti e oggetti relativi in fase di esecuzione. La stringa di connessione di una connessione OLE DB può essere ad esempio impostata dinamicamente in fase di esecuzione, specificando una configurazione che esegue il mapping di un valore alla proprietà contenente la stringa di connessione.  
  
 Non è possibile eseguire l'Installazione guidata pacchetti finché non si compila un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e non si crea un'utilità di distribuzione. Per altre informazioni, vedere [Distribuzione di pacchetti con l'utilità di distribuzione](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 Nelle sezioni seguenti vengono descritte le pagine della procedura guidata.  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>Pagina dell'Installazione guidata pacchetti  
 L' **Installazione guidata pacchetti** consente di distribuire un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per cui è stata compilata un'utilità di distribuzione dei pacchetti.  
  
 **Non visualizzare più questa pagina iniziale**  
 Selezionare questa opzione per ignorare la pagina iniziale quando si esegue nuovamente la procedura guidata.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
 **Fine**  
 Consente di passare alla pagina Completamento Installazione guidata pacchetti. Utilizzare questa opzione se sono state controllate le scelte effettuate nelle pagine precedenti della procedura guidata e si è certi di avere specificato tutte le opzioni necessarie.  
  
### <a name="configure-packages-page"></a>Pagina Configurazione pacchetti  
 La pagina **Configurazione pacchetti** consente di modificare le configurazioni dei pacchetti.  
  
#### <a name="options"></a>Opzioni  
 **File di configurazione**  
 Consente di modificare il contenuto di un file di configurazione selezionando il file dall'elenco.  
  
 **Argomenti correlati:** [Creazione di configurazioni dei pacchetti](../../integration-services/packages/create-package-configurations.md)  
  
 **Percorso**  
 Indica il percorso della proprietà da configurare.  
  
 **Tipo**  
 Indica il tipo di dati della proprietà.  
  
 **Valore**  
 Consente di specificare il valore della configurazione.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
 **Fine**  
 Consente di passare alla pagina Completamento Installazione guidata pacchetti. Utilizzare questa opzione se sono state controllate le scelte effettuate nelle pagine precedenti della procedura guidata e si è certi di avere specificato tutte le opzioni necessarie.  
  
### <a name="confirm-installation-page"></a>Pagina Conferma installazione  
 La pagina **Conferma installazione** consente di avviare l'installazione dei pacchetti, visualizzare lo stato e visualizzare informazioni che verranno usate dalla procedura guidata per l'installazione dei file dal progetto specificato.  
  
 **Avanti**  
 Consente di installare i pacchetti e le relative dipendenze, quindi di passare alla pagina successiva della procedura al termine dell'installazione.  
  
 **Status**  
 Mostra lo stato dell'installazione del pacchetto.  
  
 **Fine**  
 Consente di passare alla pagina Completamento Installazione guidata pacchetti. Utilizzare questa opzione se sono state controllate le scelte effettuate nelle pagine precedenti della procedura guidata e si è certi di avere specificato tutte le opzioni necessarie.  
  
### <a name="deploy-ssis-packages-page"></a>Pagina Distribuzione pacchetti SSIS  
 Usare la pagina **Distribuzione pacchetti SSIS** per specificare il percorso d'installazione dei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e delle relative dipendenze.  
  
#### <a name="options"></a>Opzioni  
 **Distribuzione nel file system**  
 Consente di distribuire i pacchetti e le dipendenze in una cartella specificata del file system.  
  
 **Distribuzione in SQL Server**  
 Consente di distribuire i pacchetti e le dipendenze in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usare questa opzione se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] condivide i pacchetti tra i server. Le eventuali dipendenze dei pacchetti vengono installate nella cartella specificata del file system.  
  
 **Convalida pacchetti dopo l'installazione**  
 Consente di specificare se convalidare i pacchetti dopo l'installazione.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
 **Fine**  
 Consente di passare alla pagina Completamento Installazione guidata pacchetti. Utilizzare questa opzione se sono state controllate le scelte effettuate nelle pagine precedenti della procedura guidata e si è certi di avere specificato tutte le opzioni necessarie.  
  
### <a name="packages-validation-page"></a>Pagina Convalida pacchetti  
 Usare la pagina **Convalida pacchetti** per visualizzare lo stato e i risultati della convalida dei pacchetti.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
### <a name="select-installation-folder-page"></a>Pagina Selezione cartella di destinazione  
 Usare la pagina **Selezione cartella di installazione** per specificare la cartella del file system in cui installare i pacchetti e le relative dipendenze.  
  
#### <a name="options"></a>Opzioni  
 **Cartella**  
 Consente di specificare il percorso e la cartella in cui copiare il pacchetto e le relative dipendenze.  
  
 **Sfoglia**  
 Consente di selezionare la cartella di destinazione utilizzando la finestra di dialogo **Sfoglia cartella** .  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
 **Fine**  
 Consente di passare alla pagina Completamento Installazione guidata pacchetti. Utilizzare questa opzione se sono state controllate le scelte effettuate nelle pagine precedenti della procedura guidata e si è certi di aver specificato tutte le opzioni necessarie.  
  
### <a name="specify-target-sql-server-page"></a>Pagina Impostazione istanza di SQL Server di destinazione  
 Usare la pagina **Impostazione istanza di SQL Server di destinazione** per specificare le opzioni per la distribuzione del pacchetto in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="options"></a>Opzioni  
 **Nome server**  
 Consente di specificare il nome del server in cui distribuire i pacchetti.  
  
 **Usa autenticazione di Windows**  
 Consente di specificare se utilizzare l'autenticazione di Windows per l'accesso al server. Per una maggiore sicurezza è consigliabile utilizzare l'autenticazione di Windows.  
  
 **Usa autenticazione di SQL Server**  
 Consente di specificare se il pacchetto deve utilizzare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'accesso al server. Se si usa l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password.  
  
 **Nome utente**  
 Consente di specificare un nome utente.  
  
 **Password**  
 Consente di specificare una password.  
  
 **Percorso pacchetto**  
 Consente di specificare il nome della cartella logica o immettere "/" per la cartella predefinita.  
  
 Per selezionare la cartella nella finestra di dialogo **Pacchetto SSIS** , fare clic su Sfoglia (...). Tuttavia, la finestra di dialogo non consente di selezionare la cartella predefinita. Se si desidera utilizzare la cartella predefinita, è necessario immettere "/" nella casella di testo.  
  
> [!NOTE]  
>  Se non si immette un percorso del pacchetto valido, viene visualizzato il messaggio di errore seguente: "Uno o più argomenti non sono validi."  
  
 **Usa l'archiviazione su server per la crittografia**  
 Selezionare questa opzione per usare le funzionalità di sicurezza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per proteggere i pacchetti.  
  
 **Avanti**  
 Consente di passare alla pagina successiva della procedura guidata.  
  
 **Fine**  
 Consente di passare alla pagina Completamento Installazione guidata pacchetti. Utilizzare questa opzione se sono state controllate le scelte effettuate nelle pagine precedenti della procedura guidata e si è certi di avere specificato tutte le opzioni necessarie.  
  
### <a name="finish-the-package-installation-page"></a>Pagina Completamento Installazione guidata pacchetti  
 Usare la pagina **Completamento Installazione guidata pacchetti** per visualizzare un riepilogo dei risultati dell'installazione dei pacchetti. In questa pagina sono specificati dettagli quali il nome del progetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] distribuito, i pacchetti installati, i file di configurazione e il percorso di installazione.  
  
 **Fine**  
 Fare clic su **Fine**per uscire dalla procedura guidata.  

