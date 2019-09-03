---
title: Caricatore da riga di comando dwloader-data warehouse paralleli | Microsoft Docs
description: dwloader è uno strumento da riga di comando data warehouse parallelo (PDW) che carica le righe della tabella in blocco in una tabella esistente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 598a244849f843a2b95e6614d4e676a18ba54f61
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212271"
---
# <a name="dwloader-command-line-loader-for-parallel-data-warehouse"></a>Caricatore da riga di comando dwloader per data warehouse paralleli
**dwloader** è uno strumento da riga di comando data warehouse parallelo (PDW) che carica le righe della tabella in blocco in una tabella esistente. Quando si caricano righe, è possibile aggiungere tutte le righe alla fine della tabella (modalità*Append* o *FastAppend*), aggiungere nuove righe e aggiornare le righe esistenti (*modalità Upsert*) o eliminare tutte le righe esistenti prima del caricamento e quindi inserire tutte le righe in una tabella vuota (*modalità*di ricaricamento).  
  
**Processo per il caricamento dei dati**  
  
1.  Preparare i dati di origine.  
  
    Utilizzare il proprio processo ETL per creare i dati di origine che si desidera caricare. I dati di origine devono essere formattati in modo da corrispondere allo schema della tabella di destinazione. Archiviare i dati di origine in uno o più file di testo e copiare i file di testo nella stessa directory del server di caricamento. Per informazioni sul server di caricamento, vedere [acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md)  
  
2.  Preparare le opzioni di caricamento.  
  
    Decidere quali opzioni di caricamento si utilizzeranno. Archiviare le opzioni di caricamento in un file di configurazione. Copiare il file di configurazione in un percorso locale nel server di caricamento. Le opzioni di configurazione di **dwloader** sono descritte in questo argomento.  
  
3.  Preparare le opzioni di errore di caricamento.  
  
    Decidere come si desidera che **dwloader** gestisca le righe che non vengono caricate. Per eseguire il caricamento, **dwloader** carica innanzitutto i dati in una tabella di staging e quindi trasferisce i dati alla tabella di destinazione. Quando il caricatore carica i dati nella tabella di staging, tiene traccia del numero di righe che non vengono caricate. Ad esempio, le righe non formattate correttamente non verranno caricate. Le righe con esito negativo vengono copiate in un file di rifiuto. Per impostazione predefinita, il caricamento viene interrotto dopo il primo rifiuto, a meno che non si specifichi una soglia di rifiuto diversa.  
  
4.  Installare **dwloader**.  
  
    Installare dwloader nel server di caricamento, se non è già installato. 

<!-- MISSING LINK
    See [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](install-dwloader-command-line-loader-sql-server-pdw.md). 
--> 
  
5.  Eseguire **dwloader**.  
  
    Accedere al server di caricamento ed eseguire il file eseguibile **dwloader. exe** con le opzioni della riga di comando appropriate.  
  
6.  Verificare i risultati.  
  
    È possibile controllare il file di righe con esito negativo (specificato con-R) per verificare se le righe non sono state caricate. Se il file è vuoto, tutte le righe sono state caricate correttamente. **dwloader** è transazionale, pertanto se un passaggio ha esito negativo (ad eccezione delle righe rifiutate), verrà eseguito il rollback dello stato iniziale di tutti i passaggi.  
  
<!-- 
![Topic link icon](media/topic-link.gif "Topic_Link")[Syntax Conventions](syntax-conventions-sql-server-pdw.md)  
-->  


## <a name="syntax"></a>Sintassi  
  
```  
dwloader.exe { -h }  
  
dwloader.exe   
    {  
        { -U login_name  -P password  }  
        | -W  
    }  
    [ -f parameter_file ]  
    [ -S target_appliance ]  
    { -T target_database_name . [ schema ] . table_name }   
    { -i source_data_location } [ <source_data_options> ]  
    { -R load_failure_file_name } [ <load_failure_options> ]  
    [ <loading_options> ]  
}  
  
<source_data_options> ::=  
{  
    [ -fh number_header_rows ]  
    [ < variable_length_column_options > | < fixed_width_column_options > ]  
    [ -D { mdy | myd | ymd | ydm | dmy | dym | custom_date_format } ]  
    [ -dt datetime_format_file ]  
}  
  
<variable_length_column_options> ::=  
{  
    [ -e character_encoding ]  
    -r row_delimiter   
    [ -s string_delimiter ]  
    -t field_delimiter   
}  
  
<fixed_width_column_options> ::=  
{  
    -w fixed_width_config_file   
    [ -e character_encoding ]   
    -r row_delimiter   
}  
  
<load_failure_options> ::=  
{  
    [ -rt { value | percentage } ]  
    [ -rv reject_value ]  
    [ -rs reject_sample_value ]  
}  
  
<loading_options> ::=  
{  
    [ -d staging_database_name ]  
    [ -M { append | fastappend | upsert -K merge_column [ ,...n ] | reload } ]  
    [ -b batchsize ]   
    [ -c ]  
    [ -E ]  
    [ -m ]  
    [ -N ]  
    [ -se ]
    [ -l ]   
}  
```  
  
## <a name="arguments"></a>Argomenti  
**-h**  
Visualizza semplici informazioni della guida sull'utilizzo del caricatore. La guida viene visualizzata solo se non vengono specificati altri parametri della riga di comando.  
  
