---
title: Archiviazione di stringhe e regole di confronto nei modelli tabulari | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8516f0ad-32ee-4688-a304-e705143642ca
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3aad4cf16c39897bc0796f4fb161eaf39abdb5fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938602"
---
# <a name="string-storage-and-collation-in-tabular-models"></a>Archivio di stringhe e regole di confronto nei modelli tabulari
  Le stringhe (valori di testo) vengono archiviate in un formato altamente compresso nei modelli tabulari. A causa di questa compressione, è possibile ottenere risultati imprevisti quando si recuperano stringhe intere o parziali. Inoltre, poiché le regole di confronto e le impostazioni locali delle stringhe vengono ereditate in modo gerarchico dall'oggetto padre più prossimo, se la lingua della stringa non viene definita in modo esplicito, le impostazioni locali e le regole di confronto dell'oggetto padre possono influire sulla modalità di archiviazione di ogni stringa e determinare se la stringa è univoca o unita a stringhe simili secondo quanto definito nelle regole di confronto padre.  
  
 In questo argomento viene illustrato il meccanismo in base al quale le stringhe vengono compresse e archiviate. Inoltre vengono forniti esempi su come le regole di confronto e la lingua influiscono sui risultati delle formule di testo nei modelli tabulari.  
  
## <a name="storage"></a>Archiviazione  
 Nei modelli tabulari tutti i dati sono altamente compressi affinché si adattino alla memoria. Di conseguenza, tutte le stringhe che possono essere considerate equivalenti dal punto di vista lessicale vengono archiviate una sola volta. La prima istanza della stringa viene utilizzata come rappresentazione canonica, dopodiché ogni stringa equivalente viene indicizzata allo stesso valore compresso della prima occorrenza.  
  
 La domanda cruciale è la seguente: cosa si intende per stringa equivalente dal punto di vista lessicale? Due stringhe sono considerate equivalenti dal punto di vista lessicale se possono essere considerate la stessa parola. Ad esempio, in inglese quando si cerca la parola **violin** in un dizionario, è possibile trovare la voce **Violin** o **violin**, a seconda dei criteri editoriali del dizionario, ma in genere le parole possono risultare equivalenti e la differenza nell'utilizzo delle maiuscole può essere ignorata. In un modello tabulare, il fattore che determina se due stringhe sono equivalenti dal punto di vista lessicale non è un criterio editoriale o una preferenza dell'utente, ma le impostazioni locali e l'ordine delle regole di confronto assegnato alla colonna.  
  
 Di conseguenza, sono le regole di confronto e le impostazioni locali a determinare la modalità di utilizzo delle lettere maiuscole e minuscole. Per una parola qualsiasi all'interno delle impostazioni locali, la prima occorrenza trovata in una particolare colonna verrà quindi utilizzata come rappresentazione canonica di quella parola e la stringa verrà archiviata in un formato non compresso.  Tutte le altre stringhe verranno testate rispetto alla prima occorrenza e se superano il test di equivalenza, verranno assegnate al valore compresso della prima occorrenza. In seguito, dopo essere stati recuperati i valori compressi verranno rappresentati utilizzando il valore non compresso della prima occorrenza della stringa.  
  
 Un esempio aiuterà a capire questo concetto. La colonna "Classification - English" è stata estratta da una tabella contenente informazioni su piante e alberi. Per ogni pianta (i nomi delle piante non sono riportati), la colonna di classificazione mostra la categoria generale di pianta.  
  
|Classification - English|  
|-------------------------------|  
|trEE|  
|PlAnT|  
|trEE|  
|PlAnT|  
|PlAnT|  
|Albero|  
|PlAnT|  
|trEE|  
|tree|  
|PlAnT|  
|trEE|  
  
 I dati probabilmente provengono da molte origini diverse, pertanto l'utilizzo delle maiuscole e minuscole e degli accenti non è coerente e queste differenze sono state archiviate così come sono nel database relazionale. In generale i valori sono **Plant** o **Tree**, solo con maiuscole e minuscole diverse.  
  
 Quando questi valori vengono caricati in un modello tabulare che utilizza le regole di confronto predefinite e l'ordinamento per l'inglese (Stati Uniti), case non è importante, pertanto vengono archiviati solo due valori per l'intera colonna:  
  
|Classification - English|  
|-------------------------------|  
|trEE|  
|PlAnT|  
  
 Se si utilizza la colonna **Classification-English**nel modello, ogni volta che si visualizza la classificazione Plant, non vengono visualizzati i valori originali, con i vari utilizzi di maiuscole e minuscole, ma solo la prima istanza. Il motivo è che tutti i diversi utilizzi delle maiuscole e minuscole della parola **tree** vengono considerati equivalenti da queste regole di confronto e da queste impostazioni locali. Di conseguenza, è stata mantenuta una sola stringa e la prima istanza di tale stringa rilevata dal sistema è quella che è stata salvata.  
  
