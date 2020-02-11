---
title: Finestre Risultati ricerca
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vs.findresults2
helpviewer_keywords:
- Find Results Windows dialog box
ms.assetid: 3b68dbb7-26d6-4bc9-bd2c-c27e5dc385c3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88fb0cda002694d87cad94dd8032811f6451f1cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245132"
---
# <a name="find-results-windows"></a>Finestre Risultati ricerca
  Nelle due finestre Risultati ricerca vengono visualizzate le corrispondenze trovate utilizzando la scheda **Cerca nei file** o **Sostituisci nei file** della finestra di dialogo **Trova e sostituisci** . Il comando **Opzioni risultati** disponibile nelle schede **Cerca nei file** e **Sostituisci nei file** consente di scegliere la finestra Risultati ricerca in cui verranno visualizzate le corrispondenze trovate.  
  
 Ogni volta che vengono trovate corrispondenze, la finestra Risultati ricerca selezionata verrà visualizzata automaticamente. Per visualizzare manualmente una finestra Risultati ricerca scegliere **Altre finestre** dal menu **Visualizza** e quindi fare clic su **Risultati ricerca 1** o **Risultati ricerca 2**.  
  
 Per visualizzare il file di codice e passare alla riga in cui viene rilevata una corrispondenza, fare doppio clic su una riga qualsiasi nell'elenco dei risultati. Il file del codice sorgente verrà visualizzato nell'editor del codice con il punto d'inserimento posizionato all'inizio del testo della corrispondenza. Sul margine indicatore dell'editor verrà visualizzato un simbolo per contrassegnare la riga contenente la corrispondenza e il testo completo verrà visualizzato nella barra di stato.  
  
## <a name="toolbar-buttons"></a>Pulsanti della barra degli strumenti  
 Sulla barra degli strumenti sono disponibili i pulsanti seguenti che consentono di analizzare l'elenco dei risultati e di passare alle righe del codice in cui sono state trovate corrispondenze.  
  
 **flag di pagina + freccia in su**  
 Consente di spostarsi alla riga in cui è stata trovata la corrispondenza selezionata.  
  
 **pagina + freccia sinistra**  
 Consente di spostarsi alla riga che contiene la corrispondenza precedente  
  
 **pagina + freccia destra**  
 Consente di spostarsi alla riga che contiene la corrispondenza successiva.  
  
 **Cancella tutto**  
 Consente di rimuovere tutte le corrispondenze dall'elenco **Risultati** .  
  
## <a name="shortcut-keys"></a>Tasti di scelta rapida  
 Sono disponibili i tasti di scelta rapida seguenti che consentono di spostarsi rapidamente tra le corrispondenze trovate.  
  
 CTRL+HOME  
 Consente di tornare all'inizio della finestra Risultati ricerca.  
  
 CTRL+FINE  
 Consente di spostarsi alla fine della finestra Risultati ricerca.  
  
 PGSU  
 Consente di spostarsi al gruppo di corrispondenze precedente.  
  
 PGGIÙ  
 Consente di spostarsi al gruppo di corrispondenze successivo.  
  
 FRECCIA SU  
 Consente di selezionare la corrispondenza precedente.  
  
 Freccia GIÙ  
 Consente di selezionare la corrispondenza successiva.  
  
## <a name="search-result-entries"></a>Voci dei risultati della ricerca  
 Per ogni voce nell'elenco dei risultati sono incluse le informazioni seguenti:  
  
-   Percorso completo  
  
-   Nome file  
  
-   Numero di riga  
  
-   Testo completo della riga contenente la corrispondenza  
  
> [!TIP]  
>  È possibile utilizzare **Ricerca veloce** per analizzare un lungo elenco di risultati. Aprire e ancorare la finestra Risultati ricerca e quindi fare clic sul pulsante triangolare **Vista** nella scheda **Trova** e passare a **Ricerca veloce**. Impostare il campo di ricerca **Cerca in** su **Finestra attiva**, digitare una stringa nel campo **Trova** e quindi fare clic su **Trova successivo**. In questo modo sarà possibile analizzare l'elenco dei risultati relativo alle corrispondenze trovate in determinati file o cartelle o relativo alle corrispondenze trovate all'interno di righe di codice contenenti anche un altro termine chiave.  
  
## <a name="summary-lines"></a>Righe di riepilogo  
 Ogni set dei risultati della ricerca inizia con una riga che indica i parametri di ricerca e termina con una riga di statistiche. L'elenco dei risultati di una ricerca **Cerca nei file** delle stringhe corrispondenti all'espressione regolare "`var[1-3]&par`" in tutti i documenti aperti potrebbe iniziare ad esempio con la riga seguente di parametri di ricerca:  
  
 `Find all "var[1-3]&par" Regular Expression, All Open Documents`  
  
 e potrebbe terminare con la riga seguente di statistiche:  
  
 `Total found: 57  Matching files: 23  Total files searched: 59`  
  
 L'elenco dei risultati di una sostituzione **Sostituisci nei file** delle stringhe corrispondenti all'espressione regolare "`var[1-3]&par`" con la stringa "`sample`" in tutti i documenti aperti potrebbe iniziare ad esempio con la riga seguente di parametri di ricerca:  
  
 `Replace "var[1-3]&par", "sample", Regular Expression, All Open Documents`  
  
 e potrebbe terminare con la riga seguente di statistiche:  
  
 `Total replaced: 57  Matching files: 23  Total files searched: 59`  
