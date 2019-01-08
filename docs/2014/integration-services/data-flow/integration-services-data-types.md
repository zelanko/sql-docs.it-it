---
title: Tipi di dati di Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5fc0a802cc3d266cc96d8deaaeeda39056508062
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377841"
---
# <a name="integration-services-data-types"></a>Tipi di dati di Integration Services
  Quando i dati entrano in un flusso di dati di un pacchetto, l'origine che estrae i dati li converte in un tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Ai dati numerici viene assegnato un tipo di dati numeric, ai dati stringa viene assegnato un tipo di dati character e alle date viene assegnato un tipo di dati date. Agli altri dati, ad esempio GUID e BLOB (Binary Large Object), vengono assegnati i tipi dai dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] appropriati. Se i dati sono di un tipo non convertibile in un tipo di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , verrà generato un errore.  
  
 Alcuni componenti flusso di dati consentono di eseguire la conversione tra i tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i tipi di dati gestiti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Per altre informazioni sul mapping tra [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e tipi di dati gestiti, vedere [Utilizzo di tipi di dati nel flusso di dati](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
 La tabella seguente elenca i tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Alcuni dei tipi di dati nella tabella dispongono di informazioni sulla precisione e sulla scala. Per altre informazioni su precisione e scala, vedere [Precisione, scala e lunghezza &#40;Transact-SQL&#41;](/sql/t-sql/data-types/precision-scale-and-length-transact-sql).  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|DT_BOOL|Valore booleano.|  
|DT_BYTES|Valore di dati binari. di lunghezza variabile, fino a un massimo di 8000 byte.|  
|DT_CY|Valore di valuta. Questo tipo di dati è un intero con segno a 8 byte con scala 4 e precisione massima di 19 cifre.|  
|DT_DATE|Struttura di data che include anno, mese, giorno, ora, minuti, secondi e secondi frazionari.  I secondi frazionari hanno una scala fissa di 7 cifre.<br /><br /> Il tipo di dati DT_DATE viene implementato utilizzando un numero a virgola mobile a 8 byte. I giorni vengono rappresentati tramite incrementi costituiti da numeri interi, a partire dal 30 dicembre 1899, e la mezzanotte corrisponde all'ora zero. I valori di ora sono rappresentati dal valore assoluto della parte frazionaria del numero. Poiché tuttavia i valori a virgola mobile non consentono di rappresentare tutti i numeri reali, l'intervallo di date che è possibile rappresentare utilizzando il tipo di dati DT_DATE è limitato.<br /><br /> Il tipo di dati DT_DBTIMESTAMP, invece, è rappresentato da una struttura che internamente include campi distinti per anno, mese, giorno, ore, minuti, secondi e millisecondi. Questo tipo di dati può essere utilizzato per rappresentare intervalli di date più ampi.|  
|DT_DBDATE|Struttura di data che include anno, mese e giorno.|  
|DT_DBTIME|Struttura di ora che include ora, minuto e secondo.|  
|DT_DBTIME2|Struttura di ora che include ora, minuti, secondi e secondi frazionari. I secondi frazionari hanno una scala massima di 7 cifre.|  
|DT_DBTIMESTAMP|Struttura di timestamp che include anno, mese, giorno, ora, minuti, secondi e secondi frazionari. I secondi frazionari hanno una scala massima di 3 cifre.|  
|DT_DBTIMESTAMP2|Struttura di timestamp che include anno, mese, giorno, ora, minuti, secondi e secondi frazionari. I secondi frazionari hanno una scala massima di 7 cifre.|  
|DT_DBTIMESTAMPOFFSET|Struttura di timestamp che include anno, mese, giorno, ora, minuti, secondi e secondi frazionari. I secondi frazionari hanno una scala massima di 7 cifre.<br /><br /> A differenza dei tipi di dati DT_DBTIMESTAMP e DT_DBTIMESTAMP2, il tipo di dati DT_DBTIMESTAMPOFFSET include la differenza di fuso orario. Questa differenza specifica il numero di ore e minuti di scostamento rispetto all'ora UTC (Coordinated Universal Time). La differenza di fuso orario viene utilizzata dal sistema per calcolare l'ora locale.<br /><br /> La differenza di fuso orario deve includere un segno, più o meno, per indicare se il relativo valore deve essere aggiunto all'ora UTC o sottratto da essa. Il numero valido per la differenza di ore è compreso tra -14 e +14. Il segno per la differenza di minuti dipende da quello per la differenza di ore:<br /><br /> Se il segno per la differenza di ore è negativo, la differenza di minuti deve essere un valore negativo o zero.<br /><br /> Se il segno per la differenza di ore è positivo, la differenza di minuti deve essere un valore positivo o zero.<br /><br /> Se il segno per la differenza di ore è zero, la differenza di minuti può essere qualsiasi valore da 0,59 negativo a 0,59 positivo.|  
|DT_DECIMAL|Valore numerico esatto con scala e precisione fisse. Questo tipo di dati è un intero senza segno a 12 byte, con segno a parte, scala da 0 a 28 e precisione massima 29.|  
|DT_FILETIME|Valore a 64 bit che rappresenta il numero di intervalli di 100 nanosecondi trascorsi dal 1 gennaio 1601. I secondi frazionari hanno una scala massima di 3 cifre.|  
|DT_GUID|Identificatore univoco globale (GUID, Globally Unique Identifier).|  
|DT_I1|Intero con segno a 1 byte.|  
|DT_I2|Intero con segno a 2 byte.|  
|DT_I4|Intero con segno a 4 byte.|  
|DT_I8|Intero con segno a 8 byte.|  
|DT_NUMERIC|Valore numerico esatto con scala e precisione fisse. Questo tipo di dati è un intero senza segno a 16 byte, con segno a parte, scala da 0 a 38 e precisione massima 38.|  
|DT_R4|Valore a virgola mobile con precisione singola.|  
|DT_R8|Valore a virgola mobile con precisione doppia.|  
|DT_STR|Stringa di caratteri [!INCLUDE[vcpransi](../../../includes/vcpransi-md.md)]/MBCS con terminazione Null e lunghezza massima di 8000 caratteri. Se un valore di una colonna contiene ulteriori terminatori Null, la stringa verrà troncata in corrispondenza del primo carattere Null.|  
|DT_UI1|Intero senza segno a 1 byte.|  
|DT_UI2|Intero senza segno a 2 byte.|  
|DT_UI4|Intero senza segno a 4 byte.|  
|DT_UI8|Intero senza segno a 8 byte.|  
|DT_WSTR|Stringa di caratteri Unicode con terminazione Null e lunghezza massima di 4000 caratteri. Se un valore di una colonna contiene ulteriori terminatori Null, la stringa verrà troncata in corrispondenza del primo carattere Null.|  
|DT_IMAGE|Un valore binario con dimensioni massime di 2<sup>31</sup>-1 (2.147.483.647) byte. .|  
|DT_NTEXT|Stringa di caratteri Unicode con lunghezza massima di 2<sup>30</sup> - 1 (1.073.741.823) caratteri.|  
|DT_TEXT|Un' [!INCLUDE[vcpransi](../../../includes/vcpransi-md.md)]/MBCS carattere stringa con lunghezza massima pari a 2<sup>31</sup>-1 (2.147.483.647) caratteri.|  
  
## <a name="conversion-of-data-types"></a>Conversione di tipi di dati  
 Se i dati in una colonna non richiedono l'intera larghezza allocata dal tipo di dati di origine, sarà possibile modificare il tipo di dati della colonna. Riducendo il più possibile la larghezza delle singole righe di dati è possibile ottimizzare le prestazioni delle operazioni di trasferimento dei dati, perché minore è la larghezza della riga, più rapido sarà lo spostamento dei dati dall'origine alla destinazione.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include un set completo di tipi di dati numerici ed è pertanto possibile scegliere quello più appropriato alle dimensioni dei dati. Se ad esempio i valori di una colonna con tipo di dati DT_UI8 sono sempre numeri interi da 0 a 3000, sarà possibile modificare il tipo di dati in DT_UI2. Analogamente, se una colonna con tipo di dati DT_CY può soddisfare i requisiti di dati del pacchetto anche utilizzando un tipo di dati Integer, sarà possibile modificare il tipo di dati in DT_I4.  
  
 Per modificare il tipo di dati di una colonna, procedere nel modo seguente:  
  
-   Utilizzare un'espressione per convertire in modo implicito i tipi di dati. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../expressions/integration-services-data-types-in-expressions.md), [Tipi di dati nelle espressioni di Integration Services](../expressions/integration-services-data-types-in-expressions.md), e [Espressioni di Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md).  
  
-   Utilizzare l'operatore cast per convertire i tipi di dati. Per altre informazioni, vedere [Cast &#40;espressione SSIS&#41;](../expressions/cast-ssis-expression.md).  
  
-   Utilizzare la trasformazione Conversione dati per eseguire il cast del tipo di dati di una colonna a un tipo di dati diverso. Per altre informazioni, vedere [trasformazione Conversione dati](transformations/data-conversion-transformation.md).  
  
-   Utilizzare la trasformazione Colonna derivata per creare una copia di una colonna con un tipo di dati diverso rispetto alla colonna originale. Per altre informazioni, vedere [trasformazione Colonna derivata](transformations/derived-column-transformation.md).  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>Conversione tra stringhe e tipi di dati di data e ora  
 Nella tabella seguente sono elencati i risultati di esecuzione del cast o di conversione tra stringhe e tipi di dati di data e ora:  
  
-   Quando si utilizza l'operatore cast o la trasformazione Conversione dati, i dati di tipo data e ora vengono convertiti nel formato stringa corrispondente. Ad esempio, il tipo di data DT_DBTIME sarà convertito in una stringa nel formato "hh:mm:ss".  
  
-   Quando si desidera eseguire la conversione da una stringa a un tipo di dati di data oppure ora, la stringa deve utilizzare il formato stringa che corrisponde al tipo di dati di data oppure ora appropriato. Ad esempio, per convertire correttamente alcune stringhe di data nel tipo di dati DT_DBDATE, è necessario che le stringhe siano nel formato "aaaa-mm-gg".  
  
    |Tipo di dati|Formato stringa|  
    |---------------|-------------------|  
    |DT_DBDATE|aaaa-mm-gg|  
    |DT_FILETIME|aaaa-mm-gg hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|aaaa-mm-gg hh.mm.ss[.fff]|  
    |DT_DBTIMESTAMP2|aaaa-mm-gg hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|aaaa-mm-gg hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 Nel formato per DT_FILETIME e DT_DBTIMESTAMP, fff è un valore compreso tra 0 e 999 che rappresenta i secondi frazionari.  
  
 Nel formato di data per DT_DBTIMESTAMP2, DT_DBTIME2 e DT_DBTIMESTAMPOFFSET, fffffff è un valore compreso tra 0 e 9999999 che rappresenta i secondi frazionari.  
  
 Il formato di data per DT_DBTIMESTAMPOFFSET include anche un elemento relativo al fuso orario. Tra l'elemento relativo all'ora e quello relativo al fuso orario è presente uno spazio.  
  
### <a name="converting-datetime-data-types"></a>Conversione dei tipi di dati di data e ora  
 È possibile modificare il tipo di dati di una colonna contenente informazioni di data e ora in modo da estrarre la parte di dati relativa alla data o all'ora. Nella tabella seguente sono illustrati i risultati della conversione da un tipo di dati di data e ora a un altro tipo di dati di data e ora.  
  
#### <a name="converting-from-dtfiletime"></a>Conversione da DT_FILETIME  
  
|Conversione di DT_FILETIME in|Risultato|  
|-----------------------------|------------|  
|DT_FILETIME|Nessuna modifica.|  
|DT_DATE|Conversione del tipo di dati.|  
|DT_DBDATE|Rimozione del valore di ora.|  
|DT_DBTIME|Rimozione del valore di data.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre frazionarie che il tipo di dati DT_DBTIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIME2|Rimozione del valore di data rappresentato dal tipo di dati DT_FILETIME.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Conversione del tipo di dati.|  
|DT_DBTIMESTAMP2|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Impostazione del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET su zero.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMPOFFSET può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdate"></a>Conversione da DT_DATE  
  
|Conversione di DT_DATE in|Risultato|  
|-------------------------|------------|  
|DT_FILETIME|Conversione del tipo di dati.|  
|DT_DATE|Nessuna modifica.|  
|DT_DBDATE|Rimozione del valore di ora rappresentato dal tipo di dati DT_DATA.|  
|DT_DBTIME|Rimozione del valore di data rappresentato dal tipo di dati DT_DATE.|  
|DT_DBTIME2|Rimozione del valore di data rappresentato dal tipo di dati DT_DATE.|  
|DT_DBTIMESTAMP|Conversione del tipo di dati.|  
|DT_DBTIMESTAMP2|Conversione del tipo di dati.|  
|DT_DBTIMESTAMPOFFSET|Impostazione del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET su zero.|  
  
#### <a name="converting-from-dtdbdate"></a>Conversione da DT_DBDATE  
  
|Conversione di DT_DBDATE in|Risultato|  
|---------------------------|------------|  
|DT_FILETIME|Impostazione dei campi dell'ora nel tipo di dati DT_FILETIME su zero.|  
|DT_DATE|Impostazione dei campi dell'ora nel tipo di dati DT_DATE su zero.|  
|DT_DBDATE|Nessuna modifica.|  
|DT_DBTIME|Impostazione dei campi dell'ora nel tipo di dati DT_DBTIME su zero.|  
|DT_DBTIME2|Impostazione dei campi dell'ora nel tipo di dati DT_DBTIME2 su zero.|  
|DT_DBTIMESTAMP|Impostazione dei campi dell'ora nel tipo di dati DT_DBTIMESTAMP su zero.|  
|DT_DBTIMESTAMP2|Impostazione dei campi dell'ora nel tipo di dati DT_DBTIMESTAMP su zero.|  
|DT_DBTIMESTAMPOFFSET|Impostazione dei campi dell'ora e del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET su zero.|  
  
#### <a name="converting-from-dtdbtime"></a>Conversione da DT_DBTIME  
  
|Conversione di DT_DBTIME in|Risultato|  
|---------------------------|------------|  
|DT_FILETIME|Impostazione del campo della data nel tipo di dati DT_FILETIME sulla data corrente.|  
|DT_DATE|Impostazione del campo della data nel tipo di dati DT_DATE sulla data corrente.|  
|DT_DBDATE|Impostazione del campo della data nel tipo di dati DT_DBDATE sulla data corrente.|  
|DT_DBTIME|Nessuna modifica.|  
|DT_DBTIME2|Conversione del tipo di dati.|  
|DT_DBTIMESTAMP|Impostazione del campo della data nel tipo di dati DT_DBTIMESTAMP sulla data corrente.|  
|DT_DBTIMESTAMP2|Impostazione del campo della data nel tipo di dati DT_DBTIMESTAMP2 sulla data corrente.|  
|DT_DBTIMESTAMPOFFSET|Impostazione del campo della data e del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET rispettivamente sulla data corrente e su zero.|  
  
#### <a name="converting-from-dtdbtime2"></a>Conversione da DT_DBTIME2  
  
|Conversione di DT_DBTIME2 in|Risultato|  
|----------------------------|------------|  
|DT_FILETIME|Impostazione del campo della data nel tipo di dati DT_FILETIME sulla data corrente.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_FILETIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DATE|Impostazione del campo della data nel tipo di dati DT_DATE sulla data corrente.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DATE può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBDATE|Impostazione del campo della data nel tipo di dati DT_DBDATE sulla data corrente.|  
|DT_DBTIME|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIME2|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME2 di destinazione può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Impostazione del campo della data nel tipo di dati DT_DBTIMESTAMP sulla data corrente.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Impostazione del campo della data nel tipo di dati DT_DBTIMESTAMP2 sulla data corrente.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Impostazione del campo della data e del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET rispettivamente sulla data corrente e su zero.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMPOFFSET può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestamp"></a>Conversione da DT_DBTIMESTAMP  
  
|Conversione di DT_DBTIMESTAMP in|Risultato|  
|--------------------------------|------------|  
|DT_FILETIME|Conversione del tipo di dati.|  
|DT_DATE|Se un valore rappresentato dal tipo di dati DT_DBTIMESTAMP causa l'overflow dell'intervallo supportato dal tipo di dati DT_DATE, viene restituito l'errore DB_E_DATAOVERFLOW. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBDATE|Rimozione del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMP.|  
|DT_DBTIME|Rimozione del valore di data rappresentato dal tipo di dati DT_DBTIMESTAMP.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIME2|Rimozione del valore di data rappresentato dal tipo di dati DT_DBTIMESTAMP.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Nessuna modifica.|  
|DT_DBTIMESTAMP2|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Impostazione del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET su zero.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMPOFFSET può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestamp2"></a>Conversione da DT_DBTIMESTAMP2  
  
|Conversione di DT_DBTIMESTAMP2 in|Risultato|  
|---------------------------------|------------|  
|DT_FILETIME|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_FILETIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DATE|Se un valore rappresentato dal tipo di dati DT_DBTIMESTAMP2 causa l'overflow dell'intervallo supportato dal tipo di dati DT_DATE, viene restituito l'errore DB_E_DATAOVERFLOW. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DATE può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBDATE|Rimozione del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMP2.|  
|DT_DBTIME|Rimozione del valore di data rappresentato dal tipo di dati DT_DBTIMESTAMP2.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIME2|Rimozione del valore di data rappresentato dal tipo di dati DT_DBTIMESTAMP2.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Se un valore rappresentato dal tipo di dati DT_DBTIMESTAMP2 causa l'overflow dell'intervallo supportato dal tipo di dati DT_DBTIMESTAMP, viene restituito l'errore DB_E_DATAOVERFLOW.<br /><br /> Viene eseguito il mapping di DT_DBTIMESTAMP2 a un tipo di dati di SQL Server, datetime2, con un intervallo compreso tra 1 gennaio 1 d.C e il 31 dicembre 9999. Viene eseguito il mapping di DT_DBTIMESTAM a un tipo di dati di SQL Server, datetime, con un intervallo più piccolo, compreso tra 1 gennaio 1753 e 31 dicembre 9999.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati.<br /><br /> Per altre informazioni sugli errori, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP2 di destinazione può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Impostazione del campo del fuso orario nel tipo di dati DT_DBTIMESTAMPOFFSET su zero.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMPOFFSET può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
  
#### <a name="converting-from-dtdbtimestampoffset"></a>Conversione da DT_DBTIMESTAMPOFFSET  
  
|Conversione di DT_DBTIMESTAMPOFFSET in|Risultato|  
|--------------------------------------|------------|  
|DT_FILETIME|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC (Coordinated Universal Time).<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_FILETIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DATE|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC.<br /><br /> Se un valore rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET causa l'overflow dell'intervallo supportato dal tipo di dati DT_DATE, viene restituito l'errore DB_E_DATAOVERFLOW.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DATE può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati.<br /><br /> Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBDATE|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC (Coordinated Universal Time). La modifica può influire sul valore di data. Il valore di ora viene quindi rimosso.|  
|DT_DBTIME|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC.<br /><br /> Rimozione del valore di data rappresentato dal tipo di dati DT_DBTIMESTAMPEOFFSET.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIME2|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC.<br /><br /> Rimozione del valore di data rappresentato dal tipo di dati DT_DBTIMESTAMPEOFFSET.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIME2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC.<br /><br /> Se un valore rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET causa l'overflow dell'intervallo supportato dal tipo di dati DT_DBTIMESTAMP, viene restituito l'errore DB_E_DATAOVERFLOW.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati.<br /><br /> Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMP2|Modifica del valore di ora rappresentato dal tipo di dati DT_DBTIMESTAMPOFFSET in ora UTC.<br /><br /> Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMP2 può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
|DT_DBTIMESTAMPOFFSET|Rimozione del valore di secondi frazionari quando la scala è maggiore del numero di cifre per i secondi frazionari che il tipo di dati DT_DBTIMESTAMPOFFSET di destinazione può contenere. Dopo la rimozione del valore di secondi frazionari, viene generato un report relativo al troncamento dei dati. Per altre informazioni, vedere [Gestione degli errori nei dati](error-handling-in-data.md).|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>Mapping dei tipi di dati di Integration Services ai tipi di dati di database  
 Nella tabella seguente sono incluse informazioni sul mapping tra i tipi di dati utilizzati in alcuni database e i tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Questi mapping sono riepilogati nei file di mapping utilizzati dall'Importazione/Esportazione guidata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'importazione dei dati da queste origini. Per altre informazioni su questi file di mapping, vedere [Importazione/Esportazione guidata SQL Server](../import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).  
  
> [!IMPORTANT]  
>  Questi mapping non rappresentano una rigida corrispondenza, ma offrono solo informazioni generali. In alcuni casi potrebbe essere necessario utilizzare un tipo di dati diverso rispetto a quello indicato nella tabella.  
  
> [!NOTE]  
>  I tipi di dati SQL Server possono essere utilizzati per stimare le dimensioni dei tipi di dati corrispondenti di data e ora di Integration Services.  
  
|Tipo di dati|SQL Server<br /><br /> (SQLOLEDB, SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary, varbinary, timestamp|binary, varbinary, timestamp|BigBinary, VarBinary|RAW|||  
|DT_CY|smallmoney, money|smallmoney, money|Currency||||  
|DT_DATE|||||||  
|DT_DBDATE|[date &#40;Transact-SQL&#41;](/sql/t-sql/data-types/date-transact-sql)|[date &#40;Transact-SQL&#41;](/sql/t-sql/data-types/date-transact-sql)||Data|Data|Data|  
|DT_DBTIME||||TIMESTAMP|time|time|  
|DT_DBTIME2|[time &#40;Transact-SQL&#41;](/sql/t-sql/data-types/time-transact-sql)(p)|[time &#40;Transact-SQL&#41;](/sql/t-sql/data-types/time-transact-sql) (p)|||||  
|DT_DBTIMESTAMP|[datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql), [smalldatetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/smalldatetime-transact-sql)|[datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql), [smalldatetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/smalldatetime-transact-sql)|DateTime|TIMESTAMP, DATE, INTERVAL|TIME, TIMESTAMP, DATE|TIME, TIMESTAMP, DATE|  
|DT_DBTIMESTAMP2|[datetime2 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime2-transact-sql)|[datetime2 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime2-transact-sql)||TIMESTAMP|TIMESTAMP|TIMESTAMP|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetimeoffset-transact-sql)(p)|[datetimeoffset &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetimeoffset-transact-sql) (p)||timestampoffset|timestamp,<br /><br /> varchar|timestamp,<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|INT|INT|Long||INTEGER|INTEGER|  
|DT_I8|BIGINT|BIGINT|||bigint|bigint|  
|DT_NUMERIC|decimal, numeric|decimal, numeric|Decimal|NUMBER, INT|decimal, numeric|decimal, numeric|  
|DT_R4|REAL|REAL|Singolo||real|real|  
|DT_R8|FLOAT|FLOAT|Double|FLOAT, REAL|FLOAT, DOUBLE|FLOAT, DOUBLE|  
|DT_STR|char, varchar||varchar||char, varchar|char, varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar, nvarchar, sql_variant, xml|char, varchar, nchar, nvarchar, sql_variant, xml|LongText|CHAR, ROWID, VARCHAR2, NVARCHAR2, NCHAR|GRAPHIC, VARGRAPHIC|GRAPHIC, VARGRAPHIC|  
|DT_IMAGE|image|image|LongBinary|LONG RAW, BLOB, LOBLOCATOR, BFILE, VARGRAPHIC, LONG VARGRAPHIC, definito dall'utente|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA, VARCHAR () FOR BIT DATA, BLOB|  
|DT_NTEXT|ntext|text, ntext||LONG, CLOB, NCLOB, NVARCHAR, TEXT|LONG VARCHAR, NCHAR, NVARCHAR, TEXT|LONG VARCHAR, DBCLOB, NCHAR, NVARCHAR, TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA, CLOB|  
  
 Per informazioni sul mapping di tipi di dati nel flusso di dati, vedere [Utilizzo di tipi di dati nel flusso di dati](../extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog sul [confronto delle prestazioni tra le tecniche di conversione dei tipi di dati in SSIS 2008](https://go.microsoft.com/fwlink/?LinkId=220823)su blogs.msdn.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati nei flussi di dati](data-in-data-flows.md)  
  
  
