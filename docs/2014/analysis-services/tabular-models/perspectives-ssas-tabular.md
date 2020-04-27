---
title: Prospettive (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1f78c3a1-ce2c-4e7f-a277-71a657692bea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fcd6e438327d88b79a88b5026f28e24e19fffb5e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66066874"
---
# <a name="perspectives-ssas-tabular"></a>Prospettive (SSAS tabulare)
  Nei modelli tabulari, le prospettive consentono di definire subset visualizzabili di un modello in grado di offrire punti di vista mirati, specifici di un'attività aziendale o di un'applicazione del modello.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_understanding)  
  
-   [Test delle prospettive](#bkmk_testpersp)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="benefits"></a><a name="bkmk_understanding"></a>Vantaggi  
 L'esplorazione dei modelli tabulari può risultare molto complessa per gli utenti. Un singolo modello può rappresentare il contenuto di un data warehouse completo con molte tabelle, misure e dimensioni. Tale complessità può costituire un ostacolo per gli utenti che necessitano solo di interagire con una piccola parte del modello per soddisfare determinati requisiti di Business Intelligence e creazione di report.  
  
 In una prospettiva, tabelle, colonne e misure (indicatori KPI inclusi) vengono definiti come oggetti campo. È possibile selezionare i campi visualizzabili per ogni prospettiva. In un modello possono ad esempio essere contenuti dati del prodotto, delle vendite, finanziari, geografici e dei dipendenti. Mentre un reparto vendite necessita di dati del prodotto, delle vendite, delle promozioni e geografici, non avrà probabilmente bisogno dei dati dei dipendenti e finanziari. In modo analogo, per un reparto risorse umane non sono necessari dati geografici e sulle promozioni di vendita.  
  
 Se un utente si connette a un modello (come origine dati) con prospettive definite, potrà selezionare la prospettiva desiderata. Se ad esempio ci si connette a un'origine dati del modello di Excel, gli utenti del reparto risorse umane potranno selezionare la prospettiva Risorse umane nella pagina Selezione tabelle e viste della Connessione guidata dati. Nell'elenco di campi della tabella pivot verranno visualizzati solo i campi (tabelle, colonne e misure) definiti per la prospettiva Risorse umane.  
  
 Le prospettive non sono pensate per essere utilizzate come meccanismo di sicurezza, ma piuttosto come strumento per migliorare l'esperienza utente. Tutte le impostazioni di sicurezza di una determinata prospettiva vengono ereditate dal modello sottostante. Le prospettive non possono consentire l'accesso agli oggetti del modello se l'utente non dispone già del relativo diritto di accesso. È quindi necessario risolvere la sicurezza del database modello prima di poter fornire l'accesso agli oggetti del modello tramite una prospettiva. I ruoli di sicurezza possono essere utilizzati per proteggere i metadati e i dati del modello. Per altre informazioni, vedere [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md).  
  
##  <a name="testing-perspectives"></a><a name="bkmk_testpersp"></a>Test delle prospettive  
 Quando si crea un modello, è possibile utilizzare la caratteristica Analizza in Excel in Progettazione modelli per eseguire un test circa l'efficacia delle prospettive definite. Se si fa clic su **Analizza in Excel** nel menu **Modello**in Progettazione modelli prima che venga aperto Excel, verrà visualizzata la finestra di dialogo **Scegli credenziali e prospettiva** . In questa finestra di dialogo è possibile specificare il nome utente corrente, un utente diverso, un ruolo e una prospettiva che verranno utilizzati per la connessione al database dell'area di lavoro modello come origine dati nonché per la visualizzazione dei dati.  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare e gestire prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md)|Viene descritto come creare e gestire prospettive utilizzando la finestra di dialogo Prospettive in Progettazione modelli.|  
  
## <a name="see-also"></a>Vedi anche  
 [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md)   
 [Gerarchie &#40;SSAS tabulare&#41;](hierarchies-ssas-tabular.md)  
  
  
