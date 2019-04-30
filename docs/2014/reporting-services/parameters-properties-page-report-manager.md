---
title: Pagina delle proprietà parametri (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ebb53598-2378-46ae-8935-d5192f8ea49a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f83e66d238aa67b28bf547540c5a6b5dfcc9c92d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188292"
---
# <a name="parameters-properties-page-report-manager"></a>Pagina delle proprietà Parametri (Gestione report)
  La pagina delle proprietà Parametri consente di visualizzare o modificare le impostazioni dei parametri per un report con parametri.  
  
 I parametri vengono specificati nella definizione del report prima della pubblicazione. Dopo la pubblicazione del report è possibile modificare alcuni valori delle proprietà dei parametri. I valori modificabili variano a seconda della modalità di definizione dei parametri nel report. Se per un parametro viene definito un elenco di valori statici, ad esempio, sarà possibile selezionare un diverso valore statico come valore predefinito ma non sarà possibile aggiungere o rimuovere valori nell'elenco. In modo analogo, se il parametro è basato su una query, tutte le caratteristiche della query vengono definite nel report prima della pubblicazione, inclusi il set di dati utilizzato, il supporto di valori Null o vuoti e l'impostazione di un valore predefinito.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-parameters-properties-page"></a>Per aprire la pagina delle proprietà Parametri  
  
1.  Aprire Gestione report, quindi individuare il report per il quale si desidera modificare le impostazioni dei parametri.  
  
2.  Passare con il puntatore del mouse sul report, quindi fare clic sulla freccia a discesa.  
  
3.  Scegliere **Gestisci**dal menu a discesa. Verrà visualizzata la pagina delle proprietà Generale per il report.  
  
4.  Selezionare la scheda **Parametri** . Se la scheda **Parametri** non è disponibile significa che il report non contiene parametri.  
  
## <a name="options"></a>Opzioni  
 **Nome parametro**  
 Indica il nome del parametro.  
  
 **Tipo di dati**  
 Mostra il tipo di dati del parametro.  
  
 **Ha un valore predefinito**  
 Selezionare questa casella di controllo per specificare se il parametro ha un valore predefinito. Se si seleziona questa casella di controllo, viene attivata l'opzione **Valore predefinito**. Se il parametro del report accetta valori Null, viene attivata anche l'opzione **Null** . Se l'opzione **Con valore predefinito** non è selezionata, è necessario nascondere il valore o richiedere all'utente di fornire un valore quando il report viene eseguito.  
  
 **Valore predefinito**  
 Consente di specificare un valore per il parametro. Per specificare un valore predefinito è necessario che la casella di controllo **Con valore predefinito** sia selezionata e che l'opzione **Null** non sia selezionata. È possibile specificare un valore predefinito nella definizione del report. Se per l'opzione **Valore predefinito** sono disponibili uno o più valori statici, tali valori derivano dalla definizione del report. Se l'impostazione dell'opzione **Valore predefinito** è **Basato su query**, il valore del parametro viene determinato da una query definita nel report.  
  
 Se è consentita l'immissione di un valore per **Valore predefinito** , è possibile digitare una costante o un valore con una sintassi valida per l'estensione per l'elaborazione dati utilizzata con il report. Se il linguaggio di query dell'estensione per l'elaborazione dati supporta i caratteri jolly, ad esempio, è possibile specificare un carattere jolly come valore predefinito.  
  
 Se in seguito si imposta l'opzione per la richiesta di un valore all'utente, il valore predefinito diventa il valore iniziale che l'utente può utilizzare o modificare. Se non si imposta la richiesta di un valore per il parametro, questo valore verrà utilizzato per tutti gli utenti che eseguono il report.  
  
 **Null**  
 Selezionare questa casella di controllo per impostare Null come valore predefinito. L'impostazione di un valore Null indica che il report viene eseguito anche se l'utente non fornisce un valore di parametro. Se la colonna non include una casella di controllo, il parametro non accetta valori Null.  
  
 **Nascondi**  
 Selezionare questa casella di controllo per nascondere il parametro nell'area dei parametri disponibile nella parte superiore del report. Il parametro sarà comunque disponibile nelle pagine di definizione della sottoscrizione e potrà essere specificato nell'URL di un report. È consigliabile selezionare questa casella di controllo se si desidera che il report venga sempre eseguito con un valore predefinito specificato.  
  
 Deselezionare questa casella di controllo se si desidera che il parametro venga visualizzato nel report.  
  
 **Richiedere all'utente**  
 Selezionare questa casella di controllo per visualizzare una casella di testo per richiedere agli utenti l'immissione di un valore per il parametro.  
  
 Deselezionare questa casella di controllo se si desidera eseguire il report in modalità automatica (ad esempio per generare snapshot della cronologia dei report o dell'esecuzione del report), se si desidera utilizzare lo stesso valore di parametro per tutti gli utenti oppure se non è necessario l'input dell'utente.  
  
 **Testo da visualizzare**  
 Consente di specificare la stringa di testo visualizzata accanto alla casella di testo del parametro. È possibile specificare un'etichetta o testo descrittivo. Non sono previste limitazioni per la lunghezza della stringa. Le stringhe di testo lunghe vengono mandate a capo nello spazio disponibile.  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina delle proprietà Generale, Report &#40;Gestione report&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Guida sensibile al contesto di Gestione report](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
