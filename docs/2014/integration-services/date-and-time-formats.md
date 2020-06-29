---
title: Formati di data e ora | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a5f880de91cad3925e43a65e6282319dbb1e57ee
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429708"
---
# <a name="date-and-time-formats"></a>Formati di data e ora
  L'analisi veloce offre un set di routine semplici e veloci per l'analisi dei dati. L'analisi veloce supporta i formati seguenti per i tipi di dati data e ora.  
  
## <a name="date-data-types"></a>Tipi di dati per i valori di data  
 L'analisi veloce supporta i formati stringa seguenti per i dati di data:  
  
-   Formati di data che includono spazi vuoti iniziali. Il valore " 2004- 02-03", ad esempio, è valido.  
  
-   Formati ISO 8601, elencati nella tabella seguente:  
  
    |Format|Descrizione|  
    |------------|-----------------|  
    |YYYYMMDD<br /><br /> YYYY-MM-DD|Formati di base ed esteso con anno a quattro cifre, a due cifre e giorno a due cifre. Nel formato esteso, le parti della data sono separate da un segno meno (-).|  
    |AAAA-MM|Formati di base ed esteso a precisione ridotta, con anno a quattro cifre e mese a due cifre. Nel formato esteso, le parti della data sono separate da un segno meno (-).|  
    |AAAA|Formato a precisione ridotta con anno a quattro cifre.|  
  
 L'analisi veloce non supporta i formati seguenti per i dati di data:  
  
-   Valore del mese in forma alfabetica. Ad esempio, il formato di data 31-ott-2003 non è valido.  
  
-   Formati ambigui, ad esempio GG-MM-AAAA e MM-GG-AAAA. Ad esempio, le date 03-04-1995 e 04-03-1995 non sono valide.  
  
-   Formati troncati di base ed esteso con anno di calendario a quattro cifre e giorno dell'anno a tre cifre, AAAAGGG e AAAA-GGG.  
  
-   Formati di base ed esteso con anno a quattro cifre, numero di due cifre per la settimana dell'anno e numero di una cifra per il giorno della settimana, AAAASssG e AAAA-Sss-G.  
  
-   Formati troncati di base ed esteso per date che includono anno e settimana, con anno a quattro cifre e numero di due cifre per la settimana, AAASss e AAAA-Sss.  
  
 I dati di output dell'analisi veloce sono di tipo DT_DBDATE. Ai valori di data con formati troncati viene applicato un riempimento. Ad esempio, AAAA diventa AAAA0101.  
  
 Per ulteriori informazioni, vedere [Integration Services tipi di dati](data-flow/integration-services-data-types.md).  
  
## <a name="time-data-type"></a>Tipi di dati per i valori di ora  
 L'analisi veloce supporta i formati stringa seguenti per i dati di ora:  
  
-   Formati di ora che includono spazi vuoti iniziali. Ad esempio, il valore " 10.24" è valido.  
  
-   Formato di 24 ore. L'analisi veloce non supporta la notazione con AM e PM.  
  
-   Formati di ora ISO 8601, elencati nella tabella seguente:  
  
    |Format|Descrizione|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|Formati di base ed esteso con ora a due cifre, minuto a due cifre e giorno a due cifre. Nel formato esteso, le parti dell'ora sono separate da un punto (.).|  
    |HHMI<br /><br /> HH:MI|Formati troncati di base ed esteso con ora a due cifre e minuto a due cifre. Nel formato esteso, le parti dell'ora sono separate da un punto (.).|  
    |HH|Formato troncato con ora a due cifre.|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|Formato per la mezzanotte.|  
  
