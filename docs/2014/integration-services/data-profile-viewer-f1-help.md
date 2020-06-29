---
title: Guida sensibile al contesto Visualizzatore profilo dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dataprofileviewer.f1
helpviewer_keywords:
- Data Profile Viewer [Integration Services]
- Data Profiling task [Integration Services], viewer
ms.assetid: 3469c60a-8f4f-46ba-999a-cb9070197fea
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d541e0c6143c9652629f80d911bf42db26e9a4ef
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85429718"
---
# <a name="data-profile-viewer-f1-help"></a>Guida sensibile al contesto del Visualizzatore profilo dati
  Utilizzare il Visualizzatore profilo dati per visualizzare l'output dell'attività Profiling dati.  
  
 Per altre informazioni sull'uso del Visualizzatore profilo dati, vedere [Visualizzatore profilo dati](control-flow/data-profile-viewer.md). Per altre informazioni sull'uso dell'attività Profiling dati che crea l'output del profilo analizzato nel Visualizzatore profilo dati, vedere [Impostazione dell'attività Profiling Dati](control-flow/data-profiling-task.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Apri**  
 Consente di accedere al file salvato che contiene l'output dell'attività Profiling dati.  
  
 Riquadro**Profili**  
 Espandere l'albero nel riquadro **Profili** per visualizzare i profili inclusi nell'output. Selezionare un profilo per visualizzarne i risultati.  
  
 Riquadro**Messaggio**  
 Visualizza i messaggi di stato.  
  
 Riquadro**Drill-down**  
 Visualizza le righe di dati che corrispondono a un valore nell'output, se l'origine dati utilizzata dall'attività Profiling dati è disponibile.  
  
 Se, ad esempio, si visualizza l'output di un profilo Distribuzione valori di colonna per una colonna US State, il riquadro **Distribuzione dettagliata valori** potrebbe contenere una riga per "WA". Fare doppio clic sulla riga nel riquadro **Distribuzione dettagliata valori** per visualizzare le righe di dati in cui il valore della colonna di stato è "WA" nel riquadro di drill-down.  
  
## <a name="dynamic-options"></a>Opzioni dinamiche  
  
### <a name="profile-type--column-length-distribution-profile"></a>Tipo di profilo: profilo Distribuzione lunghezze di colonna  
  
#### <a name="column-length-distribution-profile---column-pane"></a>Profilo Distribuzione lunghezze di colonna- \<column> riquadro  
 **Lunghezza minima**  
 Visualizza la lunghezza minima dei valori nella colonna.  
  
 **Lunghezza massima**  
 Visualizza la lunghezza massima dei valori nella colonna.  
  
 **Ignora spazi iniziali**  
 Indica se il profilo è stato calcolato con un valore `IgnoreLeadingSpaces` impostato su True o False. Questa proprietà è stata impostata nella pagina **Richieste profilo** in Editor attività Profiling dati.  
  
 **Ignora spazi finali**  
 Indica se il profilo è stato calcolato con un valore `IgnoreTrailingSpaces` impostato su True o False. Questa proprietà è stata impostata nella pagina **Richieste profilo** in Editor attività Profiling dati.  
  
 **Row Count**  
 Visualizza il numero di righe della tabella o della vista.  
  
#### <a name="detailed-length-distribution-pane"></a>Riquadro Distribuzione dettagliata lunghezze  
 **Lunghezza**  
 Visualizza le lunghezze di colonna rilevate nella colonna analizzata.  
  
 **Numero**  
 Visualizza il numero di righe in cui il valore della colonna analizzata ha la lunghezza indicata nella colonna **Lunghezza** .  
  
 **Percentuale**  
 Visualizza la percentuale di righe in cui il valore della colonna analizzata ha la lunghezza indicata nella colonna **Lunghezza** .  
  
### <a name="profile-type--column-null-ratio-profile"></a>Tipo di profilo: profilo Rapporto di valori Null nella colonna  
  
#### <a name="column-null-ratio-profile---column-pane"></a>Profilo rapporto di valori null nella colonna- \<column> riquadro  
 **Conteggio valori Null**  
 Visualizza il numero di righe in cui il valore della colonna analizzata è un valore Null.  
  
 **Percentuale valori Null**  
 Visualizza la percentuale di righe in cui il valore della colonna analizzata è un valore Null.  
  
 **Row Count**  
 Visualizza il numero di righe della tabella o della vista.  
  
### <a name="profile-type--column-pattern-profile"></a>Tipo di profilo: profilo Criteri di ricerca colonna  
  
#### <a name="column-pattern-profile---column-pane"></a>Riquadro profilo Criteri di ricerca colonna \<column>  
 **Row Count**  
 Visualizza il numero di righe della tabella o della vista.  
  
#### <a name="pattern-distribution-pane"></a>Riquadro Distribuzione criteri di ricerca  
 **Modello**  
 Visualizza i modelli calcolati per la colonna analizzata.  
  
 **Percentuale**  
 Visualizza la percentuale di righe i cui valori corrispondono al modello visualizzato nella colonna **Modello** .  
  
### <a name="profile-type--column-statistics-profile"></a>Tipo di profilo: profilo Statistiche di colonna  
  
#### <a name="column-statistics-profile---column-pane"></a>Profilo Statistiche di colonna- \<column> riquadro  
 **Minimo**  
 Visualizza il valore minimo rilevato nella colonna analizzata.  
  
 **Massimo**  
 Visualizza il valore massimo rilevato nella colonna analizzata.  
  
 **Significa**  
 Visualizza la media dei valori rilevati nella colonna analizzata.  
  
 **Deviazione standard**  
 Visualizza la deviazione standard dei valori rilevati nella colonna analizzata.  
  
### <a name="profile-type--column-value-distribution-profile"></a>Tipo di profilo: profilo Distribuzione valori di colonna  
  
#### <a name="column-value-distribution-profile---column-pane"></a>Profilo Distribuzione valori di colonna- \<column> riquadro  
 **Numero di valori distinct**  
 Visualizza il conteggio dei valori distinct rilevati nella colonna analizzata.  
  
 **Row Count**  
 Visualizza il numero di righe della tabella o della vista.  
  
#### <a name="detailed-value-distribution-pane"></a>Riquadro Distribuzione dettagliata valori  
 **Valore**  
 Visualizza i valori distinct rilevati nella colonna analizzata.  
  
 **Numero**  
 Visualizza il numero di righe in cui la colonna analizzata ha il valore indicato nella colonna **Valore** .  
  
 **Percentuale**  
 Visualizza la percentuale di righe in cui la colonna analizzata ha il valore indicato nella colonna **Valore** .  
  
### <a name="profile-type--candidate-key-profile"></a>Tipo di profilo: profilo Chiave candidata  
  
#### <a name="candidate-key-profile---table-pane"></a>Profilo chiave candidata- \<table> riquadro  
 **Colonne chiave**  
 Visualizza le colonne selezionate per l'analisi come chiave candidata.  
  
 **Attendibilità chiave**  
 Visualizza il livello di attendibilità (come percentuale) della colonna o combinazione di colonne chiave candidata. Un livello di attendibilità inferiore al 100% indica la presenza di valori duplicati.  
  
#### <a name="key-violations-pane"></a>Riquadro Violazioni chiave  
 **\<column1>, \<column2> e così via.**  
 Visualizza i valori duplicati rilevati nella colonna analizzata.  
  
 **Numero**  
 Visualizza il numero di righe in cui la colonna specificata ha il valore indicato nella prima colonna.  
  
### <a name="profile-type--functional-dependency-profile"></a>Tipo di profilo: profilo Dipendenza funzionale  
  
#### <a name="functional-dependency-profile-pane"></a>Riquadro Profilo Dipendenza funzionale  
 **Colonne determinanti**  
 Visualizza la colonna o le colonne selezionate come colonne determinanti. Nell'esempio in cui uno stesso codice postale ZIP (Stati Uniti) deve essere associato sempre allo stesso stato, il codice postale rappresenta la colonna determinante.  
  
 **Colonna dipendente**  
 Visualizza la colonna o le colonne selezionate come colonne dipendenti. Nell'esempio in cui uno stesso codice postale ZIP (Stati Uniti) deve essere associato sempre allo stesso stato, lo stato rappresenta la colonna dipendente.  
  
 **Attendibilità dipendenza funzionale**  
 Visualizza il livello di attendibilità (come percentuale) della dipendenza funzionale tra colonne. Un livello di attendibilità inferiore al 100% indica che vi sono casi in cui il valore determinante non determina il valore dipendente. Nell'esempio in cui uno stesso codice postale ZIP (Stati Uniti) deve essere associato sempre allo stesso stato, tale livello di attendibilità indica che alcuni valori di stato non sono validi.  
  
#### <a name="functional-dependency-violations-pane"></a>Riquadro Violazioni dipendenza funzionale  
  
> [!NOTE]  
>  Una percentuale elevata di valori non corretti nei dati può provocare risultati imprevisti da un profilo Dipendenza funzionale. Ad esempio, il 90% delle righe contiene il valore di stato "WI" per il valore di codice postale ZIP "98052". Il profilo segnala le righe che contengono il valore di stato "WA" corretto come violazioni.  
  
 **\<determinant column name>**  
 Visualizza il valore della colonna determinante o della combinazione di colonne determinanti in questa istanza di una violazione della dipendenza funzionale.  
  
 **\<dependent column name>**  
 Visualizza il valore della colonna dipendente in questa istanza di una violazione della dipendenza funzionale.  
  
 **Conteggio del supporto**  
 Visualizza il numero di righe in cui il valore della colonna determinante determina la colonna dipendente.  
  
 **Conteggio violazioni**  
 Visualizza il numero di righe in cui il valore della colonna determinante non determina la colonna dipendente. Si tratta delle righe in cui il valore dipendente corrisponde al valore visualizzato nella **\<dependent column name>** colonna.  
  
 **Percentuale del supporto**  
 Visualizza la percentuale di righe in cui la colonna determinante determina la colonna dipendente.  
  
### <a name="profile-type--value-inclusion-profile"></a>Tipo di profilo: profilo Inclusione valore  
  
#### <a name="value-inclusion-profile-pane"></a>Riquadro Profilo Inclusione valore  
 **Colonne lato subset**  
 Visualizza la colonna o la combinazione di colonne analizzate per determinare se sono incluse nelle colonne del superset.  
  
 **Colonne lato superset**  
 Visualizza la colonna o la combinazione di colonne analizzate per determinare se includono i valori delle colonne del subset.  
  
 **Attendibilità inclusione**  
 Visualizza il livello di attendibilità (come percentuale) della sovrapposizione tra colonne. Un livello di attendibilità inferiore al 100% indica che vi sono casi in cui il valore del subset non viene rilevato tra i valori del superset.  
  
#### <a name="inclusion-violations-pane"></a>Riquadro Violazioni inclusione  
 **\<column1>, \<column2> e così via.**  
 Visualizza i valori nella colonna o colonne del subset che non sono disponibili nella colonna o colonne del superset.  
  
 **Numero**  
 Visualizza il numero di righe in cui la colonna specificata ha il valore indicato nella prima colonna.  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzatore profilo dati](control-flow/data-profile-viewer.md)   
 [Attività Profiling dati e visualizzatore](control-flow/data-profiling-task-and-viewer.md)  
  
  
