---
title: Opzioni di Richiesta profilo Criteri di ricerca colonna (Attività Profiling dati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 9ccb8fc5-f65e-41a2-9511-7fa55586eb8b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a00c72e6f444ec1e62082f254d6b77894b479d09
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84919642"
---
# <a name="column-pattern-profile-request-options-data-profiling-task"></a>Opzioni di Richiesta profilo Criteri di ricerca colonna (Attività Profiling dati)
  Usare il riquadro **Proprietà richiesta** della pagina **Richieste profilo** per impostare le opzioni per la **Richiesta profilo Criteri di ricerca colonna** selezionata nel riquadro delle richieste. Un profilo Criteri di ricerca colonna segnala un set di espressioni regolari che analizzano la percentuale specificata di valori in una colonna stringa. Questo profilo consente di identificare eventuali problemi nei dati, ad esempio le stringhe non valide, e può indicare le possibili espressioni regolari da utilizzare in futuro per convalidare nuovi valori. Un profilo di criteri di ricerca di una colonna contenente i codici postali ZIP (Stati Uniti), ad esempio, può produrre le espressioni regolari \d{5}-\d{4}, \d{5} e \d{9}. Se vengono visualizzate altre espressioni regolari, è probabile che i dati contengano valori non validi o in formato non corretto.  
  
> [!NOTE]  
>  Le opzioni descritte in questo argomento vengono visualizzate nella pagina **Richieste profilo** in **Editor attività Profiling dati**. Per altre informazioni su questa pagina dell'editor, vedere [Editor attività Profiling dati &#40;pagina Richieste profilo&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Per altre informazioni su come usare l'attività Profiling dati, vedere [Impostazione dell'attività Profiling dati](data-profiling-task.md). Per altre informazioni sull'uso del Visualizzatore profilo dati per analizzare l'output dell'attività Profiling dati, vedere [Visualizzatore profilo dati](data-profile-viewer.md).  
  
## <a name="understanding-the-use-of-delimiters-and-symbols"></a>Informazioni sull'utilizzo di delimitatori e simboli  
 Prima di calcolare i criteri di ricerca per una **Richiesta profilo Criteri di ricerca colonna**, l'attività Profiling dati suddivide in token i dati, ovvero separa i valori stringa in unità minori note come token. L'attività separa le stringhe in token in base ai delimitatori e i simboli specificati per le proprietà **Delimiters** e **Symbols** :  
  
-   **Delimiters** Per impostazione predefinita, l'elenco dei delimitatori contiene i caratteri seguenti: spazio, tabulazione orizzontale (\t), nuova riga (\n) e ritorno a capo (\r). È possibile specificare delimitatori aggiuntivi, ma non è possibile rimuovere i delimitatori predefiniti.  
  
-   **Simboli** Per impostazione predefinita, l'elenco di **simboli** contiene i caratteri seguenti: `,.;:-"'` ~ =&/@!? () <> [] {} | # * ^% `. For example, if the symbols are "` ()-' ", il valore" (425) 123-4567 "viene suddiviso in token come [" ("," 425 ",") "," 123 ","-"," 4567 ",") "].  
  
 Un carattere non può essere simultaneamente un delimitatore e un simbolo.  
  
 Tutti i delimitatori vengono normalizzati in un singolo spazio come parte del processo di suddivisione in token, mentre i simboli vengono mantenuti.  
  
## <a name="understanding-the-use-of-the-tag-table"></a>Informazioni sull'utilizzo della tabella dei tag  
 È facoltativamente possibile raggruppare token correlati con un singolo tag archiviando i tag e i termini correlati in una tabella speciale creata in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La tabella dei tag deve contenere due colonne stringa, denominate "Tag" e "Termine". Tali colonne possono essere di tipo `char`, `nchar`, `varchar` o `nvarchar`, ma non `text` o `ntext`. È possibile combinare più tag e i termini corrispondenti in una singola tabella. Una richiesta di profilo Criteri di ricerca colonna può utilizzare solo una tabella dei tag. È possibile usare una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] distinta per la connessione alla tabella dei tag. Di conseguenza, la tabella dei tag può essere archiviata in un database diverso o un server diverso dalla tabella di origine.  
  
 È possibile, ad esempio, raggruppare i valori "East", "West", "North" e "South" eventualmente visualizzati negli indirizzi stradali statunitensi utilizzando il singolo tag "Direction". La tabella seguente rappresenta un esempio di tale tabella dei tag.  
  
|Tag|Termine|  
|---------|----------|  
|Direction|East|  
|Direction|West|  
|Direction|North|  
|Direction|South|  
  
 È possibile utilizzare un altro tag per raggruppare le parole diverse che esprimono la nozione di strada negli indirizzi stradali:  
  
|Tag|Termine|  
|---------|----------|  
|Via|Street|  
|Street|Avenue|  
|Via|Posizione|  
|Via|Way|  
  
 In base a questa combinazione di tag, il criterio di ricerca risultante per un indirizzo stradale potrebbe essere simile al seguente:  
  
 `\d+\ LookupTag=Direction \d+\p{L}+\ LookupTag=Street`  
  
> [!NOTE]  
>  L'utilizzo di una tabella dei tag influisce negativamente sulle prestazioni dell'attività Profiling dati. Non utilizzare più di 10 tag o più di 100 termini per tag.  
  
 Lo stesso termine può appartenere a più tag.  
  
## <a name="request-properties-options"></a>Opzioni del riquadro Proprietà richiesta  
 Nel riquadro **Proprietà richiesta**per **Richiesta profilo Criteri di ricerca colonna** vengono visualizzati i gruppi di opzioni seguenti:  
  
-   **Dati**che include le opzioni **TableOrView** e **Column**  
  
-   **Generale**  
  
-   **Opzioni**  
  
### <a name="data-options"></a>Opzioni dati  
 **ConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) ai fini della connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contenente la tabella o la vista di cui eseguire il profiling.  
  
 **TableOrView**  
 Consente di selezionare la tabella o la vista esistente che contiene la colonna da analizzare.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni TableorView" in questo argomento.  
  
 **Colonna**  
 Consente di selezionare la colonna esistente da analizzare. Selezionare **( \* )** per profilare tutte le colonne.  
  
 Per ulteriori informazioni, vedere la sezione "Opzioni Column" in questo argomento.  
  
