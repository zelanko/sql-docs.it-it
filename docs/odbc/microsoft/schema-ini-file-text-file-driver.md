---
title: File schema ini (Driver File di testo) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd95329c91c69af38b1ffc7951191498fcc40479
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987941"
---
# <a name="schemaini-file-text-file-driver"></a>File Schema.ini (driver file di testo)
Quando viene usato il driver di testo, il formato del file di testo viene determinato usando un file di informazioni dello schema. Il file di informazioni dello schema è sempre denominato schema. ini e mantenuto sempre nella stessa directory dell'origine dati di testo. Il file di informazioni dello schema fornisce le IISAM con informazioni sul formato generale del file, il nome della colonna e le informazioni sul tipo di dati e diverse altre caratteristiche di dati. File schema ini è sempre obbligatorio per l'accesso ai dati a lunghezza fissa. Quando la tabella di testo contiene DateTime, Currency, o dati Decimal o ogni volta che si desidera maggiore controllo sulla gestione dei dati nella tabella, è consigliabile utilizzare un file ini.  
  
> [!NOTE]  
>  Il testo ISAM otterrà valori iniziali dal Registro di sistema, ma non da schema. ini. Lo stesso formato di file predefinito si applica a tutte le nuove tabelle di dati di testo. Tutti i file creati dall'istruzione CREATE TABLE ereditano questi stessi valori di formato predefinito, che vengono impostate selezionando i valori di formato di file nei **definire formato di testo** finestra di dialogo con \<predefinito > scelto nel  **Tabelle** elenco. Se i valori del Registro di sistema sono diversi dai valori di schema. ini, i valori del Registro di sistema verranno sovrascritti dai valori di schema. ini.  
  
## <a name="understanding-schemaini-files"></a>Informazioni sui file di schema. ini  
 I file ini forniscono informazioni sullo schema relative i record in un file di testo. Ogni voce di schema. ini consente di specificare una delle cinque caratteristiche della tabella:  
  
-   Il nome del file di testo  
  
-   Il formato di file  
  
-   I nomi dei campi, larghezza delle colonne e tipi  
  
-   Il set di caratteri  
  
-   Conversioni di tipi di dati speciali  
  
 Le sezioni seguenti illustrano queste caratteristiche.  
  
