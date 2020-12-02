---
description: Configurare e gestire i file del thesaurus per la ricerca full-text
title: Configurare e gestire i file del thesaurus per la ricerca full-text
ms.date: 07/01/2020
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: d713b4eb49a527f2cbbbf871cce9d01d4449443d
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130941"
---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>Configurare e gestire i file del thesaurus per la ricerca full-text
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In  le query di ricerca full-text consentono di eseguire una ricerca di sinonimi dei termini specificati dall'utente usando un *thesaurus* della ricerca full-text. Ogni theasurus definisce un set di sinonimi per una lingua specifica. Sviluppando un thesaurus basato sui dati full-text in uso, è possibile ampliare in modo efficace l'ambito delle query full-text su tali dati.

La corrispondenza con il thesaurus si verifica per tutte le query [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) e per tutte le query [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) che specificano la clausola `FORMSOF THESAURUS`.
  
Un thesaurus di ricerca full-text è un file di testo XML.
  
##  <a name="whats-in-a-thesaurus"></a><a name="tasks"></a> Contenuto di un thesaurus  
 Prima che le query di ricerca full-text siano in grado di eseguire la ricerca di sinonimi in una determinata lingua, è necessario definire mapping del thesaurus, ovvero sinonimi, per tale lingua. È necessario configurare manualmente ogni thesaurus per definire gli elementi seguenti:  
  