**-U** *login_name*  
Un account di accesso con autenticazione SQL Server valido con le autorizzazioni appropriate per eseguire il caricamento.  
  
**-P** *password*  
Password per un *login_name*di autenticazione SQL Server.  
  
**-W**  
Utilizza l'autenticazione di Windows. (Nessuna *login_name* o *password* obbligatoria). 

<!-- MISSING LINK
For information about configuring Windows Authentication, see [Security - Configure Domain Trusts](security-configure-domain-trusts.md).  
-->
  
**-f** *parameter_file_name*  
Usare un file di parametri, *parameter_file_name*, al posto dei parametri della riga di comando. *parameter_file_name* può contenere qualsiasi parametro della riga di comando tranne *user_name* e *password*. Se viene specificato un parametro nella riga di comando e nel file dei parametri, la riga di comando esegue l'override del parametro file.  
  
Il file di parametri contiene un parametro, senza **-** prefisso, per riga.  
  
Esempi:  
  
`rt=percentage`  
  
`rv=25`  
  
**-S** *target_appliance*  
Specifica il SQL Server PDW Appliance che riceverà i dati caricati.  
  
*Per le connessioni InfiniBand*, *target_appliance* viene specificato come < nome-dispositivo >-SQLCTL01. Per configurare la connessione denominata, vedere [configurare le schede di rete InfiniBand](configure-infiniband-network-adapters.md).  
  
Per le connessioni Ethernet, *target_appliance* è l'indirizzo IP per il cluster del nodo di controllo.  
  
Se omesso, dwloader USA per impostazione predefinita il valore specificato al momento dell'installazione di dwloader. 

<!-- MISSING LINK
For more information about this install option, see [Install dwloader Command-Line Loader](install-dwloader.md).  
-->
  
**-T** *target_database_name.* [*schema*]. *table_name*  
Nome in tre parti della tabella di destinazione.  
  
**-I** *source_data_location*  
Percorso di uno o più file di origine da caricare. Ogni file di origine deve essere un file di testo o un file di testo compresso con gzip. È possibile comprimere un solo file di origine in ogni file gzip.  
  
Per formattare un file di origine:  
  
-   Il file di origine deve essere formattato in base alle opzioni di caricamento.  
  
-   Ogni riga in un file di origine contiene i dati per una riga di tabella. I dati di origine devono corrispondere allo schema della tabella di destinazione. Anche l'ordine delle colonne e i tipi di dati devono corrispondere. Ogni campo della riga rappresenta una colonna della tabella di destinazione.  
  
-   Per impostazione predefinita, i campi sono a lunghezza variabile e separati da un delimitatore. Per specificare il tipo di delimitatore, utilizzare le opzioni della riga di comando < variable_length_column_options >. Per specificare i campi a lunghezza fissa, utilizzare le opzioni della riga di comando < fixed_width_column_options >.  
  
Per specificare il percorso dei dati di origine:  
  
-   Il percorso dei dati di origine può essere un percorso di rete o un percorso locale di una directory nel server di caricamento.  
  
-   Per specificare tutti i file in una directory, immettere il percorso della directory seguito dal carattere jolly *.  Il caricatore non carica i file da alcuna sottodirectory che si trovano nel percorso dei dati di origine. Errori del caricatore quando esiste una directory in un file gzip.  
  
-   Per specificare alcuni dei file in una directory, utilizzare una combinazione di caratteri e il carattere jolly *.  
  
Per caricare più file con un solo comando:  
  
-   Tutti i file devono esistere nella stessa directory.  
  
-   I file devono essere costituiti da tutti i file di testo, da tutti i file gzip o da una combinazione di file di testo e gzip.  
  
-   Nessuno dei file può contenere informazioni di intestazione.  
  
-   Tutti i file devono usare lo stesso tipo di codifica dei caratteri. Vedere l'opzione-e.  
  
-   Tutti i file devono essere caricati nella stessa tabella.  
  
-   Tutti i file verranno concatenati e caricati come se fossero un file e le righe rifiutate verranno indirizzate a un singolo file di rifiuto.  
  
Esempi:  
  
-   -i \\\loadserver\loads\daily\\*. gz  
  
-   -i \\\loadserver\loads\daily\\*.txt  
  
-   -i \\\loadserver\loads\daily\monday. *  
  
-   -i \\\loadserver\loads\daily\monday.txt  
  
-   -i \\\loadserver\loads\daily\\*  
  
**-R** *load_failure_file_name*  
Se si verificano errori di caricamento, **dwloader** archivia la riga che non è stato possibile caricare e l'errore Descrizione le informazioni sull'errore in un file denominato *load_failure_file_name*. Se il file esiste già, dwloader sovrascriverà il file esistente. *load_failure_file_name* viene creato quando si verifica il primo errore. Se tutte le righe vengono caricate correttamente, *load_failure_file_name* non viene creato.  
  
**-FH** *number_header_rows*  
Numero di righe (righe) da ignorare all'inizio di *source_data_file_name*. Il valore predefinito è 0.  
  