#### <a name="tableorview-options"></a>Opzioni TableOrView  
 **Schema**  
 Specifica lo schema a cui appartiene la tabella selezionata. Questa opzione è di sola lettura.  
  
 **Tabella**  
 Visualizza il nome della tabella selezionata. Questa opzione è di sola lettura.  
  
#### <a name="column-options"></a>Opzioni relative alle colonne  
 **IsWildCard**  
 Specifica se è stato selezionato il carattere jolly **( \* )** . Questa opzione è impostata su **True** se è stato selezionato **(\*)** per profilare tutte le colonne. È impostata su **False** se è stata selezionata una singola colonna da analizzare. Questa opzione è di sola lettura.  
  
 **ColumnName**  
 Visualizza il nome della colonna selezionata. Questa opzione è vuota se è stato selezionato **( \* )** per profilare tutte le colonne. Questa opzione è di sola lettura.  
  
 **StringCompareOptions**  
 Questa opzione non si applica al profilo Criteri di ricerca colonna.  
  
### <a name="general-options"></a>Opzioni generali  
 **RequestID**  
 Nome descrittivo per identificare la richiesta di profilo. Non è in genere necessario modificare il valore generato automaticamente.  
  
### <a name="options"></a>Opzioni  
 **MaxNumberOfPatterns**  
 Specifica il numero massimo di criteri di ricerca che si desidera vengano calcolati dal profilo. Il valore predefinito di questa opzione è 10. Il valore massimo è 100.  
  
 **PercentageDataCoverageDesired**  
 Specifica la percentuale di dati che si desidera vengano analizzati dai criteri di ricerca calcolati. Il valore predefinito di questa opzione è 95 (percentuale).  
  
 **CaseSensitive**  
 Indica se i criteri di ricerca devono applicare la distinzione tra maiuscole e minuscole. Il valore predefinito di questa opzione è **False**.  
  
 **Delimiters**  
 Elenco dei caratteri che devono essere considerati spazi tra parole quando il testo viene suddiviso in token. Per impostazione predefinita, l'elenco **Delimiters** contiene i caratteri seguenti: spazio, tabulazione orizzontale (\t), nuova riga (\n) e ritorno a capo (\r). È possibile specificare delimitatori aggiuntivi, ma non è possibile rimuovere i delimitatori predefiniti.  
  
 Per ulteriori informazioni, tornare alla sezione "Informazioni sull'utilizzo di delimitatori e simboli" di questo argomento.  
  
 **Simboli**  
 Elenco dei simboli che devono essere mantenuti come parte dei criteri di ricerca. I simboli, ad esempio, possono includere "/" per le date, "." per le ore e "@" per gli indirizzi di posta elettronica. Per impostazione predefinita, l'elenco di **simboli** contiene i caratteri seguenti: `,.;:-"'` ~ =&/@!? () <> [] {} | # * ^%'.  
  
 Per ulteriori informazioni, tornare alla sezione "Informazioni sull'utilizzo di delimitatori e simboli" di questo argomento.  
  
 **TagTableConnectionManager**  
 Consente di selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] esistente che usa il provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) ai fini della connessione al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che contiene la tabella dei tag.  
  
 Per ulteriori informazioni, tornare alla sezione "Utilizzo della tabella dei tag" di questo argomento.  
  
 **TagTableName**  
 Consente di selezionare la tabella dei tag esistenti, che deve contenere due colonne stringa denominate Tag e Termine.  
  
 Per ulteriori informazioni, tornare alla sezione "Utilizzo della tabella dei tag" di questo argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività Profiling dati &#40;pagina generale&#41;](../general-page-of-integration-services-designers-options.md)   
 [Form profilo rapido singola tabella &#40;Attività Profiling dati&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
