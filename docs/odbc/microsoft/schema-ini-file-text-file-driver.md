---
title: File Schema.ini (Driver file di testo) Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305512"
---
# <a name="schemaini-file-text-file-driver"></a>File Schema.ini (driver file di testo)
Quando viene utilizzato il driver di testo, il formato del file di testo viene determinato utilizzando un file di informazioni sullo schema. Il file di informazioni sullo schema è sempre denominato Schema.ini e viene sempre mantenuto nella stessa directory dell'origine dati di testo. Il file di informazioni sullo schema fornisce a IISAM informazioni sul formato generale del file, sul nome della colonna e sul tipo di dati e su diverse altre caratteristiche dei dati. Un file Schema.ini è sempre necessario per accedere ai dati a lunghezza fissa. È necessario utilizzare un file Schema.ini quando la tabella di testo contiene dati DateTime, Currency o Decimal o in qualsiasi momento in cui si desidera un maggiore controllo sulla gestione dei dati nella tabella.  
  
> [!NOTE]  
>  L'ISAM Text otterrà i valori iniziali dal Registro di sistema, non da Schema.ini. Lo stesso formato di file predefinito si applica a tutte le nuove tabelle di dati di testo. Tutti i file creati dall'istruzione CREATE TABLE ereditano gli stessi valori di formato predefiniti, che \<vengono impostati selezionando i valori del formato di file nella finestra di dialogo **Definisci formato testo** con i> predefiniti selezionati nell'elenco **Tabelle.** Se i valori nel Registro di sistema sono diversi dai valori in Schema.ini, i valori nel Registro di sistema verranno sovrascritti dai valori di Schema.ini.  
  
## <a name="understanding-schemaini-files"></a>Informazioni sui file Schema.iniUnderstanding Schema.ini Files  
 I file Schema.ini forniscono informazioni sullo schema relative ai record in un file di testo. Ogni voce Schema.ini specifica una delle cinque caratteristiche della tabella:  
  
-   Il nome del file di testo  
  
-   Il formato del file  
  
-   Nomi, larghezze e tipi dei campi  
  
-   Il set di caratteri  
  
-   Conversioni di tipi di dati specialiSpecial data type conversions  
  
 Le sezioni seguenti illustrano queste caratteristiche.  
  
## <a name="specifying-the-file-name"></a>Specifica del nome del file  
 La prima voce in Schema.ini è sempre il nome del file di origine del testo racchiuso tra parentesi quadre. Nell'esempio seguente viene illustrata la voce relativa al file Sample.txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Specifica del formato di file  
 L'opzione **Format** in Schema.ini specifica il formato del file di testo. Il testo IISAM può leggere automaticamente il formato dalla maggior parte dei file delimitati da caratteri. È possibile utilizzare qualsiasi carattere singolo come delimitatore nel file ad eccezione delle virgolette doppie ("). L'impostazione **Format** in Schema.ini sostituisce l'impostazione nel Registro di sistema di Windows, file per file. Nella tabella seguente sono elencati i valori validi per l'opzione **Format.**  
  