<variable_length_column_options>  
Opzioni per un *source_data_file_name* con colonne a lunghezza variabile delimitate da caratteri. Per impostazione predefinita, *source_data_file_name* contiene caratteri ASCII nelle colonne a lunghezza variabile.  
  
Per i file ASCII, i valori NULL vengono rappresentati inserendo delimitatori consecutivi. Ad esempio, in un file delimitato da pipe ("|"), un valore NULL è indicato da "| |". In un file delimitato da virgole, un valore NULL è indicato da ",,". Inoltre, è necessario specificare l'opzione **-E** (--emptyStringAsNull). Per ulteriori informazioni su-E, vedere di seguito.  
  
**-e** *character_encoding*  
Specifica un tipo di codifica dei caratteri per i dati da caricare dal file di dati. Le opzioni sono ASCII (impostazione predefinita), UTF8, UTF16 o UTF16BE, dove UTF16 è little endian e UTF16BE è big endian. Queste opzioni non fanno distinzione tra maiuscole e minuscole.  
  
**-t** *field_delimiter*  
Delimitatore per ogni campo (colonna) nella riga. Il delimitatore di campo è costituito da uno o più caratteri di escape ASCII o valori esadecimali ASCII.  
  
|Name|Carattere escape|Carattere esadecimale|  
|--------|--------------------|-----------------|  
|TAB|\t|0x09|  
|Ritorno a capo (CR)|\r|0x0D|  
|Avanzamento riga (LF)|\n|0x0a|  
|CRLF|\r\n|0x0d0x0a|  
|Virgola|','|0x2c|  
|Virgoletta doppia|\\"|0x22|  
|Virgoletta singola|\\'|0x27|  
  
Per specificare il carattere barra verticale nella riga di comando, racchiuderlo tra virgolette doppie, "|". In questo modo si eviterà un'interpretazione errata da parte del parser della riga di comando. Gli altri caratteri sono racchiusi tra virgolette singole.  
  
Esempi:  
  
-t "|"  
  
-t ' '  
  
-t 0x0a  
  
-t \t  
  
-t '~|~'  
  
**-r** *row_delimiter*  
Delimitatore per ogni riga del file di dati di origine. Il delimitatore di riga è uno o più valori ASCII.  
  
Per specificare un ritorno a capo (CR), un carattere di avanzamento riga (LF) o un carattere di tabulazione come delimitatore, è possibile usare i caratteri di escape (\, \n, \t) o i relativi valori esadecimali (0x, 0D, 09). Per specificare altri caratteri speciali come delimitatori, usare il relativo valore esadecimale.  
  
Esempi di CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Esempi di CR:  
  
-r  
  
-r 0x0D  
  
Esempi di LF:  
  
-r \n  
  
-r 0x0a  
  
Per UNIX è necessario un LF. Per Windows è necessario un CR.  
  
**-s** *string_delimiter*  
Delimitatore per il campo con tipo di dati stringa di un file di input delimitato da testo. Il delimitatore di stringa è uno o più valori ASCII.  Può essere specificato come carattere (ad esempio,-s *) o come valore esadecimale, ad esempio-s 0x22 per le virgolette doppie.  
  
Esempi:  
  
-s *  
  
-s 0x22  
  
< fixed_width_column_options >  
Opzioni per un file di dati di origine con colonne a lunghezza fissa. Per impostazione predefinita, *source_data_file_name* contiene caratteri ASCII nelle colonne a lunghezza variabile.  
  
Le colonne a larghezza fissa non sono supportate quando-e è UTF8.  
  
**-w** *fixed_width_config_file*  
Percorso e nome del file di configurazione che specifica il numero di caratteri in ogni colonna. È necessario specificare ogni campo.  
  
Questo file deve risiedere nel server di caricamento. Il percorso può essere un percorso UNC, relativo o assoluto. Ogni riga in *fixed_width_config_file* contiene il nome di una colonna e il numero di caratteri per la colonna. È presente una riga per ogni colonna, come indicato di seguito, e l'ordine nel file deve corrispondere all'ordine nella tabella di destinazione:  
  
=*num_chars* column_name  
  
=*num_chars* column_name  
  
Esempio di file di configurazione a larghezza fissa:  
  
SalesCode=3  
  
SalesID=10  
  
Righe di esempio in *source_data_file_name*:  
  
230Shirts0056  
  
320Towels1356  
  
Nell'esempio precedente, la prima riga caricata avrà SalesCode =' 230' e SalesID =' Shirts0056'. La seconda riga caricata avrà SalesCode =' 320' e SaleID =' Towels1356'.  
  
Per informazioni su come gestire gli spazi iniziali e finali o la conversione del tipo di dati in modalità a larghezza fissa, vedere [regole di conversione dei tipi di dati per dwloader](dwloader-data-type-conversion-rules.md).  
  
**-e** *character_encoding*  
Specifica un tipo di codifica dei caratteri per i dati da caricare dal file di dati. Le opzioni sono ASCII (impostazione predefinita), UTF8, UTF16 o UTF16BE, dove UTF16 è little endian e UTF16BE è big endian. Queste opzioni non fanno distinzione tra maiuscole e minuscole.  
  
Le colonne a larghezza fissa non sono supportate quando-e è UTF8.  
  
**-r** *row_delimiter*  
Delimitatore per ogni riga del file di dati di origine. Il delimitatore di riga è uno o più valori ASCII.  
  
