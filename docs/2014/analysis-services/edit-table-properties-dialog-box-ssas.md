---
title: Modifica finestra di dialogo Proprietà tabella (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.edittablepropdb.f1
ms.assetid: 8d913e83-7246-44cc-8fc7-31729023c0d8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fefc72d81129ac4691f35209f25c4f348272c81
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081439"
---
# <a name="edit-table-properties-dialog-box-ssas"></a>Finestra di dialogo Modifica proprietà tabella (SSAS)
  La finestra di dialogo **Modifica proprietà tabella** consente di visualizzare e modificare le proprietà di tabelle importate in Progettazione modelli tramite l'Importazione guidata tabella. Per accedere a questa finestra di dialogo, in Progettazione modelli selezionare una tabella, quindi scegliere **Proprietà tabella** dal menu **Tabella**.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Le opzioni per questa finestra di dialogo sono diverse, a seconda che i dati siano stati originariamente importati selezionando tabelle da un elenco o utilizzando una query SQL.  
  
## <a name="table-preview-mode"></a>Modalità Anteprima tabella  
 **Nome tabella**  
 Visualizza il nome della tabella dati nel modello.  
  
> [!NOTE]  
>  Il nome della tabella non può essere modificato in questo punto. Tuttavia, è possibile modificarlo facendo clic con il pulsante destro del mouse sulla scheda della tabella nella parte inferiore di Progettazione modelli.  
  
 **Nome connessione**  
 Visualizza il nome della connessione attualmente in uso.  
  
 **Nome origine**  
 Consente di visualizzare o modificare la tabella dalla quale vengono ottenuti i dati.  
  
 Se per l'origine si imposta una tabella con colonne diverse rispetto alla tabella corrente, viene visualizzato un messaggio indicante che le colonne sono diverse. Sarà necessario quindi selezionare le colonne che si desidera inserire nella tabella corrente e fare clic su **Salva**. Selezionando la casella di controllo a sinistra della tabella è possibile sostituire l'intera tabella.  
  
> [!NOTE]  
>  Quando si modifica l'origine dati di una tabella, essenzialmente si sostituisce il contenuto della tabella corrente con il contenuto della nuova tabella di origine.  
  
 **Nomi delle colonne**  
 |||  
|-|-|  
|**Origine**|Selezionare questa opzione per sostituire i nomi delle colonne correnti con i nomi delle colonne della tabella di origine selezionata.|  
|**Modello**|Selezionare questa opzione per utilizzare i nomi delle colonne correnti poiché presenti nel modello.|  
  
 **Aggiorna anteprima**  
 Fare clic per visualizzare le colonne di dati nella tabella di origine attualmente selezionata.  
  
 **Passare a**  
 |||  
|-|-|  
|**Anteprima tabella**|Selezionare questa opzione per visualizzare l'anteprima della tabella selezionata e un numero limitato di righe di dati.|  
|**Editor di query**|Selezionare questa opzione per visualizzare la query sull'origine dati selezionata. Questa opzione non è disponibile per tutte le origini dati.|  
  
 **Casella di controllo nell'intestazione di colonna**  
 Selezionare la casella di controllo per includere la colonna nell'importazione dei dati. Deselezionare la casella di controllo per rimuovere la colonna dall'importazione dei dati.  
  
 **Pulsante freccia in giù nell'intestazione di colonna**  
 Consente di filtrare i dati nella colonna.  
  
 **Cancella filtri di riga**  
 Fare clic per rimuovere qualsiasi filtro applicato.  
  
 **OK**  
 Fare clic per applicare tutte le modifiche apportate, inclusa la sostituzione delle colonne.  
  
## <a name="query-design-mode"></a>Modalità Progettazione query  
 **Nome tabella**  
 Visualizza il nome della tabella dati nel modello.  
  
> [!NOTE]  
>  Il nome della tabella non può essere modificato in questo punto, ma facendo clic con il pulsante destro del mouse sulla scheda della tabella nella parte inferiore della finestra di progettazione.  
  
 **Nome connessione**  
 Visualizza il nome della connessione attualmente in uso.  
  
 **Passare a**  
 |||  
|-|-|  
|**Anteprima tabella**|Selezionare questa opzione per visualizzare l'anteprima della tabella selezionata e alcune righe di dati.|  
|**Editor di query**|Selezionare questa opzione per visualizzare la query che sarà eseguita sull'origine dati selezionata.|  
  
 **Istruzione SQL**  
 Visualizza l'istruzione SQL eseguita sull'origine dati corrente per recuperare le righe. Per impostazione predefinita, vengono recuperate tutte le righe, tuttavia è possibile anche recuperare un subset di righe progettando un filtro o modificando manualmente l'istruzione SQL.  
  
 **Validate**  
 Fare clic per verificare che l'istruzione sia sintatticamente corretta per l'origine dati e il provider selezionati.  
  
 **Progetta**  
 Fare clic per aprire una finestra Progettazione query visiva e compilare un'istruzione per la query. Per informazioni sull'utilizzo della finestra di progettazione, premere F1 dalla finestra di progettazione.  
  
 **OK**  
 Fare clic per applicare tutte le modifiche apportate, inclusa la sostituzione delle colonne.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e colonne &#40;SSAS tabulare&#41;](tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