-   Set di espansione  
  
     Un set di espansione contiene un gruppo di sinonimi, ad esempio "writer", "author" e "journalist", che vengono sostituiti gli uni con gli altri da una query full-text. Le query che contengono una corrispondenza per uno dei sinonimi in un set di espansione vengono espanse per includere ogni altro sinonimo nel set di espansione stesso.  
  
     Per altre informazioni, vedere [Struttura XML di un set di espansione](#expansion) più avanti in questo argomento.  
  
-   Set di sostituzione  
  
     Un set di sostituzione include un criterio di testo da sostituire con parole specifiche. Vedere, ad esempio, la sezione [Struttura XML di un set di sostituzione](#replacement) più avanti in questo argomento. 

-   Impostazione dei segni diacritici  
  
     Per un determinato thesaurus, tutti i criteri di ricerca supportano o non supportano la distinzione relativa ai segni diacritici come la tilde ( **~** ), l'accento acuto ( **&acute;** ), o l'umlaut ( **&uml;** ), ovvero *supportano la distinzione tra caratteri accentati e non accentati* o *non supportano la distinzione tra caratteri accentati e non accentati*. Si supponga, ad esempio, di specificare la sostituzione del criterio "caf&eacute;" con altri criteri in una query di ricerca full-text. Se il thesaurus non supporta la distinzione tra caratteri accentati e non accentati, tramite la ricerca full-text verranno sostituiti i criteri "caf&eacute;" e "cafe". Se il thesaurus supporta la distinzione tra caratteri accentati e non accentati, tramite la ricerca full-text verrà sostituito solo il criterio "caf&eacute;". Per impostazione predefinita, un thesaurus non supporta la distinzione tra caratteri accentati e non accentati.  
  
##  <a name="default-thesaurus-files"></a><a name="initial_thesaurus_files"></a> File del thesaurus predefiniti
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre un set di file XML del thesaurus, uno per ogni lingua supportata. Tali file sono essenzialmente vuoti e contengono solo la struttura XML di livello principale comune a tutti i thesaurus di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e un thesaurus di esempio costituito da commenti.  
  
##  <a name="location-of-thesaurus-files"></a><a name="location"></a> Posizione dei file del thesaurus  
 Il percorso predefinito dei file del thesaurus è il seguente:  
  
`<SQL_Server_data_files_path>\MSSQL13.MSSQLSERVER\MSSQL\FTDATA\`
  
Tale percorso predefinito contiene i file seguenti:  
  
-   File del thesaurus **specifici della lingua**  

    Il programma di installazione installa file del thesaurus vuoti nel percorso sopra indicato, uno per ogni lingua supportata. Tali file possono essere personalizzati da un amministratore di sistema.  
  
    Per i nomi predefiniti dei file del thesaurus viene usato il formato seguente:  
  
    `'ts' + <three-letter language-abbreviation> + '.xml'`
  
    Il nome del file del thesaurus per ogni lingua viene specificato nel valore seguente del Registro di sistema:
     
    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<instance-name>\MSSearch\<language-abbrev>`
  
-   File del thesaurus **globale**  
  
    File del thesaurus globale vuoto denominato tsGlobal.xml.  

### <a name="change-the-location-of-a-thesaurus-file"></a>Modificare il percorso di un file del thesaurus 
È possibile modificare il percorso e il nome di un file del thesaurus modificando la relativa chiave del Registro di sistema. Per ogni lingua, il percorso del file del thesaurus viene specificato nel seguente valore del Registro di sistema:  
  
`HKLM\SOFTWARE\Microsoft\Microsoft SQL Server\<instance name>\MSSearch\Language\<language-abbreviation>\TsaurusFile`
  
 Il file del thesaurus globale corrisponde alla lingua neutra con LCID 0. Questo valore può essere modificato solo dagli amministratori.  

##  <a name="how-full-text-queries-use-the-thesaurus"></a><a name="how_queries_use_tf"></a> Uso del thesaurus per le query full-text  
Una query sul thesaurus usano sia un thesaurus specifico della lingua sia un thesaurus globale.
1.  La query esegue innanzitutto la ricerca in un file specifico della lingua e lo carica per l'elaborazione, a meno che non sia già caricato. La query viene quindi espansa per includere i sinonimi specifici della lingua indicati dalle regole del set di espansione e del set di sostituzione nel file del thesaurus. 
2.  Questi passaggi vengono quindi ripetuti per il thesaurus globale. Se, tuttavia, nel file del thesaurus specifico della lingua è già stata individuata una corrispondenza per un termine, tale termine non può essere considerato valido per la corrispondenza nel thesaurus globale.  

##  <a name="structure-of-a-thesaurus-file"></a><a name="structure"></a> Struttura di un file del thesaurus  
 Ogni file del thesaurus definisce un contenitore XML, il cui ID è `Microsoft Search Thesaurus`, e un commento `<!--` ... `-->` che contiene un thesaurus di esempio. Il thesaurus è definito in un elemento `<thesaurus>` contenente esempi degli elementi figlio che definiscono l'impostazione dei segni diacritici, i set di espansione e i set di sostituzione.

Un file del thesaurus vuoto tipico contiene gli elementi XML seguenti:  
  
```xml  
<XML ID="Microsoft Search Thesaurus">  
  
<!--  Commented out  
  
    <thesaurus xmlns="x-schema:tsSchema.xml">  
<diacritics_sensitive>0</diacritics_sensitive>  
        <expansion>  
            <sub>Internet Explorer</sub>  
            <sub>IE</sub>  
            <sub>IE5</sub>  
        </expansion>  
        <replacement>  
            <pat>NT5</pat>  
            <pat>W2K</pat>  
            <sub>Windows 2012</sub>  
        </replacement>  
        <expansion>  
            <sub>run</sub>  
            <sub>jog</sub>  
        </expansion>  
    </thesaurus>  
-->  
</XML>  
```

### <a name="xml-structure-of-an-expansion-set"></a><a name="expansion"></a> XML structure of an expansion set  
  
 Ogni set di espansione è racchiuso in un elemento `<expansion>`. All'interno di questo elemento è possibile specificare una o più sostituzioni in un elemento `<sub>`. Nel set di espansione è possibile specificare un gruppo di sostituzioni che sono sinonimi una dell'altra.  
  
 Ad esempio, è possibile modificare la sezione di espansione per considerare le sostituzioni "writer", "author" e "journalist" come sinonimi. per includere tutte le altre sostituzioni specificate nel set di espansione, vengono espanse le query di ricerca full-text che contengono corrispondenze in una sostituzione. Di conseguenza, quando nell'esempio precedente si esegue una query FORMS OF THESAURUS o FREETEXT per la parola "author", vengono restituiti anche i risultati di ricerca contenenti le parole "writer" e "journalist".  
  
La sezione del set di espansione dell'esempio precedente sarà la seguente:  
  
```xml  
<expansion>  
        <sub>writer</sub>  
        <sub>author</sub>  
        <sub>journalist</sub>  
</expansion>  
```  
  
### <a name="xml-structure-of-a-replacement-set"></a><a name="replacement"></a> XML structure of a replacement set  
  
Ogni set di sostituzione è racchiuso in un elemento `<replacement>`. All'interno di questo elemento è possibile specificare uno o più criteri in un elemento `<pat>` e zero o più sostituzioni in elementi `<sub>`, uno per sinonimo. È possibile specificare un criterio da sostituire con un set di sostituzione. I criteri e le sostituzioni possono contenere una parola o una sequenza di parole. Se non viene specificata alcuna sostituzione per un criterio, questo verrà rimosso dalla query dell'utente.  
  
Si supponga, ad esempio, di voler eseguire query per sostituire il criterio "Win8" con "Windows Server 2012" o "Windows 8.0". Se si esegue una query full-text per "Win8", verranno restituiti solo i risultati di ricerca full-text contenenti le sostituzioni "Windows Server 2012" o "Windows 8.0". ma non quelli contenenti "Win8". Questo accade perché "Win8" è stato "sostituito" con "Windows Server 2012" e "Windows 8.0".  
  
La sezione del set di sostituzione dell'esempio sopra descritto sarebbe:  
  
```xml  
<replacement>  
        <pat>Win8</pat>  
        <sub>Windows Server 2012</sub>  
        <sub>Windows 8.0</sub>  
</replacement>  
```  
  
Se sono presenti due set di sostituzione con criteri di testo simili da associare, il più lungo dei due ha la precedenza. Se, ad esempio, si esegue una query FORMS OF THESAURUS per "Internet Explorer online community" e sono presenti i set di sostituzione indicati di seguito, "Internet Explorer" ha la precedenza su "Internet". La query verrà pertanto elaborata come "IE online community" o "IE 9 online community".  
  
```xml  
<replacement>  
         <pat>Internet</pat>  
         <sub>intranet</sub>  
</replacement>  
```  
  
e  
  
```xml  
<replacement>  
         <pat>Internet Explorer</pat>  
         <sub>IE</sub>  
         <sub>IE 9</sub>  
</replacement>  
```

### <a name="xml-structure-of-the-diacritics-setting"></a>Struttura XML dell'impostazione dei segni diacritici  
  
L'impostazione dei segni diacritici di un thesaurus è specificata in un singolo elemento `<diacritics_sensitive>`, che contiene un valore intero che determina il supporto della distinzione tra caratteri accentati e non accentati, come indicato di seguito:  
  
|Impostazione dei segni diacritici|valore|XML|  
|------------------------|-----------|---------|  
|non supportano la distinzione tra caratteri accentati e non accentati|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
|supportano la distinzione tra caratteri accentati e non accentati|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
> [!NOTE]  
>  Questa impostazione può essere applicata solo una volta nel file e si applica a tutti i criteri di ricerca nel file. L'impostazione non può essere specificata per singoli criteri.  

##  <a name="edit-a-thesaurus-file"></a><a name="editing"></a> Modificare un file del thesaurus  
È possibile configurare il thesaurus per una lingua specifica modificando il relativo file XML. Durante la configurazione vengono installati file del thesaurus vuoti che contengono solo il contenitore `<xml>` e un elemento `<thesaurus` di esempio impostato come commento. Ai fini della corretta esecuzione delle query di ricerca full-text per la ricerca di sinonimi, è necessario creare un elemento `<thesaurus`> effettivo che definisca un set di sinonimi. È possibile definire due forme di sinonimi, i set di espansione e i set di sostituzione.  

### <a name="edit-a-thesaurus-file"></a>Modificare un file del thesaurus  
  
1.  Aprire il file del thesaurus nel Blocco note o in un altro editor di testo.  
  
2.  Se si modifica un file del thesaurus per la prima volta, rimuovere le righe di commento seguenti all'inizio e alla fine del file, rispettivamente:  
  
    ```xml  
    <!--Commented out  
    -->  
    ```  
  
3.  Aggiungere, modificare o eliminare un set di sostituzione o un set di espansione.  
  
4.  Salvare il file e chiudere il Blocco note.  
  
5.  Utilizzare [sp_fulltext_load_thesaurus_file](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md) per caricare il contenuto del file del thesaurus in tempdb, specificando l'identificatore LCID corrispondente alla lingua del file del thesaurus. Per il file del thesaurus per la lingua inglese, denominato tsenu.xml, l'identificatore LCID corrispondente è 1033.  
  
    ```sql  
    USE AdventureWorks;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO
    ```

### <a name="recommendations-for-editing-thesaurus-files"></a>Indicazioni per la modifica dei file del thesaurus  
  
 È consigliabile che le voci del file del thesaurus non contengano caratteri speciali, in quanto i word breaker rivelano comportamenti imprevedibili in presenza di tale tipo di caratteri. Se una voce del thesaurus contiene un carattere speciale, i word breaker usati in combinazione con la voce possono avere un comportamento imprevisto con implicazioni su una query full-text.  
  
 È consigliabile che le voci `<sub>` non contengano parole non significative, in quanto tali parole vengono omesse dall'indice full-text. Le query vengono espanse per includere le voci `<sub>` da un file del thesaurus e se una voce `<sub>` contiene parole non significative, le dimensioni della query aumentano inutilmente.  

### <a name="restrictions-for-editing-thesaurus-files"></a>Limitazioni per la modifica dei file del thesaurus  
  
 Alla modifica di un file del thesaurus si applicano le restrizioni seguenti:  
  
-   Solo gli amministratori di sistema possono aggiornare, modificare o eliminare i file del thesaurus.  
  
-   Quando si usano editor di testo per modificare i file del thesaurus, è necessario salvare i file in formato Unicode e specificare gli indicatori per l'ordine dei byte (BOM).  
  
-   Le voci del thesaurus non possono essere vuote e non è possibile eseguirne il word breaking in una stringa vuota.  
  
-   Le frasi nel file del thesaurus non devono essere costituite da più di 512 caratteri.  
  
-   Un thesaurus non deve contenere alcuna voce duplicata fra le voci `<sub>` dei set di espansione e gli elementi `<pat>` dei set di sostituzione.  

## <a name="see-also"></a>Vedere anche  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)     
 [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql.md)  
 [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)
 