-   Formati ora che specificano un fuso orario, elencati nella tabella seguente:  
  
    |Format|Descrizione|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|Formati di base ed estesi che indicano il numero di ore e minuti da aggiungere all'ora UTC (Coordinated Universal Time) per ottenere l'ora locale.|  
    |-HH:MI<br /><br /> -HHMI|Formati di base ed estesi che indicano il numero di ore e minuti da sottrarre all'ora UTC per ottenere l'ora locale.|  
    |+HH|Formato troncato che indica il numero di ore da aggiungere all'ora UTC per ottenere l'ora locale.|  
    |-HH|Formato troncato che indica il numero di ore da sottrarre all'ora UTC per ottenere l'ora locale.|  
    |Z|Valore 0 che indica che l'ora è rappresentata in formato UTC.|  
  
     I formati per tutti i dati di ora e di data e ora possono includere un elemento relativo al fuso orario. Il valore del fuso orario viene tuttavia ignorato dal sistema, ad eccezione del caso in cui i dati sono di tipo DT_DBTIMESTAMPOFFSET. Per ulteriori informazioni, vedere [Integration Services tipi di dati](data-flow/integration-services-data-types.md).  
  
     Nei formati che includono un elemento del fuso orario, non vi sono spazi tra l'elemento relativo all'ora e quello relativo al fuso orario, come illustrato nell'esempio seguente:  
  
     HH:MI:SS[+HH:MI]  
  
     Le parentesi quadrate nell'esempio precedente indicano che il valore del fuso orario è facoltativo.  
  
-   Formati di ora che includono una frazione decimale, elencati nella tabella seguente:  
  
    |Format|Descrizione|  
    |------------|-----------------|  
    |HH[.nnnnnnn]|n è un valore compreso tra 0 e 9999999 che rappresenta una frazione di ore. Le parentesi quadrate indicano che tale valore è facoltativo.<br /><br /> Il valore 12.750 indica ad esempio le 12:45.|  
    |HHMI[.nnnnnnn]<br /><br /> HH:MI[.nnnnnnn]|n è un valore compreso tra 0 e 9999999 che rappresenta una frazione di minuti. Le parentesi quadrate indicano che tale valore è facoltativo.<br /><br /> Il valore 1220,500 indica ad esempio le 12:20:30.|  
    |HHMISS[.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n è un valore compreso tra 0 e 9999999 che rappresenta una frazione di secondi. Le parentesi quadrate indicano che tale valore è facoltativo.<br /><br /> Il valore 122040,250 indica ad esempio le 12:20:40.15.|  
  
    > [!NOTE]  
    >  Il separatore della parte frazionaria per i formati di ora nella tabella precedente può essere un punto o una virgola.  
  
-   Valori di ora che includono un secondo intercalare, come illustrato negli esempi seguenti:  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 Le stringhe di output dell'analisi veloce sono di tipo DT_DBTIME e DT_DBTIME2. Ai valori di ora con formati troncati viene applicato un riempimento. HH:MI diventa ad esempio HH:MM:00.000.  
  
 Per ulteriori informazioni, vedere [Integration Services tipi di dati](data-flow/integration-services-data-types.md).  
  
## <a name="datetime-data-type"></a>Tipi di dati per i valori di data e ora  
 L'analisi veloce supporta i formati stringa seguenti per i dati di data e ora:  
  
-   Formati che includono spazi vuoti iniziali. Il valore "  2003-01-10T203910", ad esempio, è valido.  
  
-   Combinazioni di formati di data validi e formati di ora validi separati da una T maiuscola e di formati di fuso orario validi. Ad esempio, AAAAMMGGT[HHMISS][+HH:MI]. I valori relativi a ora e fuso orario non sono obbligatori. Il valore "2003-10-14", ad esempio, è valido.  
  
 L'analisi veloce non supporta gli intervalli di tempo. Non è ad esempio possibile analizzare un intervallo di tempo identificato da una data e ora di inizio e da una data e ora di fine, nel formato AAAAMMGGThhmmss/AAAAMMGGThhmmss.  
  
 Le stringhe di output dell'analisi veloce sono di tipo DT_DATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET. Ai valori di data e ora con formati troncati viene applicato un riempimento. Nella tabella seguente sono elencati i valori aggiunti per le parti mancanti relative a data e ora.  
  
|Parte della data o dell'ora|Spaziatura interna|  
|---------------------|-------------|  
|Secondi|Viene aggiunto 00.|  
|Minuti|Aggiungi 00:00.|  
|Ora|Viene aggiunto 00.00.00.|  
|Giorno|Viene aggiunto 01 come giorno del mese.|  
|Month|Viene aggiunto 01 come mese dell'anno.|  
  
 Per ulteriori informazioni, vedere [Integration Services tipi di dati](data-flow/integration-services-data-types.md).  
  
  