Per specificare un ritorno a capo (CR), un carattere di avanzamento riga (LF) o un carattere di tabulazione come delimitatore, è possibile usare i caratteri di escape (\, \n, \t) o i relativi valori esadecimali (0x, 0D, 09). Per specificare altri caratteri speciali come delimitatori, usare il relativo valore esadecimale.  
  
Esempi di CR + LF:  
  
-r \r\n  
  
-r 0x0d0x0a  
  
Esempi di CR:  
  
-r  
  
-r 0x0D  
  
Esempi di LF:  
  
-r \n  
  
-r 0x0a  
  
Per UNIX è necessario un LF. Per Windows è necessario un CR.  
  
**-D** { **YMD** | AGM | MDY | MYD |  DMY | DYM | *custom_date_format* }  
Specifica l'ordine di month (m), Day (d) e Year (y) per tutti i campi DateTime nel file di input. L'ordine predefinito è YMD. Per specificare più formati di ordine per lo stesso file di origine, utilizzare l'opzione-DT.  
  
YMD | DMY  
AGM e DMY consentono gli stessi formati di input. Entrambi consentono l'inizio o la fine della data dell'anno. Per i formati di data **AGM** e **DMY** , ad esempio, è possibile che nel file di input sia presente 2013-02-03 o 02-03-2013.  
  
AGM  
È possibile caricare solo l'input formattato come AGM in colonne con tipo di dati DateTime e smalldatetime. Non è possibile caricare valori AGM in una colonna con tipo di dati datetime2, date o DateTimeOffset.  
  
mdy  
MDY consente <month>. <space> <day> <comma> <year>  
  
Esempi di dati di input di MDY per l'1 gennaio 1975:  
  
-   1 gennaio 1975  
  
-   01 gennaio 75  
  
-   Jan/1/75  
  
-   01011975  
  
myd  
Esempi di file di input per il 04 marzo 2010: 03-2010-04, 3/2010/4  
  
dym  
Esempi di file di input per il 04 marzo 2010: 04-2010-03, 4/2010/3  
  
*custom_date_format*  
*custom_date_format* è un formato di data personalizzato (ad esempio, mm/gg/aaaa) ed è incluso solo per compatibilità con le versioni precedenti. dwloader non impone il formato di data personalizzato. Al contrario, quando si specifica un formato di data personalizzato, **dwloader** lo convertirà nell'impostazione corrispondente di ymd, AGM, MDY, MYD, DYM o DMY.  
  
Se, ad esempio, si specifica-D MM/gg/aaaa, dwloader prevede che tutti gli input di data vengano ordinati prima con il mese, quindi il giorno e infine l'anno (MDY). Non applica due mesi, i giorni a 2 cifre e gli anni a 4 cifre come specificato dal formato di data personalizzato. Di seguito sono riportati alcuni esempi dei modi in cui le date possono essere formattate nel file di input quando il formato della data è-D MM/gg/aaaa: 01/02/2013, Jan. 02.2013, 1/2/2013  
  
Per informazioni più complete sulla formattazione, vedere [regole di conversione dei tipi di dati per dwloader](dwloader-data-type-conversion-rules.md).  
  
**-dt** *datetime_format_file*  
Ogni formato DateTime viene specificato in un file denominato *datetime_format_file*. A differenza dei parametri della riga di comando, i parametri del file che includono spazi non devono essere racchiusi tra virgolette doppie. Non è possibile modificare il formato DateTime durante il caricamento dei dati. Il file di dati di origine e la colonna corrispondente nella tabella di destinazione devono avere lo stesso formato.  
  
Ogni riga contiene il nome di una colonna nella tabella di destinazione e il relativo formato DateTime.  
  
Esempi:  
  
`LastReceiptDate=ymd`  
  
`ModifiedDate=dym`  
  
**-d** *staging_database_name*  
Nome del database che conterrà la tabella di staging. Il valore predefinito è il database specificato con l'opzione-T, ovvero il database per la tabella di destinazione. Per ulteriori informazioni sull'utilizzo di un database di gestione temporanea, vedere [creare il database di gestione temporanea](staging-database.md).  
  
**-M** *load_mode_option*  
Specifica se accodare, Upsert o ricaricare i dati. La modalità predefinita è Append.  
  
append  
Il caricatore inserisce le righe alla fine delle righe esistenti nella tabella di destinazione.  
  
FastAppend  
Il caricatore inserisce direttamente le righe, senza usare una tabella temporanea, alla fine delle righe esistenti nella tabella di destinazione. FastAppend richiede l'opzione multitransaction (-m). Impossibile specificare un database di gestione temporanea quando si utilizza FastAppend. Non viene eseguito alcun rollback con FastAppend, il che significa che il ripristino da un caricamento non riuscito o interrotto deve essere gestito dal proprio processo di caricamento.  
  
Upsert **-K**  *merge_column* [,... *n* ]  
Il caricatore utilizza l'istruzione MERGE SQL Server per aggiornare le righe esistenti e inserire nuove righe.  
  
L'opzione-K specifica la colonna o le colonne su cui basare il merge. Queste colonne formano una chiave di merge, che dovrebbe rappresentare una riga univoca. Se la chiave di Unione esiste nella tabella di destinazione, la riga viene aggiornata. Se la chiave di merge non esiste nella tabella di destinazione, viene aggiunta la riga.  
  
