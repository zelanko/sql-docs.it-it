---
title: Generazione di report (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 69ef5fd9-190d-4c58-8199-b3f77d5e1883
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2d96b82e3ce883bcf9e704ea001024228be81761
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989655"
---
# <a name="generating-reports-db2tosql"></a>Generazione di report (DB2ToSQL)
I report di determinate attività eseguite usando i comandi vengono generati nella Console SSMA a livello di oggetto dell'albero.  
  
Utilizzare la procedura seguente per generare report:  
  
1.  Specificare il **scrittura riepilogo-report-a-** parametro. Il report viene archiviato come il nome del file (se specificato) o nella cartella specificati. È il nome del file system predefinito come indicato nella tabella seguente, dove **&lt;n&gt;** è il numero di file univoco che viene incrementato con una cifra a ogni esecuzione del comando stesso.  
  
    I comandi nei confronti di report sono:  
  
    ||||  
    |-|-|-|  
    |**SL. No.**|**Command**|**Titolo del report**|  
    |1|generare report di valutazione|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrate-data|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|synchronize-target|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|aggiornamento da database|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Un report di output è diverso dal Report di valutazione. Il primo è un report sulle prestazioni di un comando eseguito durante, quest'ultimo è un report XML per l'utilizzo a livello di codice.  
  
    Per le opzioni di comando per i report di output (da Sl. No. 2-4 sopra), vedere la [esecuzione della Console SSMA &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) sezione.  
  
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
    |1|Segnala errori = "false"|Nessun dettaglio in caso di errore / avviso / i messaggi di informazioni.|  
    |2|Segnala errori = "true"|Dettagli errore / avviso / i messaggi di informazioni.|  
  
    > [!NOTE]  
    > Le impostazioni di segnalazione di errori specificato in precedenza sono applicabili per generare report di valutazione, convert-schema, eseguire la migrazione di dati, i comandi di convert-sql-statement.  
  
**Esempio:**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>synchronize-target:  
Il comando **destinazione sincronizzare** ha **report errori-a-** parametro che specifica il percorso del report di errore per l'operazione di sincronizzazione. Quindi, un file con nome **TargetSynchronizationReport&lt;n&gt;. XML** viene creato nella posizione specificata, in cui **&lt;n&gt;** è il numero di file univoco che viene incrementato con una cifra a ogni esecuzione del comando stesso.  
  
**Nota:** Se il percorso della cartella è specificato, 'report-errori-to' parametro diventa un attributo facoltativo per il comando 'sincronizzare-target'.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**object-name:** Specifica gli oggetti considerati per la sincronizzazione (può anche avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
**in errore:** Specifica se specificare gli errori di sincronizzazione come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
-   -Totale report come avviso  
  
-   report-each-come-avviso  
  
-   Errore-script  
  
### <a name="refresh-from-database"></a>aggiornamento dal database:  
Il comando **dal database di aggiornamento** ha **report errori-a-** parametro che specifica il percorso del report di errore per l'operazione di aggiornamento. Quindi, un file con nome **SourceDBRefreshReport&lt;n&gt;. XML** viene creato nella posizione specificata, in cui **&lt;n&gt;** è il numero di file univoco che viene incrementato con una cifra a ogni esecuzione del comando stesso.  
  
**Nota:** Se il percorso della cartella è specificato, 'report-errori-to' parametro diventa un attributo facoltativo per il comando 'sincronizzare-target'.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**object-name:** Specifica gli oggetti considerati per l'aggiornamento (può anche avere un nome di oggetto gruppo o nomi di oggetto individuali).  
  
**in errore:** Specifica se occorre indicare errori di aggiornamento come avvisi o errori. Opzioni disponibili per in caso di errore:  
  
-   -Totale report come avviso  
  
-   report-each-come-avviso  
  
-   Errore-script  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione della console SSMA](https://msdn.microsoft.com/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
