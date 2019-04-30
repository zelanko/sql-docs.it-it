---
title: Generating Reports (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Generating reports
ms.assetid: 1c0202e8-546d-4cb3-a37f-1d2e35d53839
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: beebb6df04675e87ff65b51161191700e07f0199
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183052"
---
# <a name="generating-reports-mysqltosql"></a>Generazione di report (MySQLToSQL)
I report di determinate attività eseguite usando i comandi vengono generati nella Console SSMA a livello di oggetto dell'albero.  
  
Utilizzare la procedura seguente per generare report:  
  
1.  Specificare il **scrittura riepilogo-report-a-** parametro. Il report viene archiviato come il nome del file (se specificato) o nella cartella specificati. È il nome del file system predefinito come indicato nella tabella seguente, dove **&lt;n&gt;** è il numero di file univoco che viene incrementato con una cifra a ogni esecuzione del comando stesso.  
  
    I comandi nei confronti di report sono:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Command**|**Titolo del report**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrate-data|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|synchronize-target|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|aggiornamento da database|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Un report di output è diverso dal Report di valutazione. Il primo è un report sulle prestazioni di un comando eseguito durante, quest'ultimo è un report XML per l'utilizzo a livello di codice.  
  
    Per le opzioni di comando per i report di output (da Sl. No. 2-4 sopra), vedere la [esecuzione della Console SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) sezione.  
  
2.  Indica che l'extent di dettaglio desiderato nel report di output utilizzando le impostazioni di Report livello di dettaglio:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Comando e parametri**|**Descrizione di output**|  
    |1|verbose="false"|Genera un report di riepilogo dell'attività.|  
    |2|verbose="true"|Genera un report di stato di riepilogo e dettagliate per ogni attività.|  
  
    > [!NOTE]  
    > Le impostazioni del livello di dettaglio Report specificata in precedenza sono applicabili per generare report di valutazione, convert-schema, eseguire la migrazione di dati, i comandi di convert-sql-statement.  
  
3.  Indica che l'extent di dettaglio desiderato nei report di errore utilizzando le impostazioni di segnalazione errori:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Comando e parametri**|**Descrizione di output**|  
    |1|report-errors="false"|Nessun dettaglio in caso di errore / avviso / i messaggi di informazioni.|  
    |2|report-errors="true"|Dettagli errore / avviso / i messaggi di informazioni.|  
  
    > [!NOTE]  
    > Le impostazioni di segnalazione di errori specificato in precedenza sono applicabili per generare report di valutazione, convert-schema, eseguire la migrazione di dati, i comandi di convert-sql-statement.  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>synchronize-target:  
Il comando **destinazione sincronizzare** ha **report errori-a-** parametro che specifica il percorso del report di errore per l'operazione di sincronizzazione. Quindi, un file con nome **TargetSynchronizationReport&lt;n&gt;. XML** viene creato nella posizione specificata, in cui **&lt;n&gt;** è il numero di file univoco che viene incrementato con una cifra a ogni esecuzione del comando stesso.  
  
**Nota:** Se il percorso della cartella è specificato, 'report-errori-to' parametro diventa un attributo facoltativo per il comando 'sincronizzare-target'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**object-name:** Specifica gli oggetti considerati per la sincronizzazione (può anche avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
**on-error:** Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   fail-script  
  
### <a name="refresh-from-database"></a>aggiornamento dal database:  
Il comando **dal database di aggiornamento** ha **report errori-a-** parametro che specifica il percorso del report di errore per l'operazione di aggiornamento. Quindi, un file con nome **SourceDBRefreshReport&lt;n&gt;. XML** viene creato nella posizione specificata, in cui **&lt;n&gt;** è il numero di file univoco che viene incrementato con una cifra a ogni esecuzione del comando stesso.  
  
**Nota:** Se il percorso della cartella è specificato, 'report-errori-to' parametro diventa un attributo facoltativo per il comando 'sincronizzare-target'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**object-name:** Specifica gli oggetti considerati per l'aggiornamento (può anche avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
**on-error:** Specifica se occorre indicare errori di aggiornamento come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   fail-script  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della Console SSMA (MySQL)](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