Per le tabelle con distribuzione hash, la chiave di merge deve essere o includere la colonna di distribuzione.  
  
Per le tabelle replicate, la chiave di merge è la combinazione di una o più colonne. Queste colonne vengono specificate in base alle esigenze dell'applicazione.  
  
Più colonne devono essere separate da virgole senza spazi oppure separate da virgole con spazi e racchiuse tra virgolette singole.  
  
Se due righe della tabella di origine hanno valori di chiave di unione corrispondenti, le rispettive righe devono essere identiche.  
  
ricaricare  
Il caricatore tronca la tabella di destinazione prima di inserire i dati di origine.  
  
**-b** *BatchSize*  
Consigliato solo per l'uso da parte di supporto tecnico Microsoft, *BatchSize* è la dimensione del batch SQL Server per la copia bulk eseguita da DMS nelle istanze di SQL Server nei nodi di calcolo.  Quando si specifica *BatchSize* , SQL Server PDW eseguirà l'override della dimensione del caricamento batch calcolata dinamicamente per ogni carico.  
  
A partire da SQL Server 2012 PDW, il nodo di controllo calcola dinamicamente le dimensioni del batch per ogni carico per impostazione predefinita. Questo calcolo automatico si basa su diversi parametri, ad esempio le dimensioni della memoria, il tipo di tabella di destinazione, lo schema della tabella di destinazione, il tipo di carico, le dimensioni del file e la classe di risorse dell'utente.  
  
Se, ad esempio, la modalità di caricamento è FASTAPPEND e la tabella include un indice columnstore cluster, per impostazione predefinita SQL Server PDW tenterà di usare una dimensione di batch pari a 1.048.576 in modo che RowGroups venga chiuso e venga caricato direttamente nel columnstore senza passare attraverso il Archivio Delta. Se la memoria non consente le dimensioni del batch 1.048.576, dwloader sceglierà un BatchSize più piccolo.  
  
Se il tipo di carico è FASTAPPEND, *BatchSize* si applica al caricamento dei dati nella tabella; in caso contrario *BatchSize* si applica al caricamento dei dati nella tabella di staging.  
  
<reject_options>  
Specifica le opzioni per determinare il numero di errori di caricamento consentiti dal caricatore. Se gli errori di caricamento superano la soglia, il caricatore si arresterà e non eseguirà il commit di alcuna riga.  
  
**-RT** { **value** | percentuale}  
Specifica se-*reject_value* nell'opzione **-RV** *reject_value* è un numero letterale di righe (valore) o un tasso di errore (percentuale). Il valore predefinito è value.  
  
L'opzione percentuale è un calcolo in tempo reale che si verifica a intervalli in base all'opzione-RS.  
  
Se, ad esempio, il caricatore tenta di caricare 100 righe e 25 ha esito negativo e 75 ha esito positivo, la percentuale di errori è pari al 25%.  
  
**-RV** *reject_value*  
Specifica il numero o la percentuale di rifiuti di riga da consentire prima di arrestare il carico. L'opzione **-RT** determina se *reject_value* fa riferimento al numero di righe o alla percentuale di righe.  
  
Il valore predefinito di *reject_value* è 0.  
  
Quando viene usato con il valore-RT, il caricatore interrompe il caricamento quando il numero di righe rifiutate supera reject_value.  
  
Quando si usa con la percentuale-RT, il caricatore calcola la percentuale a intervalli (opzione-RS). Pertanto, la percentuale di righe con esito negativo può superare *reject_value*.  
  
**-RS** *reject_sample_size*  
Utilizzato con l' `-rt percentage` opzione per specificare i controlli della percentuale incrementale. Se, ad esempio, reject_sample_size è 1000, il caricatore calcolerà la percentuale di righe con esito negativo dopo aver tentato di caricare 1000 righe. Consente di ricalcolare la percentuale di righe con esito negativo dopo il tentativo di caricamento di ogni 1000 righe aggiuntive.  
  
**-c**  
Rimuove gli spazi vuoti dal lato sinistro e destro dei campi char, nchar, varchar e nvarchar. Converte in una stringa vuota ogni campo che contiene solo spazi vuoti.  
  
Esempi:  
  
'' viene troncato in ''  
  
' ABC ' viene troncato in ' ABC '  
  
Quando si usa-c con-E, l'operazione-E si verifica per prima. I campi che contengono solo spazi vuoti vengono convertiti in una stringa vuota e non NULL.  
  
**-E**  
Converte le stringhe vuote in NULL. Per impostazione predefinita, non è possibile eseguire queste conversioni.  
  
**-m**  
Utilizzare la modalità multitransazione per la seconda fase del caricamento; Quando si caricano dati dalla tabella di staging in una tabella distribuita.  
  
Con **-m**, SQL Server PDW esegue ed esegue il commit dei caricamenti in parallelo. Questa operazione viene eseguita molto più velocemente rispetto alla modalità di caricamento predefinita, ma non è indipendente dalle transazioni.  
  
Senza **-m**, il SQL Server PDW esegue e commit in modo seriale tra le distribuzioni all'interno di ogni nodo di calcolo e simultaneamente tra i nodi di calcolo. Questo metodo è più lento della modalità multitransazione, ma è indipendente dalle transazioni.  
  