|Identificatore di formato|Formato tabella|Istruzione Schema.ini Format|  
|----------------------|------------------|---------------------------------|  
|**Delimitato da tabulazione**|I campi nel file sono delimitati da tabulazioni.|Formato: delimitato da tabulazioni|  
|**Delimitato CSV**|I campi nel file sono delimitati da virgole (valori delimitati da virgole).|Formato: CSVElimited|  
|**Delimitato personalizzato**|I campi nel file sono delimitati da qualsiasi carattere che si sceglie di immettere nella finestra di dialogo. Sono consentiti tutti tranne le virgolette doppie (") , incluso lo spazio vuoto.|Formato: delimitato *(carattere personalizzato*)<br /><br /> -oppure-<br /><br /> Senza delimitatore specificato:<br /><br /> Formato: delimitato( )|  
|**Lunghezza fissa**|I campi nel file sono di lunghezza fissa.|Formato: FixedLength (Formato)|  
  
## <a name="specifying-the-fields"></a>Specifica dei campi  
 È possibile specificare i nomi dei campi in un file di testo delimitato da caratteri in due modi:  
  
-   Includere i nomi dei campi nella prima riga della tabella e impostare **ColNameHeader** su **True.**  
  
-   Specificare ogni colonna in base al numero e designare il nome e il tipo di dati della colonna.  
  
 È necessario specificare ogni colonna in base al numero e designare il nome della colonna, il tipo di dati e la larghezza per i file a lunghezza fissa.  
  
> [!NOTE]  
>  L'impostazione **ColNameHeader** in Schema.ini esegue l'override dell'impostazione **FirstRowHasNames** nel Registro di sistema di Windows, file per file.  
  
 È inoltre possibile determinare i tipi di dati dei campi. Utilizzare l'opzione **MaxScanRows** per indicare il numero di righe da analizzare quando si determinano i tipi di colonna. Se si imposta **MaxScanRows** su 0, viene analizzato l'intero file. L'impostazione **MaxScanRows** in Schema.ini sostituisce l'impostazione nel Registro di sistema di Windows, file per file.  
  
 La voce seguente indica che Microsoft Jet deve utilizzare i dati nella prima riga della tabella per determinare i nomi dei campi e deve esaminare l'intero file per determinare i tipi di dati utilizzati:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 La voce successiva definisce i campi di una tabella utilizzando l'opzione relativa al numero di colonna (**Col**_n_), facoltativa per i file delimitati da caratteri e necessaria per i file a lunghezza fissa. Nell'esempio vengono illustrate le voci Schema.ini per due campi, un campo di testo CustomerNumber di 10 caratteri e un campo di testo NomeCliente di 30 caratteri:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintassi di **Col**_n_ è:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella tabella seguente viene descritta ogni parte della voce **Col**_n._  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*ColumnName*|Nome di testo della colonna. Se il nome della colonna contiene spazi incorporati, è necessario racchiuderlo tra virgolette doppie.|  
|*type*|I tipi di dati sono i seguenti:<br /><br /> **Tipi di dati di Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> Valuta<br /><br /> Single<br /><br /> Double<br /><br /> Datetime<br /><br /> Testo<br /><br /> Memo<br /><br /> **Tipi di dati ODBC** Char (come Testo)<br /><br /> Float (uguale a Double)<br /><br /> Intero (uguale a Short)<br /><br /> LongChar (come Memo)<br /><br /> Formato *data data*|  
|**Larghezza**|Valore della `Width`stringa letterale . Indica che il numero seguente indica la larghezza della colonna (facoltativo per i file delimitati da caratteri; obbligatorio per i file a lunghezza fissa).|  
|*#*|Valore intero che definisce la larghezza della colonna (obbligatorio se **Width** è specificato).|  
  
## <a name="selecting-a-character-set"></a>Selezione di un set di caratteri  
 È possibile scegliere tra due set di caratteri: ANSI e OEM. L'impostazione **CharacterSet** in Schema.ini sostituisce l'impostazione nel Registro di sistema di Windows, file per file. Nell'esempio seguente viene illustrata la voce Schema.ini che imposta il set di caratteri su ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Specifica dei formati dei tipi di dati e delle conversioniSpecifying Data Type Formats and Conversions  
 Il file Schema.ini contiene diverse opzioni che è possibile utilizzare per specificare la modalità di conversione o visualizzazione dei dati. Nella tabella seguente sono elencate tutte queste opzioni.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**DateTimeFormat**|Può essere impostato su una stringa di formato che indica date e ore. È necessario specificare questa voce se tutti i campi data/ora nell'importazione/esportazione vengono gestiti con lo stesso formato. Tutti i formati Microsoft Jet ad eccezione di A.M. sia quello sono supportate. Se non è presente alcuna stringa di formato, vengono utilizzate le opzioni di data e ora brevi del Pannello di controllo di Windows.|  
|**Simbolo decimale**|Può essere impostato su qualsiasi carattere singolo utilizzato per separare il numero intero dalla parte frazionaria di un numero.|  
|**NumberDigits**|Indica il numero di cifre decimali nella parte frazionaria di un numero.|  
|**NumeroPorta zero**|Specifica se un valore decimale minore di 1 e maggiore di -1 deve contenere zeri iniziali; questo valore può essere False (nessun zero iniziale) o True.|  
|**CurrencySymbol**|Indica il simbolo di valuta che può essere utilizzato per i valori di valuta nel file di testo. Gli esempi includono il simbolo del dollaro (-) e Dm.|  
|**CurrencyPosFormat (Formato CurrencyPos)**|Può essere impostato su uno dei seguenti valori:<br /><br /> - Prefisso del simbolo di valuta senza separazione (n. 1)<br />- Suffisso simbolo di valuta senza separazione (1)<br />- Prefisso del simbolo di valuta con una separazione di caratteri (n. 1)<br />- Suffisso simbolo di valuta con una separazione di caratteri (1 )|  
|**CurrencyDigits (Cifra)**|Specifica il numero di cifre utilizzate per la parte frazionaria di un importo in valuta.|  
|**Formato CurrencyNeg**|I possibili valori sono i seguenti:<br /><br /> - (n. 1)<br />- - 1 USD<br />- N. 1 (da 1 USD)<br />- 1 USD<br />- (1o)<br />- - 1o<br />- 1-e<br />- 1 o più anni<br />- 1.<br />- - 1<br />- 1 - -<br />- 1- USD<br />- -1 USD<br />- 1- .<br />- (n. 1)<br />- (1 usd)<br /><br /> In questo esempio viene illustrato il simbolo del dollaro, ma è necessario sostituirlo con il valore **CurrencySymbol** appropriato nel programma effettivo.|  
|**CurrencyThousandSimbolo**|Indica il simbolo a carattere singolo che può essere utilizzato per separare i valori di valuta nel file di testo per migliaia.|  
|**CurrencyDecimalSymbol (Simbolo CurrencyDecimal)**|Può essere impostato su qualsiasi carattere singolo utilizzato per separare l'intero dalla parte frazionaria di un importo in valuta.|  
  
> [!NOTE]  
>  Se si omettere una voce, viene utilizzato il valore predefinito nel Pannello di controllo di Windows.