> [!WARNING]  
>  È possibile decidere quale stringa sarà la prima a essere archiviata, in base a ciò che viene considerato corretto, ma tale operazione potrebbe risultare molto difficile. Non esiste un modo semplice per determinare in anticipo quale riga deve essere elaborata per prima dal motore, considerando che tutti i valori vengono considerati equivalenti. In alternativa, se è necessario impostare il valore standard, è necessario eseguire la pulizia di tutte le stringhe prima di caricare il modello.  
  
## <a name="locale-and-collation-order"></a>Impostazioni locali e ordinamento delle regole di confronto  
 Quando si confrontano le stringhe (valori di testo), ciò che definisce l'equivalenza è in genere l'aspetto culturale della modalità di interpretazione di tali stringhe. In alcune culture un accento o l'utilizzo delle maiuscole e maiuscole per un carattere può modificare completamente il significato della stringa. Di conseguenza, tali differenze vengono prese in considerazione per determinare l'equivalenza per un'area o una lingua particolare.  
  
 In genere, il computer è già configurato in base alla propria cultura e al proprio comportamento linguistico e le operazioni eseguite sulle stringhe, ad esempio l'ordinamento e il confronto di valori del testo, generano i risultati previsti. Le impostazioni che controllano il comportamento specifico della lingua vengono definite tramite le **impostazioni locali e della lingua** di Windows. Le applicazioni leggono queste impostazioni e modificano di conseguenza il loro comportamento. In alcuni casi, un'applicazione potrebbe disporre di una caratteristica che consente di modificare il comportamento culturale dell'applicazione o il modo in cui vengono confrontate le stringhe.  
  
 Quando si crea un database del modello tabulare, per impostazione predefinita il database eredita queste impostazioni culturali e linguistiche sotto forma di un identificatore della lingua e di regole di confronto.  
  
-   L'identificatore della lingua definisce il set di caratteri da utilizzare per le stringhe in base alla propria cultura.  
  
-   Le regole di confronto definiscono l'ordinamento dei caratteri e la relativa equivalenza.  
  
 È importante notare che un identificatore della lingua non identifica soltanto una lingua, ma anche il paese o l'area geografica in cui tale lingua viene utilizzata. Ogni identificatore della lingua è associato anche a regole di confronto specificate. Per ulteriori informazioni sugli identificatori di lingua, vedere la pagina relativa agli [ID delle impostazioni locali assegnati da Microsoft](https://msdn.microsoft.com/goglobal/bb964664.aspx). È possibile utilizzare la colonna LCID Dec per ottenere l'ID corretto quando si inserisce manualmente un valore. Per altre informazioni sul concetto SQL delle regole di confronto, vedere [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations). Per informazioni sulle designazioni delle regole di confronto e sugli stili di confronto per i nomi delle regole di confronto di Windows, vedere [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql). L'argomento [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql) offre una mappa dei nomi delle regole di confronto di Windows e i nomi usati per SQL.  
  
 Dopo avere creato il database del modello tabulare, tutti i nuovi oggetti del modello erediteranno gli attributi della lingua e delle regole di confronto dagli attributi del database. Questo vale per tutti gli oggetti. Il percorso di ereditarietà ha inizio dall'oggetto. Nell'elemento padre vengono cercati eventuali attributi della lingua e delle regole di confronto da ereditare e se non ne vengono trovati la ricerca di tali attributi viene spostata al livello del database. In altre parole, se non si specificano gli attributi della lingua e delle regole di confronto per un oggetto, per impostazione predefinita l'oggetto eredita gli attributi dall'elemento padre più prossimo.  
  
 Per le colonne, gli attributi della lingua e delle regole di confronto vengono ereditati alla creazione, secondo le regole seguenti:  
  
1.  Nell'oggetto dimensione padre vengono cercati gli attributi della lingua e delle regole di confronto. Se vengono trovati entrambi, i valori vengono copiati negli attributi della colonna, se ne viene trovato solo uno, l'altro viene dedotto da quello esistente ed entrambi vengono assegnati, se nessuno dei due valori viene trovato, è necessario procedere al passaggio successivo.  
  
2.  La ricerca nell'oggetto di database viene eseguita seguendo lo stesso processo descritto nel Passaggio 1 per le dimensioni. Se non viene trovato alcun attributo, procedere al passaggio successivo.  
  
3.  La ricerca nell'oggetto server viene eseguita seguendo lo stesso processo descritto nel Passaggio 1 per le dimensioni. Se non viene trovato alcun attributo, viene utilizzato l'identificatore della lingua di Windows e l'attributo delle regole di confronto viene dedotto da questo valore.  
  
 È importante notare che in genere l'identificatore della lingua e l'ordinamento delle regole di confronto nel database di origine non hanno praticamente alcun effetto sulla modalità di archiviazione dei valori nella colonna del modello tabulare. Si verifica un'eccezione se il database di origine trasforma o filtra i valori richiesti.  
  
  