**-m** è facoltativo per *Append*, *reload*e *Upsert*.  
  
**-m** è obbligatorio per FastAppend.  
  
**-m** non può essere usato con le tabelle replicate.  
  
**-m** si applica solo alla seconda fase di caricamento. Non si applica alla prima fase di caricamento. caricamento dei dati nella tabella di staging.  
  
Non viene eseguito alcun rollback con la modalità multitransazione, il che significa che il ripristino da un carico non riuscito o interrotto deve essere gestito dal proprio processo di caricamento.  
  
È consigliabile usare **-m** solo quando si esegue il caricamento in una tabella vuota, in modo che sia possibile eseguire il ripristino senza perdita di dati. Per eseguire il ripristino a seguito di un errore di caricamento: eliminare la tabella di destinazione, risolvere il problema di carico, ricreare la tabella di destinazione e ripetere il caricamento.  
  
**-N**  
Verificare che l'appliance di destinazione disponga di un certificato di SQL Server PDW valido da un'autorità attendibile. Questa operazione consente di garantire che i dati non vengano dirottati da un utente malintenzionato e inviati a una posizione non autorizzata. Il certificato deve essere già installato nell'appliance. L'unico modo supportato per installare il certificato è l'amministratore del dispositivo a installarlo utilizzando lo strumento Configuration Manager. Se non si è certi che nel dispositivo sia installato un certificato attendibile, rivolgersi all'amministratore del dispositivo.  
  
**-se**  
Ignora il caricamento di file vuoti. Questa operazione ignora anche la decompressione di file gzip vuoti.

**-l**  
Disponibile con l'aggiornamento di CU 7.4, specifica la lunghezza massima della riga (in byte) che può essere caricata. I valori validi sono numeri interi compresi tra 32768 e 33554432. Utilizzare solo quando necessario per caricare righe di grandi dimensioni (maggiori di 32 KB), in quanto verrà allocata una maggiore quantità di memoria nel client e nel server.
  
## <a name="return-code-values"></a>Valori restituiti  
0 (esito positivo) o altro valore integer (esito negativo)  
  
In una finestra di comando o in un file `errorlevel` batch usare per visualizzare il codice restituito. Esempio:  
  
```  
dwloader  
echo ReturnCode=%errorlevel%  
if not %errorlevel%==0 echo Fail  
if %errorlevel%==0 echo Success  
```  
  
Quando si usa PowerShell, `$LastExitCode`usare.  
  
## <a name="permissions"></a>Permissions  
È richiesta l'autorizzazione LOAD e le autorizzazioni applicabili (INSERT, UPDATE, DELETE) nella tabella di destinazione. È richiesta l'autorizzazione CREATE (per la creazione di una tabella temporanea) nel database di gestione temporanea. Se non viene utilizzato un database di gestione temporanea, è necessario disporre dell'autorizzazione CREATE nel database di destinazione. 

<!-- MISSING LINK
For more information, see [Grant permissions to load data](grant-permissions-to-load-data.md).  
-->
  
## <a name="general-remarks"></a>Osservazioni generali  
Per informazioni sulle conversioni dei tipi di dati durante il caricamento con dwloader, vedere [regole di conversione dei tipi di dati per dwloader](dwloader-data-type-conversion-rules.md).  
  
Se un parametro include uno o più spazi, racchiuderlo tra virgolette doppie.  
  
È necessario eseguire il caricatore dal percorso di installazione. Il file eseguibile dwloader è preinstallato con l'appliance e si trova nella directory C:\Programmi\Microsoft SQL Server Data Warehouse\DWLoader.  
  
È possibile eseguire l'override di un parametro specificato nel file di parametri (opzione-f) specificandone il parametro come parametro della riga di comando.  
  
È possibile eseguire contemporaneamente più istanze del caricatore. Il numero massimo di istanze del caricatore è preconfigurato e non può essere modificato. 

<!-- MISSING LINK
For the maximum number of loads per appliance, see [Minimum and Maximum Values](minimum-maximum-values.md)  
-->
  
I dati caricati potrebbero richiedere più o meno spazio sul dispositivo rispetto al percorso di origine. Per stimare l'utilizzo del disco, è possibile eseguire importazioni di test con subset di dati.  
  
Anche se **dwloader** è un processo di transazione e viene eseguito correttamente il rollback in caso di errore, non è possibile eseguirne il rollback una volta completato il caricamento bulk. Per annullare un processo **dwloader** attivo, digitare CTRL + C.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
La dimensione totale di tutti i caricamenti che si verificano simultaneamente deve essere minore di LOG_SIZE per il database ed è consigliabile che le dimensioni totali di tutti i carichi simultanei siano inferiori al 50% del LOG_SIZE. Per ottenere questa limitazione delle dimensioni, è possibile suddividere i carichi di grandi dimensioni in più batch. Per ulteriori informazioni su LOG_SIZE, vedere [create database](../t-sql/statements/create-database-parallel-data-warehouse.md)  
  
Quando si caricano più file con un solo comando Load, tutte le righe rifiutate vengono scritte nello stesso file Reject. Il file di rifiuto non indica il file di input contenente ogni riga rifiutata.  
  