## <a name="specifying-the-file-name"></a>Specifica il nome del File  
 La prima voce di schema. ini è sempre il nome del file di origine in testo racchiuso tra parentesi quadre. Nell'esempio seguente viene illustrata la voce per il file Sample. txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Che specifica il formato di File  
 Il **formato** opzione di schema. ini consente di specificare il formato del file di testo. Text IISAM possibile leggere il formato automaticamente da più caratteri-file delimitati da virgole. È possibile usare qualsiasi singolo carattere come delimitatore del file eccetto le virgolette doppie ("). Il **formato** impostazione ini sostituisce l'impostazione nel Registro di sistema Windows, file per file. Nella tabella seguente sono elencati i valori validi per il **formato** opzione.  
  
|Identificatore di formato|Formato di tabella|Istruzione di formato di schema. ini|  
|----------------------|------------------|---------------------------------|  
|**Valori delimitati da tabulazioni**|Campi nel file sono delimitati da tabulazioni.|Formato = TabDelimited|  
|**Delimitato da virgola**|Campi nel file sono delimitati da virgole (con valori delimitati da virgole).|Formato = CSVDelimited|  
|**Personalizzato**|I campi nel file sono delimitati da qualsiasi carattere che si sceglie di input nella finestra di dialogo. Tutto eccetto le virgolette doppie (") sono consentiti, tra cui vuoto.|Formato = delimitato (*caratteri personalizzato*)<br /><br /> -oppure-<br /><br /> Con alcun delimitatore specificato:<br /><br /> Formato = delimitato)|  
|**Lunghezza fissa**|I campi nel file sono di lunghezza fissa.|Formato = FixedLength|  
  
## <a name="specifying-the-fields"></a>Che specifica i campi  
 È possibile specificare i nomi dei campi in un file di testo delimitati da caratteri in due modi:  
  
-   Includere i nomi dei campi nella prima riga della tabella e impostare **ColNameHeader** a **True.**  
  
-   Specificare ogni colonna in base al numero e designare il tipo di dati e nome di colonna.  
  
 È necessario specificare ogni colonna in base al numero e definire il nome della colonna, tipo di dati e larghezza per i file di lunghezza fissa.  
  
> [!NOTE]  
>  Il **ColNameHeader** impostazione in override ini il **FirstRowHasNames** impostazione nel Registro di sistema Windows, file per file.  
  
 Possono essere determinati anche i tipi di dati dei campi. Usare la **MaxScanRows** opzione per indicare il numero di righe deve essere analizzato per determinare i tipi di colonna. Se si imposta **MaxScanRows** su 0, viene analizzato l'intero file. Il **MaxScanRows** impostazione ini sostituisce l'impostazione nel Registro di sistema Windows, file per file.  
  
 La voce seguente indica che Microsoft Jet deve usare i dati nella prima riga della tabella per determinare i nomi dei campi e deve esaminare l'intero file per determinare i dati di tipi usati:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 Alla voce successiva definisce i campi in una tabella con il numero di colonna (**Col**_n_) opzione, che è facoltativa per i file delimitati da caratteri ed è obbligatorio per i file di lunghezza fissa. L'esempio mostra le voci di schema. ini per due campi, un campo di testo NumeroCliente 10 caratteri e un campo di testo CustomerName 30 caratteri:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintassi del **Col**_n_ è:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Note  
 La tabella seguente descrive ogni parte i **Col**_n_ voce.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|*ColumnName*|Il nome della colonna di testo. Se il nome della colonna contiene spazi incorporati, è necessario racchiuderlo tra virgolette.|  
|*type*|Come indicato di seguito sono riportati i tipi di dati:<br /><br /> **Tipi di dati di Microsoft Jet**<br /><br /> Bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> Currency<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Testo<br /><br /> Memo<br /><br /> **Tipi di dati ODBC** Char (lo stesso testo)<br /><br /> Float (uguale a Double)<br /><br /> Integer (uguale a breve)<br /><br /> LongChar (uguale al credito)<br /><br /> Data *formato data*|  
|**Width**|Il valore di stringa letterale `Width`. Indica che il numero seguente definisce la larghezza della colonna (facoltativo per i file delimitati da caratteri; richiesto per i file di lunghezza fissa).|  
|*#*|Il valore intero che definisce la larghezza della colonna (obbligatorio se **larghezza** è specificato).|  
  
## <a name="selecting-a-character-set"></a>Selezione di un Set di caratteri  
 È possibile scegliere tra due set di caratteri: ANSI e OEM. Il **CharacterSet** impostazione ini sostituisce l'impostazione nel Registro di sistema Windows, file per file. Nell'esempio seguente mostra la voce di schema. ini che imposta il set di caratteri da ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Specificare i formati di tipo di dati e conversioni  
 Il file di schema. ini contiene numerose opzioni che è possibile usare per specificare come i dati vengono convertiti o visualizzati. Nella tabella seguente sono elencati ognuna di queste opzioni.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**DateTimeFormat**|Può essere impostato su una stringa di formato che indica le date e ore. Se tutti i campi di data/ora nell'importazione/esportazione sono gestiti con lo stesso formato, è necessario specificare questa voce. Tutti i formati di Microsoft Jet, ad eccezione del mattino. A.M. /p.m. sono supportati. Se è presente alcuna stringa di formato, vengono utilizzate le opzioni di immagine e l'ora di data breve del Pannello di controllo Windows.|  
|**DecimalSymbol**|Può essere impostato su qualsiasi carattere singolo che viene usato per separare il valore integer dalla parte frazionaria di un numero.|  
|**NumberDigits**|Indica il numero di cifre decimali nella parte frazionaria di un numero.|  
|**NumberLeadingZeros**|Specifica se un valore decimale minore di 1 e più di 1 deve contenere zeri iniziali. Questo valore può essere entrambi False (senza zeri iniziali) o True.|  
|**CurrencySymbol**|Indica il simbolo di valuta che può essere usato per i valori di valuta nel file di testo. Ad esempio il segno di dollaro ($) e gestione dei dispositivi.|  
|**CurrencyPosFormat**|Può essere impostata su uno dei valori seguenti:<br /><br /> -Il simbolo di valuta prefisso senza separazione ($1)<br />-Il simbolo di valuta suffisso con nessuna separazione tra (1$)<br />-Il simbolo di valuta prefisso con un carattere di separazione ($ 1)<br />-Il simbolo di valuta suffisso con un carattere di separazione (1 $)|  
|**CurrencyDigits**|Specifica il numero di cifre utilizzate per la parte frazionaria di un importo di valuta.|  
|**CurrencyNegFormat**|Il valore può essere uno dei seguenti:<br /><br /> -   ($1)<br />--$1<br />-$-1<br />-$1:<br />-   (1$)<br />-   -1$<br />--1$<br />-   1$-<br />--1 $<br />--$ 1<br />-$- 1<br />-   $ 1-<br />-$ -1<br />--1$<br />-   ($ 1)<br />-   (1 $)<br /><br /> Questo esempio viene illustrato il segno di dollaro, ma è necessario sostituirlo con l'appropriato **CurrencySymbol** valore al programma effettivo.|  
|**CurrencyThousandSymbol**|Indica il simbolo di caratteri che può essere utilizzato per separare i valori di valuta nel file di testo da migliaia.|  
|**CurrencyDecimalSymbol**|Può essere impostato su qualsiasi carattere singolo che viene usato per separare l'intero dalla parte frazionaria di un importo di valuta.|  
  
> [!NOTE]  
>  Se si omette una voce, viene utilizzato il valore predefinito nel Pannello di controllo di Windows.
