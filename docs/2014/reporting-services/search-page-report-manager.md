---
title: Eseguire ricerche di pagina (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 51ffdc07-e1b9-4ed7-acb3-dd98d7cce273
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 12413c103230d8c085a9701e3fb83db15135895a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102255"
---
# <a name="search-page-report-manager"></a>Pagina Cerca (Gestione report)
  Utilizzare la pagina Risultati ricerca per visualizzare i risultati di un'operazione di ricerca eseguita in report, report collegati, modelli di report, origini dei dati condivise, cartelle o risorse. I risultati della ricerca vengono visualizzati in ordine alfabetico e possono essere ordinati in base al tipo, al nome o alla descrizione.  
  
 Dalle operazioni di ricerca sono esclusi gli snapshot di report inclusi nella cronologia dei report, le sottoscrizioni e le pianificazioni condivise. In modo analogo, se non si dispone di autorizzazioni sufficienti per la visualizzazione di una cartella o un report, tale elemento verrà escluso dalla ricerca.  
  
 Non è possibile cercare testo all'interno di un report o di un modello. Per cercare testo specifico all'interno di un report, utilizzare la barra degli strumenti nella parte superiore del report.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-search-results-page"></a>Per aprire la pagina Risultati ricerca  
  
1.  Aprire Gestione report.  
  
2.  All'inizio della pagina, digitare il criterio di ricerca nella casella **Cerca** . Quindi premere Invio o fare clic sulla freccia Cerca.  
  
## <a name="options"></a>Opzioni  
 **Elimina**  
 Fare clic per rimuovere un elemento da un database del server di report.  
  
> [!NOTE]  
>  Questo pulsante è disponibile solo in **Visualizzazione Dettagli**. Tuttavia, è possibile passare il puntatore del mouse su un elemento e utilizzare il menu per accedere alla funzionalità di eliminazione in **Visualizzazione Dettagli** o in **Visualizzazione Elenco**.  
  
 **Sposta**  
 Fare clic per spostare un elemento. Verrà visualizzata la pagina di spostamento degli elementi, nella quale è possibile selezionare un diverso percorso della cartella.  
  
> [!NOTE]  
>  Questo pulsante è disponibile solo in **Visualizzazione Dettagli**. Tuttavia, è possibile passare il puntatore del mouse su un elemento e utilizzare il menu per accedere alla funzionalità di spostamento in **Visualizzazione Dettagli** o in **Visualizzazione Elenco**.  
  
 Casella Cerca  
 Digitare tutto o parte del nome di un elemento che si desidera individuare e quindi fare clic su **Vai** per avviare la ricerca. La stringa di ricerca può essere composta al massimo da 128 caratteri.  
  
 Nei risultati di ricerca verranno inclusi i nomi o le descrizioni degli elementi che contengono l'intera stringa di ricerca in qualsiasi posizione nel valore di testo.  
  
 Gli operatori booleani, ad esempio il segno più (+), non sono supportati.  
  
 **Visualizzazione dettagli**  
 Fare clic per visualizzare la pagina Risultati ricerca in un elenco che contiene informazioni aggiuntive sugli elementi, quale il tipo di elemento, il nome, la descrizione, la cartella che contiene l'elemento e la data dell'ultima esecuzione. In **Visualizzazione Dettagli**, è possibile utilizzare i pulsanti **Elimina** e **Sposta** per rimuovere e spostare gli elementi nella cartella.  
  
 Passare con il puntatore del mouse su un elemento e fare clic sulla freccia a discesa per aprire il menu a discesa dal quale è possibile accedere alle proprietà dell'elemento selezionato ed eseguirne la configurazione.  
  
 **Visualizzazione elenco**  
 Fare clic per visualizzare la pagina risultati ricerca senza dettagli come in **visualizzazione dettagli**. Visualizzazione Elenco è la visualizzazione predefinita quando viene visualizzata la pagina Risultati ricerca.  
  
 Passare con il puntatore del mouse su un elemento e fare clic sulla freccia a discesa per aprire il menu a discesa dal quale è possibile accedere alle proprietà dell'elemento selezionato ed eseguirne la configurazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