La stringa vuota non deve essere utilizzata come delimitatore. Quando una stringa vuota viene utilizzata come delimitatore di riga, il caricamento avrà esito negativo. Se usato come delimitatore di colonna, il carico ignora il delimitatore e continua a usare il valore predefinito "|" come delimitatore di colonna. Se utilizzato come delimitatore di stringa, la stringa vuota viene ignorata e viene applicato il comportamento predefinito.  
  
## <a name="locking-behavior"></a>Comportamento di blocco  
il comportamento di blocco **dwloader** varia a seconda del *load_mode_option*.  
  
-   **Append** -Append è l'opzione consigliata e più comune. Accoda carica i dati in una tabella di staging. Il blocco viene descritto in dettaglio di seguito.  
  
-   **Fast Append** : Fast: accoda i caricamenti direttamente nella tabella finale che accetta un blocco di tabella ExclusiveUpdate ed è l'unica modalità che non usa una tabella di staging.  
  
-   **ricarica** : ricarica carica i dati in una tabella di staging e richiede un blocco esclusivo sia nella tabella di staging che nella tabella finale. Il ricaricamento non è consigliato per le operazioni simultanee.  
  
-   **Upsert** -Upsert carica i dati in una tabella di staging, quindi esegue un'operazione di Unione dalla tabella di staging alla tabella finale. Upsert non richiede blocchi esclusivi sulla tabella finale. Quando si usa Upsert, le prestazioni possono variare. Testare il comportamento nell'ambiente in uso.  
  
### <a name="locking-behavior"></a>Comportamento di blocco  
**Blocco in modalità Append**  
  
L'accodamento può essere eseguito in modalità transazionale (usando l'argomento-m) ma non è indipendente dalle transazioni. Pertanto, l'accodamento deve essere usato come operazione transazionale (senza usare l'argomento-m). Sfortunatamente, durante l'operazione di inserimento-selezione finale, la modalità transazionale è attualmente circa sei volte più lenta rispetto alla modalità transazionale.  
  
La modalità di accodamento consente di caricare i dati in due fasi. La fase 1 carica i dati dal file di origine in una tabella di staging simultaneamente (può verificarsi la frammentazione). La fase 2 carica i dati dalla tabella di staging alla tabella finale. La seconda fase esegue un'istruzione **Insert into... Operazione SELECT WITH (TABLOCK)** . La tabella seguente illustra il comportamento di blocco nella tabella finale e il comportamento di registrazione quando si usa la modalità Append:  
  
|Tipo di tabella|Più transazioni<br />Modalità (-m)|Tabella vuota|Concorrenza supportata|Registrazione|  
|--------------|-----------------------------------|------------------|-------------------------|-----------|  
|Heap|Yes|Yes|Yes|Minime|  
|Heap|Yes|No|Yes|Minime|  
|Heap|No|Sì|No|Minime|  
|Heap|No|No|No|Minime|  
|Cl|Yes|Sì|No|Minime|  
|Cl|Yes|No|Yes|Full|  
|Cl|No|Sì|No|Minime|  
|Cl|No|No|Yes|Full|  
  
La tabella precedente Mostra **dwloader** usando il caricamento in modalità Accodamento in un heap o una tabella dell'indice cluster (ci), con o senza il flag transazionale, e il caricamento in una tabella vuota o in una tabella non vuota. Nella tabella viene visualizzato il comportamento di blocco e di registrazione di ogni combinazione di carico. Ad esempio, la fase di caricamento (2a) con la modalità di Accodamento in un indice cluster senza modalità transazionale e in una tabella vuota creerà un blocco esclusivo sulla tabella e la registrazione sarà minima. Questo significa che un cliente non sarà in grado di caricare (2a) fase e query simultaneamente in una tabella vuota. Tuttavia, quando si carica con la stessa configurazione in una tabella non vuota, PDW non emette un blocco esclusivo sulla tabella e la concorrenza è possibile. Sfortunatamente, la registrazione completa si verifica, rallentando il processo.  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-simple-dwloader-example"></a>R. Esempio di dwloader semplice  
L'esempio seguente mostra l'avvio del **caricatore** con solo le opzioni obbligatorie selezionate. Altre opzioni sono tratte dal file di configurazione globale, *loadparamfile. txt*.  
  
Esempio di utilizzo dell'autenticazione SQL Server.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -U mylogin -P 123jkl -f /configfiles/loadparamfile.txt  
```  
  
Lo stesso esempio che usa l'autenticazione di Windows.  
  
```  
--Load over Ethernet  
dwloader.exe -S 10.192.63.148 -W -f /configfiles/loadparamfile.txt  
  
