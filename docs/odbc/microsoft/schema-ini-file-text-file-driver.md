---
title: File schema. ini (driver file di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365351724f27205e7d460c757f1268d042cefc76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305512"
---
# <a name="schemaini-file-text-file-driver"></a>File Schema.ini (driver file di testo)
Quando si utilizza il driver di testo, il formato del file di testo viene determinato utilizzando un file di informazioni sullo schema. Il file di informazioni sullo schema è sempre denominato schema. ini e viene sempre mantenuto nella stessa directory dell'origine dati di testo. Il file di informazioni sullo schema fornisce IISAM con informazioni sul formato generale del file, il nome della colonna e le informazioni sul tipo di dati e diverse altre caratteristiche dei dati. Per accedere ai dati a lunghezza fissa è sempre necessario un file schema. ini. È consigliabile utilizzare un file schema. ini quando la tabella di testo contiene dati DateTime, Currency o Decimal oppure ogni volta che si desidera un maggiore controllo sulla gestione dei dati nella tabella.  
  
> [!NOTE]  
>  L'ISAM del testo otterrà i valori iniziali dal registro di sistema, non da schema. ini. Lo stesso formato di file predefinito si applica a tutte le nuove tabelle di dati di testo. Tutti i file creati dall'istruzione CREATE TABLE ereditano gli stessi valori di formato predefiniti, che vengono impostati selezionando i valori del formato di file nella finestra di dialogo **Definisci formato testo** con \<> predefiniti selezionati nell'elenco **tabelle** . Se i valori nel registro di sistema sono diversi da quelli di schema. ini, i valori del registro di sistema verranno sovrascritti dai valori di schema. ini.  
  
## <a name="understanding-schemaini-files"></a>Informazioni sui file schema. ini  
 I file schema. ini forniscono informazioni sullo schema relative ai record in un file di testo. Ogni voce di schema. ini specifica una delle cinque caratteristiche della tabella:  
  
-   Nome del file di testo  
  
-   Formato del file  
  
-   Nomi dei campi, larghezze e tipi  
  
-   Set di caratteri  
  
-   Conversioni speciali dei tipi di dati  
  
 Le sezioni seguenti illustrano queste caratteristiche.  
  
## <a name="specifying-the-file-name"></a>Specifica del nome file  
 La prima voce di schema. ini è sempre il nome del file di origine di testo racchiuso tra parentesi quadre. Nell'esempio seguente viene illustrata la voce relativa al file Sample. txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Specifica del formato di file  
 L'opzione **Format** in Schema. ini specifica il formato del file di testo. Il testo IISAM può leggere il formato automaticamente dalla maggior parte dei file delimitati da caratteri. È possibile utilizzare qualsiasi carattere singolo come delimitatore nel file eccetto le virgolette doppie ("). L'impostazione del **formato** in Schema. ini sostituisce l'impostazione nel registro di sistema di Windows, file per file. Nella tabella seguente sono elencati i valori validi per l'opzione **Format** .  
  
|Identificatore di formato|Formato tabella|Istruzione di formato schema. ini|  
|----------------------|------------------|---------------------------------|  
|**Delimitato da tabulazione**|I campi nel file sono delimitati da tabulazioni.|Formato = TabDelimited|  
|**CSV delimitati**|I campi nel file sono delimitati da virgole (valori separati da virgole).|Formato = CSVDelimited|  
|**Delimitato personalizzato**|I campi nel file sono delimitati da qualsiasi carattere scelto per l'input nella finestra di dialogo. Sono consentite tutte le virgolette doppie ("), incluso blank.|Format = delimitato (*carattere personalizzato*)<br /><br /> -oppure-<br /><br /> Non è stato specificato alcun delimitatore:<br /><br /> Formato = delimitato ()|  
|**Lunghezza fissa**|I campi nel file hanno una lunghezza fissa.|Formato = FixedLength|  
  
## <a name="specifying-the-fields"></a>Specifica dei campi  
 È possibile specificare i nomi dei campi in un file di testo con valori delimitati da caratteri in due modi:  
  
-   Includere i nomi dei campi nella prima riga della tabella e impostare **ColNameHeader** su **true.**  
  
-   Specificare ogni colonna in base al numero e designare il nome della colonna e il tipo di dati.  
  
 È necessario specificare ogni colonna in base al numero e designare il nome della colonna, il tipo di dati e la larghezza per i file a lunghezza fissa.  
  
> [!NOTE]  
>  L'impostazione **ColNameHeader** in Schema. ini sostituisce l'impostazione **FirstRowHasNames** nel registro di sistema di Windows, file per file.  
  
 È possibile determinare anche i tipi di dati dei campi. Utilizzare l'opzione **MaxScanRows** per indicare il numero di righe che devono essere analizzate quando si determinano i tipi di colonna. Se si imposta **MaxScanRows** su 0, viene eseguita l'analisi dell'intero file. L'impostazione **MaxScanRows** in Schema. ini sostituisce l'impostazione nel registro di sistema di Windows, file per file.  
  
 La voce seguente indica che Microsoft Jet deve usare i dati nella prima riga della tabella per determinare i nomi dei campi ed esaminare l'intero file per determinare i tipi di dati usati:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 La voce successiva designa i campi di una tabella utilizzando l'opzione numero di colonna (**col**_n_), che è facoltativa per i file delimitati da caratteri e necessaria per i file a lunghezza fissa. Nell'esempio vengono illustrate le voci schema. ini per due campi, un campo di testo CustomerNumber di 10 caratteri e un campo di testo CustomerName di 30 caratteri:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintassi di **col**_n_ è la seguente:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Osservazioni  
 La tabella seguente descrive ogni parte della voce **col**_n_ .  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*ColumnName*|Nome di testo della colonna. Se il nome della colonna contiene spazi incorporati, è necessario racchiuderlo tra virgolette doppie.|  
|*type*|I tipi di dati sono i seguenti:<br /><br /> **Tipi di dati Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> Valuta<br /><br /> Single<br /><br /> Double<br /><br /> Datetime<br /><br /> Testo<br /><br /> Memo<br /><br /> **Tipi di dati ODBC** Char (uguale a testo)<br /><br /> Float (uguale a Double)<br /><br /> Integer (uguale a short)<br /><br /> LongChar (uguale a memo)<br /><br /> *Formato data* data|  
|**Larghezza**|Valore `Width`stringa letterale. Indica che il numero seguente indica la larghezza della colonna (facoltativa per i file delimitati da caratteri; obbligatoria per i file a lunghezza fissa).|  
|*#*|Valore intero che definisce la larghezza della colonna (obbligatoria se è specificata la **larghezza** ).|  
  
## <a name="selecting-a-character-set"></a>Selezione di un set di caratteri  
 È possibile scegliere tra due set di caratteri: ANSI e OEM. L'impostazione del set di **caratteri** in Schema. ini sostituisce l'impostazione nel registro di sistema di Windows, file per file. Nell'esempio seguente viene illustrata la voce Schema. ini che imposta il set di caratteri su ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Specifica di formati e conversioni di tipi di dati  
 Il file schema. ini contiene diverse opzioni che è possibile utilizzare per specificare la modalità di conversione o visualizzazione dei dati. La tabella seguente elenca ognuna di queste opzioni.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**DateTimeFormat**|Può essere impostato su una stringa di formato che indica date e ore. È necessario specificare questa voce se tutti i campi di data/ora nell'importazione/esportazione vengono gestiti con lo stesso formato. Tutti i formati Microsoft Jet eccetto A.M. sia quello sono supportate. Se non è presente alcuna stringa di formato, vengono usate le opzioni immagine e ora del pannello di controllo di Windows.|  
|**DecimalSymbol**|Può essere impostato su qualsiasi singolo carattere utilizzato per separare il valore intero dalla parte frazionaria di un numero.|  
|**NumberDigits**|Indica il numero di cifre decimali nella parte frazionaria di un numero.|  
|**NumberLeadingZeros**|Specifica se un valore decimale minore di 1 e maggiore di-1 deve contenere zeri iniziali; Questo valore può essere false (senza zeri iniziali) o true.|  
|**CurrencySymbol**|Indica il simbolo di valuta che può essere usato per i valori di valuta nel file di testo. Gli esempi includono il simbolo del dollaro ($) e il DM.|  
|**CurrencyPosFormat**|Può essere impostato su uno dei valori seguenti:<br /><br /> -Prefisso del simbolo di valuta senza separazione ($1)<br />-Suffisso del simbolo di valuta senza separazione ($1)<br />-Prefisso del simbolo di valuta con una separazione di caratteri ($1)<br />-Suffisso del simbolo di valuta con una separazione di caratteri ($1)|  
|**CurrencyDigits**|Specifica il numero di cifre utilizzate per la parte frazionaria di un importo di valuta.|  
|**CurrencyNegFormat**|I possibili valori sono i seguenti:<br /><br /> -($1)<br />--$1<br />-$-1<br />-$1-<br />-($1)<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-$-1<br />-1-$<br />-($1)<br />-($1)<br /><br /> Questo esempio mostra il simbolo del dollaro, ma è necessario sostituirlo con il valore di **CurrencySymbol** appropriato nel programma effettivo.|  
|**CurrencyThousandSymbol**|Indica il simbolo a carattere singolo che può essere usato per separare le migliaia di valori di valuta nel file di testo.|  
|**CurrencyDecimalSymbol**|Può essere impostato su qualsiasi singolo carattere utilizzato per separare l'intero dalla parte frazionaria di un importo di valuta.|  
  
> [!NOTE]  
>  Se si omette una voce, viene usato il valore predefinito nel pannello di controllo di Windows.
