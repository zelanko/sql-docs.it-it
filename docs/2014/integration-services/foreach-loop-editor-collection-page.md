---
title: Editor ciclo foreach (pagina raccolta) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.collection.f1
ms.assetid: 95a19dde-61ca-4d9b-aa3d-131fa4264296
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5b9396ab5a25bba979859ac685c4759b8b01c24d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66428805"
---
# <a name="foreach-loop-editor-collection-page"></a>Editor ciclo Foreach (pagina Raccolta)
  Usare la pagina **Raccolta** della finestra di dialogo **Editor ciclo Foreach** per specificare il tipo di enumeratore e configurarlo.  
  
 Per informazioni sul contenitore Ciclo Foreach e su come configurarlo, vedere [Contenitore Ciclo Foreach](control-flow/foreach-loop-container.md) e [Configurazione di un contenitore Ciclo Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Enumeratore**  
 Consente di selezionare il tipo di enumeratore nell'elenco. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Enumeratore Foreach File**|Consente di enumerare i file. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach File Enumerator**.|  
|**Enumeratore Foreach Item**|Consente di enumerare i valori in un elemento. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach File Enumerator**.|  
|**Foreach ADO Enumerator**|Consente di enumerare tabelle o righe nelle tabelle. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach ADO Enumerator**.|  
|**Enumeratore del set di righe dello schema Foreach ADO.NET**|Consente di enumerare uno schema. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach ADO.NET Enumerator**.|  
|**Enumeratore Foreach From Variable**|Consente di enumerare il valore in una variabile. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach From Variable Enumerator**.|  
|**Enumeratore Foreach Nodelist**|Consente di enumerare i nodi in un documento XML. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach File Enumerator**.|  
|**Enumeratore Foreach SMO**|Consente di enumerare un oggetto SMO. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach SMO Enumerator**.|  
|**Enumeratore BLOB di Azure foreach**|Enumerare i file BLOB nel percorso BLOB specificato. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Foreach Azure Blob Enumerator**.|  
|**Enumeratore Foreach ADLS file**|Enumerare i file in ADLS con i filtri. La selezione di questo valore determina la visualizzazione delle opzioni dinamiche nella sezione **Enumeratore Foreach file di ADLS**.|
  
 **Espressioni**  
 Fare clic su **Espressioni** o espandere questa voce per visualizzare l'elenco delle espressioni di proprietà esistenti. Fare clic sul pulsante con i puntini di sospensione **(...)** per aggiungere un'espressione di proprietà per una proprietà dell'enumeratore oppure per modificare e valutare un'espressione di proprietà esistente.  
  
 **Argomenti correlati:**[Integration Services &#40;espressioni di&#41; SSIS](expressions/integration-services-ssis-expressions.md), [Editor espressioni di proprietà](expressions/property-expressions-editor.md), [Generatore](expressions/expression-builder.md) di espressioni    
  
## <a name="enumerator-dynamic-options"></a>Opzioni dinamiche relative all'enumeratore  
  
### <a name="enumerator--foreach-file-enumerator"></a>Enumeratore = Foreach File Enumerator  
 Foreach File Enumerator consente di enumerare i file contenuti in una cartella. Se il Ciclo Foreach include ad esempio un'attività Esegui SQL, è possibile utilizzare Foreach File Enumerator per enumerare i file che contengono le istruzioni SQL che sono eseguite dall'attività Esegui SQL. È possibile configurare l'enumeratore in modo da includere le sottocartelle.  
  
 Il contenuto delle cartelle e delle sottocartelle che sono enumerate da Foreach File Enumerator potrebbe cambiare durante l'esecuzione del ciclo, in quanto in questa fase le attività o i processi esterni nel ciclo possono aggiungere, rinominare o eliminare file. Di conseguenza potrebbe verificarsi una serie di situazioni impreviste:  
  
-   Se i file vengono eliminati, un'attività nel Ciclo Foreach potrebbe operare su un set di file diverso dai file utilizzati dalle attività successive.  
  
-   Se i file vengono rinominati e un processo esterno aggiunge automaticamente altri file per sostituire quelli rinominati, il Ciclo Foreach potrebbe operare due volte sullo stesso contenuto.  
  
-   Se i file vengono aggiunti, potrebbe essere difficile determinare per quali file ha operato il Ciclo Foreach.  
  
 **Cartella**  
 Consente di specificare il percorso della cartella radice da enumerare.  
  
 **Sfoglia**  
 Consente di individuare la cartella radice.  
  
 **File**  
 Consente di specificare i file da enumerare.  
  
> [!NOTE]  
>  Utilizzare i caratteri jolly (*) per specificare i file da includere nella raccolta. Per includere i file i cui nomi contengono "abc", ad esempio, usare il filtro seguente: \*abc\*.  
>   
>  Quando si specifica un'estensione per il nome di file, l'enumeratore restituisce anche i file che presentano la stessa estensione con altri caratteri aggiunti. Si tratta dello stesso comportamento del comando **dir** del sistema operativo, che prevede anch'esso il confronto dei nomi di file 8.3 per la compatibilità con le versioni precedenti. Questo comportamento dell'enumeratore può provocare risultati imprevisti. Se, ad esempio, si desidera enumerare solo file di Excel 2003 e si specifica "* .xls", l'enumeratore restituirà anche i file di Excel 2007 perché presentano l'estensione ".xlsx".  
>   
>  È possibile usare un'espressione per specificare i file da includere in una raccolta espandendo **Espressioni** nella pagina **Raccolta**, selezionando la proprietà **FileSpec** e quindi facendo clic sul pulsante con i puntini di sospensione (...) per aggiungere l'espressione di proprietà. Per ulteriori informazioni sulla selezione dinamica di file specificati, vedere la pagina relativa al [filtro dei file impostati dinamicamente da SSIS: filespec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html)  
  
 **Completo**  
 Selezionare questa opzione per recuperare il percorso completo dei nomi di file. Se nell'opzione File si specificano caratteri jolly, i percorsi completi restituiti corrisponderanno al filtro.  
  
 **Solo nome**  
 Selezionare questa opzione per recuperare solo i nomi di file. Se nell'opzione File si specificano caratteri jolly, i nomi di file restituiti corrisponderanno al filtro.  
  
 **Nome ed estensione**  
 Selezionare questa opzione per recuperare i nomi di file e le estensioni corrispondenti. Se nell'opzione File si specificano caratteri jolly, il nome e l'estensione dei file restituiti corrisponderanno al filtro.  
  
 **Attraversa sottocartelle**  
 Selezionare questa opzione per includere le sottocartelle nell'enumerazione.  
  
### <a name="enumerator--foreach-item-enumerator"></a>Enumeratore = Foreach Item Enumerator  
 Foreach Item Enumerator consente di enumerare gli elementi contenuti in una raccolta. È possibile definire gli elementi nella raccolta specificando le colonne e i valori delle colonne Le colonne in una riga definiscono un elemento. Avrà ad esempio due colonne un elemento che specifica gli eseguibili eseguiti da un'attività Esegui processo e la directory di lavoro utilizzata dall'attività: in una colonna saranno elencati i nomi degli eseguibili e nell'altra la directory di lavoro. Il numero di righe determina il numero di volte che il ciclo viene ripetuto. Se la tabella ha 10 righe, il ciclo si ripete 10 volte.  
  
 Per aggiornare le proprietà dell'attività Esegui processo, è possibile eseguire il mapping delle variabili alle colonne dell'elemento utilizzando l'indice della colonna. La prima colonna definita nell'elemento dell'enumeratore ha il valore indice 0, la seconda colonna 1 e così via. I valori variabili sono aggiornati ad ogni ripetizione del ciclo. Le proprietà `Executable` e `WorkingDirectory` dell'attività Esegui processo possono essere quindi aggiornate da espressioni di proprietà che utilizzano queste variabili.  
  
 **Definire gli elementi nella raccolta For Each Item**  
 Consente di specificare un valore per ogni colonna della tabella.  
  
> [!NOTE]  
>  Dopo avere immesso i valori nelle colonne della riga, alla tabella viene aggiunta automaticamente una nuova riga.  
  
> [!NOTE]  
>  Se i valori specificati non sono compatibili con il tipo di dati della colonna, il testo viene visualizzato in rosso.  
  
 **Tipo di dati della colonna**  
 Elenca il tipo di dati della colonna attiva.  
  
 **Rimuovi**  
 Selezionare un elemento e quindi fare clic su **Rimuovi** per rimuoverlo dall'elenco.  
  
 **Colonne**  
 Fare clic su questo pulsante per configurare il tipo di dati delle colonne nell'elemento.  
  
 **Argomenti correlati:** [riferimento all'interfaccia utente della finestra di dialogo colonne per ogni elemento](../../2014/integration-services/for-each-item-columns-dialog-box-ui-reference.md)  
  
### <a name="enumerator--foreach-ado-enumerator"></a>Enumeratore = Foreach ADO Enumerator  
 Foreach ADO Enumerator consente di enumerare le righe o le tabelle in un oggetto ADO o ADO.NET archiviato in una variabile. Se il Ciclo Foreach include ad esempio un'attività Script che scrive un set di dati in una variabile, è possibile utilizzare Foreach ADO Enumerator per enumerare le righe nel set di dati. Se la variabile contiene un set di dati ADO.NET, è possibile configurare l'enumeratore in modo da enumerare le righe in più tabelle o in modo da enumerare le tabelle.  
  
 **Variabile di origine oggetto ADO**  
 Selezionare una variabile definita dall'utente nell'elenco oppure fare clic su \<**Nuova variabile**> per creare una nuova variabile.  
  
> [!NOTE]  
>  Il tipo di dati della variabile deve essere Oggetto. In caso contrario si verificherà un errore.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
 **Righe nella prima tabella**  
 Selezionare questa opzione per enumerare solo le righe nella prima tabella.  
  
 **Righe in tutte le tabelle (solo set di dati ADO.NET)**  
 Selezionare questa opzione per enumerare le righe in tutte le tabelle. Questa opzione è disponibile solo se gli oggetti da enumerare sono tutti membri dello stesso set di dati ADO.NET.  
  
 **Tutte le tabelle (solo set di dati ADO.NET)**  
 Selezionare questa opzione per enumerare solo le tabelle.  
  
### <a name="enumerator--foreach-adonet-schema-rowset-enumerator"></a>Enumeratore = Foreach ADO.NET Schema Rowset Enumerator  
 Foreach ADO.NET Schema Rowset Enumerator consente di enumerare uno schema per un'origine dei dati specificata. Se il Ciclo Foreach include ad esempio un'attività Esegui SQL, è possibile utilizzare Foreach ADO.NET Schema Rowset Enumerator per enumerare gli schemi, ad esempio le colonne nel database **AdventureWorks** , e utilizzare l'attività Esegui SQL per ottenere le autorizzazioni dello schema.  
  
 **Connessione**  
 Selezionare una gestione connessione ADO.NET nell'elenco oppure fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione ADO.NET.  
  
> [!IMPORTANT]  
>  La gestione connessione ADO.NET deve utilizzare necessariamente un provider .NET per OLE DB. In caso di connessione a SQL Server, il provider consigliato è [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client, incluso nell'elenco della sezione **Provider .Net per OleDb** nella finestra di dialogo **Gestione connessione** .  
  
 **Argomenti correlati:** [gestione connessione ADO](connection-manager/ado-connection-manager.md), [configurare Gestione connessione ADO.NET](configure-ado-net-connection-manager.md)  
  
 **Schema**  
 Consente di selezionare lo schema da enumerare.  
  
 **Imposta restrizioni**  
 Consente di impostare le restrizioni da applicare allo schema specificato.  
  
 **Argomenti correlati:** finestra di [dialogo restrizioni schema](../../2014/integration-services/schema-restrictions-dialog-box.md)  
  
### <a name="enumerator--foreach-from-variable-enumerator"></a>Enumeratore = Foreach From Variable Enumerator  
 Foreach From Variable Enumerator consente di enumerare gli oggetti enumerabili nella variabile specificata. Se il Ciclo Foreach include ad esempio un'attività Esegui SQL che esegue una query e archivia il risultato in una variabile, è possibile utilizzare Foreach From Variable Enumerator per enumerare i risultati della query.  
  
 **Variabile**  
 Selezionare una variabile nell'elenco oppure fare clic su \< **nuova variabile...**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
### <a name="enumerator--foreach-nodelist-enumerator"></a>Enumeratore = Foreach NodeList Enumerator  
 Foreach Nodelist Enumerator consente di enumerare il set di nodi XML ottenuto dall'applicazione di un'espressione XPath a un file XML. Se il Ciclo Foreach include ad esempio un'attività Script, è possibile utilizzare Foreach NodeList Enumerator per passare un valore che risponda ai criteri dell'espressione XPath dal file XML all'attività Script.  
  
 L'espressione XPath che viene applicata al file XML è l'operazione XPath esterna, archiviata nella proprietà OuterXPathString. Se il tipo di enumerazione XPath è impostato `ElementCollection`su, l'enumeratore Foreach NodeList può applicare un'espressione XPath interna, archiviata nella proprietà InnerXPathString, a una raccolta di elementi.  
  
 Per ulteriori informazioni sull'utilizzo di documenti e dati XML, vedere "[Employing XML in the .NET Framework (utilizzo di XML in .NET Framework)](https://go.microsoft.com/fwlink/?LinkId=56214)" in MSDN Library.  
  
 **Proprietà DocumentSourceType**  
 Consente di selezionare il tipo di origine del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **DocumentSource**  
 Se la proprietà **DocumentSourceType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione (...) per specificarlo usando la finestra di dialogo **Editor origine documento**.  
  
 Se la proprietà **DocumentSourceType** è impostata su **Connessione file**, selezionare una gestione connessione file oppure fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se la proprietà **DocumentSourceType** è impostata su **Variabile**, selezionare una variabile esistente oppure fare clic su \<**Nuova variabile**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **EnumerationType**  
 Consente di selezionare un tipo di enumeratore nell'elenco. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Strumento di spostamento**|Consente di eseguire l'enumerazione utilizzando uno strumento di spostamento XPathNavigator.|  
|**Nodo**|Consente di enumerare i nodi restituiti da un'operazione XPath.|  
|**NodeText**|Consente di enumerare i nodi di testo restituiti da un'operazione XPath.|  
|`ElementCollection`|Consente di enumerare i nodi degli elementi restituiti da un'operazione XPath.|  
  
 **Proprietà OuterXPathStringSourceType**  
 Consente di selezionare il tipo di origine della stringa XPath. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 `OuterXPathString`  
 Se la proprietà **OuterXPathStringSourceType** è impostata su **Input diretto**, indicare la stringa XPath.  
  
 Se la proprietà **OuterXPathStringSourceType** è impostata su **Connessione file**, selezionare una gestione connessione file oppure fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se la proprietà **OuterXPathStringSourceType** è impostata su **Variabile**, selezionare una variabile esistente oppure fare clic su \<**Nuova variabile**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **InnerElementType**  
 Se **EnumerationType** è impostato su `ElementCollection`, selezionare il tipo di elemento interno nell'elenco.  
  
 **Proprietà InnerXPathStringSourceType**  
 Consente di selezionare il tipo di origine della stringa XPath interna. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 `InnerXPathString`  
 Se la proprietà **InnerXPathStringSourceType** è impostata su **Input diretto**, indicare la stringa XPath.  
  
 Se la proprietà **InnerXPathStringSourceType** è impostata su **Connessione file**, selezionare una gestione connessione file oppure fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se la proprietà **InnerXPathStringSourceType** è impostata su **Variabile**, selezionare una variabile esistente oppure fare clic su \<**Nuova variabile**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
### <a name="enumerator--foreach-smo-enumerator"></a>Enumeratore = Foreach SMO Enumerator  
 Foreach SMO Enumerator consente di enumerare gli oggetti SQL Server Management Objects (SMO). Se il Ciclo Foreach include ad esempio un'attività Esegui SQL, è possibile utilizzare Foreach SMO Enumerator per enumerare le tabelle nel database **AdventureWorks** ed eseguire query che contino il numero di righe in ogni tabella.  
  
 **Connessione**  
 Selezionare una gestione connessione ADO.NET nell'elenco oppure fare clic su \<**Nuova connessione**> per creare una nuova gestione connessione.  
  
 Argomenti correlati: [ADO.NET Connection Manager](connection-manager/ado-net-connection-manager.md), [Configure ADO.NET Connection Manager](configure-ado-net-connection-manager.md)  
  
 **Enumerare**  
 Consente di specificare l'oggetto SMO da enumerare.  
  
 **Sfoglia**  
 Consente di selezionare l'enumerazione SMO.  
  
 **Argomenti correlati:** finestra di [dialogo Seleziona enumerazione SMO](../../2014/integration-services/select-smo-enumeration-dialog-box.md)  
  
### <a name="enumerator--foreach-azure-blob-enumerator"></a>Enumerator = Foreach Azure Blob Enumerator  
 
  **Azure Blob Enumerator**consente a un pacchetto SSIS di enumerare i file BLOB nel percorso BLOB specificato. Il nome del file BLOB enumerato può essere archiviato in una variabile e usato nelle attività interne al Contenitore Ciclo Foreach.  
  
 **Gestione connessione di archiviazione di Azure**  
 Selezionare una gestione connessione di archiviazione di Azure esistente o crearne una nuova che si riferisca a un Account di archiviazione Azure.  
  
 Argomenti correlati: [Azure Storage Connection Manager](connection-manager/azure-storage-connection-manager.md).  
  
 **Nome del contenitore BLOB**  
 Specificare il nome del contenitore BLOB che contiene i file BLOB da enumerare.  
  
 **Directory BLOB**  
 Specificare la directory BLOB che contiene i file BLOB da enumerare. La directory BLOB è una struttura gerarchica virtuale.  
  
 **Filtro nome BLOB**  
 Specificare un filtro di nome per enumerare i file con un determinato modello di nome. ad esempio Foglio*.xls\* includerà file come Foglio001.xls e FoglioABC.xlsx.  
  
 **Filtro intervallo di tempo BLOB da/a**  
 Specificare un filtro di intervallo di tempo. I file modificati dopo **TimeRangeFrom** e prima di **TimeRangeTo** saranno enumerati.  
### <a name="enumerator--foreach-adls-file-enumerator"></a> Enumeratore = Enumeratore Foreach file di ADLS  
L' **enumeratore di file ADLS** consente a un pacchetto SSIS di enumerare i file in ADLS con i filtri. Il percorso completo`/`con prefisso barra () per i file enumerati può essere archiviato in una variabile e usato nelle attività all'interno del contenitore ciclo foreach.
  
**AzureDataLakeConnection**  
Specifica una gestione connessione di Azure Data Lake o crea una nuova istanza che fa riferimento a un account ADLS.   
  
**AzureDataLakeDirectory**  
Specifica la directory ADLS in cui eseguire la ricerca.
  
**FileNamePattern**  
Specifica un filtro per il nome file. Verranno enumerati solo i file il cui nome corrisponde al modello specificato. Sono supportati i caratteri jolly `*` e `?`. 
  
**SearchRecursively**  
Specifica se eseguire la ricerca in modo ricorsivo all'interno della directory specificata.  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Intervento nel blog relativo all' [enumeratore Foreach Nodelist in SSIS](https://go.microsoft.com/fwlink/?LinkId=220671)sul sito Web bidn.com.  
  
-   Intervento nel Blog relativo al [filtro file con set dinamico SSIS: filespec](https://rajsudeep.blogspot.com/2010/09/ssisdynamically-set-file-mask-filespec.html).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor ciclo foreach &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor ciclo foreach &#40;pagina Mapping variabili&#41;](../../2014/integration-services/foreach-loop-editor-variable-mappings-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Contenitore Ciclo For](control-flow/for-loop-container.md)  
  
  