--Load over InfiniBand to appliance named MyPDW  
dwloader.exe -S MyPDW-SQLCTL01 -W -f /configfiles/loadparamfile.txt  
```  
  
Esempio di utilizzo di argomenti per un file di origine e un file degli errori.  
  
```  
--Load over Ethernet  
dwloader.exe -U mylogin -P 123jkl -S 10.192.63.148  -i C:\SQLData\AWDimEmployees.csv -T AdventureWorksPDW2012.dbo.DimEmployees -R C:\SQLData\LoadErrors  
```  
  
### <a name="b-load-data-into-an-adventureworks-table"></a>B. Caricare i dati in una tabella AdventureWorks  
L'esempio seguente fa parte di uno script batch che carica i dati in **AdventureWorksPDW2012**.  Per visualizzare lo script completo, aprire il file aw_create. bat fornito con il pacchetto di installazione **AdventureWorksPDW2012** . 

<!-- Missing link
For more information, see [Install AdventureWorksPDW2012](install-adventureworkspdw2012.md).  
-->

Il frammento di script seguente usa dwloader per caricare i dati nelle tabelle DimAccount e DimCurrency. Questo script usa un indirizzo Ethernet. Se utilizza InfiniBand, il server *< >* `-SQLCTL01`appliance_name.  
  
```  
set server=10.193.63.134  
set user=<MyUser>  
set password=<MyPassword>  
  
set schema=AdventureWorksPDW2012.dbo  
set load="C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe"  
set mode=reload  
  
--Loads data into the AdventureWorksPDW2012.dbo.DimAccount table  
--Source data is stored in the file DimAccount.txt,   
--which is in the current directory.  
  
set t1=DimAccount  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%   
  
--Loads data from the DimCurrency.txt file into  
--AdventureWorksPDW2012.dbo.DimCurrency  
set t1=DimCurrency  
%load% -S %server% -E -M %mode% -e Utf16 -i .\%t1%.txt -T %schema%.%t1% -R %t1%.bad -t "|" -r \r\n -U %user% -P %password%  
```  
  
Di seguito è riportata la DDL per la tabella DimAccount.  
  
```  
CREATE TABLE DimAccount(  
AccountKey int NOT NULL,  
ParentAccountKey int,  
AccountCodeAlternateKey int,  
ParentAccountCodeAlternateKey int,  
AccountDescription nvarchar(50),  
AccountType nvarchar(50),  
Operator nvarchar(50),  
CustomMembers nvarchar(300),  
ValueType nvarchar(50),  
CustomMemberOptions nvarchar(200))  
with (CLUSTERED INDEX(AccountKey),  
DISTRIBUTION = REPLICATE);  
```  
  
Di seguito è riportato un esempio del file di dati, DimAccount. txt, che contiene i dati da caricare nella tabella DimAccount.  
  
```  
--Sample of data in the DimAccount.txt load file.  
  
1||1||Balance Sheet||~||Currency|  
2|1|10|1|Assets|Assets|+||Currency|  
3|2|110|10|Current Assets|Assets|+||Currency|  
4|3|1110|110|Cash|Assets|+||Currency|  
5|3|1120|110|Receivables|Assets|+||Currency|  
6|5|1130|1120|Trade Receivables|Assets|+||Currency|  
7|5|1140|1120|Other Receivables|Assets|+||Currency|  
8|3|1150|110|Allowance for Bad Debt|Assets|+||Currency|  
9|3|1160|110|Inventory|Assets|+||Currency|  
10|9|1162|1160|Raw Materials|Assets|+||Currency|  
11|9|1164|1160|Work in Process|Assets|+||Currency|  
12|9|1166|1160|Finished Goods|Assets|+||Currency|  
13|3|1170|110|Deferred Taxes|Assets|+||Currency|  
```  
  
### <a name="c-load-data-from-the-command-line"></a>C. Caricare i dati dalla riga di comando  
Lo script nell'esempio B può essere sostituito immettendo tutti i parametri nella riga di comando, come illustrato nell'esempio seguente.  
  
```  
C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe -S <Control node IP> -E -M reload -e UTF16 -i .\DimAccount.txt -T AdventureWorksPDW2012.dbo.DimAccount -R DimAccount.bad -t "|" -r \r\n -U <login> -P <password>  
```  
  
Descrizione dei parametri della riga di comando:  
  
-   *C:\programmi\microsoft SQL Server Parallel Data Warehouse\100\dwloader.exe* è il percorso di installazione di dwloader. exe.  
  
-   *-S* è seguito dall'indirizzo IP del nodo di controllo.  
  
-   *-E* specifica di caricare stringhe vuote come null.  
  
-   *-M ricarica* specifica di troncare la tabella di destinazione prima di inserire i dati di origine.  
  
-   *-e UTF16* indica che il file di origine usa il tipo di codifica dei caratteri little endian.  
  
-   *-i .\DimAccount.txt* specifica che i dati si trovino in un file denominato DimAccount. txt, presente nella directory corrente.  
  
-   *-T AdventureWorksPDW2012. dbo. DimAccount* specifica il nome in tre parti della tabella per la ricezione dei dati.  
  
-   *-R DimAccount. Bad* specifica che le righe che non vengono caricate verranno scritte in un file denominato DimAccount. Bad.  
  
-   *-t "|"* indica che i campi nel file di input, DimAccount. txt, sono separati dal carattere barra verticale.  
  
-   *-r \r\n* specifica che ogni riga in DimAccount. txt termina con un ritorno a capo e un carattere di avanzamento riga.  
  
-   *-U < login_name >-P <password>*  specifica l'account di accesso e la password per l'account di accesso che dispone delle autorizzazioni per eseguire il caricamento.  
  

<!-- MISSING LINK

## See Also  
[Common Metadata Query Examples](metadata-query-examples.md)  

-->
  
