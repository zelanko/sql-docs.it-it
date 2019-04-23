---
title: Pagina delle proprietà generale, Report parti (gestione Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 93ddce72-31f1-42f7-abd5-8191acbb00c5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 25dc3a8eb075f212728796465fe2d95c460cbebf
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59963317"
---
# <a name="general-properties-page-report-parts-report-manager"></a>Pagina delle proprietà Generale, Parti di report (Gestione report)
  La pagina delle proprietà consente di visualizzare e gestire le proprietà generali per una parte di report.  
  
 In Gestione report non è possibile visualizzare o modificare l'aspetto e la funzionalità della parte di report. Per modificare la progettazione, è necessario utilizzare uno strumento di creazione per aprirla e modificarla e quindi salvarla nel server.  
  
## <a name="navigation"></a>Navigazione  
 Utilizzare la procedura riportata di seguito per navigare fino a questo percorso nell'interfaccia utente.  
  
###### <a name="to-open-the-properties-page-for-a-report-part"></a>Per aprire la pagina delle proprietà per una parte di report  
  
1.  Aprire Gestione report, quindi individuare la parte di report per la quale si desidera configurare le proprietà.  
  
2.  Passare con il puntatore del mouse sulla parte di report, quindi fare clic sulla freccia a discesa.  
  
3.  Nell'elenco a discesa fare clic su **Gestisci**. Verrà visualizzata la pagina delle proprietà Generale.  
  
## <a name="options"></a>Opzioni  
 **Data ultima modifica**  
 Data e ora dell'ultima modifica apportata alle proprietà della parte di report pubblicato nel server o della pubblicazione di una nuova versione della parte di report pubblicato nel server. Di sola lettura.  
  
 **Modificato da**  
 Nome dell'ultimo utente che ha modificato la parte di report. Di sola lettura.  
  
 **Data creazione**  
 Data e ora della pubblicazione iniziale della parte di report pubblicata nel server. Di sola lettura.  
  
 **Creato da**  
 Nome dell'utente che ha originariamente creato la parte di report. Di sola lettura.  
  
 **Dimensione**  
 Specifica le dimensioni file della parte di report. Di sola lettura.  
  
 **Name**  
 Digitare un nome per identificare la parte di report.  
  
 **Descrizione**  
 Vengono fornite informazioni sulla parte di report. La descrizione viene visualizzata nella pagina Contenuto in Gestione report. Tale descrizione può essere utilizzata come testo di ricerca quando si ricercano parti di report da uno strumento di creazione report.  
  
 **Nascondi in visualizzazione elenco**  
 Selezionare questa opzione per fare in modo che la parte di report non venga visualizzato per gli utenti che utilizzano la modalità di visualizzazione Elenco in Gestione report. La modalità di visualizzazione Elenco è il formato di visualizzazione predefinito utilizzato per l'esplorazione della gerarchia di cartelle del server di report. Gli elementi possono essere nascosti nella visualizzazione Elenco ma non nella visualizzazione Dettagli. Se si desidera limitare l'accesso a un elemento, è necessario creare un'assegnazione di ruolo.  
  
 **Tipo**  
 Tipo della parte di report. Di sola lettura.  
  
 **Applica**  
 Salvare le modifiche.  
  
 **Elimina**  
 Consente di rimuovere la parte di report dal database del server di report. L'eliminazione di una parte di report dal server non impedirà l'esecuzione del rendering di report esistenti a cui la parte di report è stata aggiunta.  
  
 **Sposta**  
 Fare clic per aprire la pagina per lo spostamento di elementi per spostare una parte di report all'interno della gerarchia delle cartelle del server di report. Per altre informazioni, vedere [pagina spostamento elementi &#40;gestione Report&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Scarica**  
 Consente di estrarre una copia della definizione della parte di report da salvare come file con estensione rsc. Il file con estensione rsc può essere caricato in una cartella del server di report oppure utilizzato per sostituire una parte di report esistente in una cartella del server di report.  
  
 **Sostituisci**  
 Consente di sostituire la definizione della parte di report con una diversa da un file con estensione rsc.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione di parti di Report](report-design/managing-report-parts.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Pagina Contenuto &#40;Gestione report&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Parti del report &#40;Generatore report e SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Guida F1 di gestione report](../../2014/reporting-services/report-manager-f1-help.md)   
 [Parti del report e set di dati in Generatore report](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
