---
title: Definire relazioni logiche in una vista origine dati (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d59812b7e1a427dc00f26c2d583d8cbca45506d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208994"
---
# <a name="define-logical-relationships-in-a-data-source-view-analysis-services"></a>Definire relazioni logiche in una vista origine dati (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Creazione guidata vista origine dati e Progettazione vista origine dati consentono di definire automaticamente le relazioni tra le tabelle aggiunte a una vista origine dati, in base alle relazioni di database sottostanti o ai criteri di corrispondenza nomi specificati.  
  
 Nei casi in cui si utilizzano dati da più origini dati, può essere necessario definire manualmente le relazioni logiche nella vista origine dati per integrare le relazioni definite automaticamente. In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le relazioni sono necessarie per identificare le tabelle dei fatti e delle dimensioni, per costruire query per il recupero di dati e metadati dalle origini dati sottostanti, nonché per sfruttare i vantaggi delle funzionalità avanzate di Business Intelligence.  
  
 In Progettazione vista origine dati è possibile definire i tipi di relazioni seguenti:  
  
-   Una relazione tra due tabelle nella stessa origine dei dati  
  
-   Una relazione tra una tabella e se stessa, come in una relazione padre figlio  
  
-   Una relazione tra una tabella di un'origine dei dati e un'altra tabella di un'origine dati diversa.  
  
> [!NOTE]  
>  Le relazioni definite in una vista origine dati sono logiche e potrebbero non riflettere le relazioni effettive definite nell'origine dati sottostante. In Progettazione vista origine dati è possibile creare relazioni che non esistono nell'origine dei dati sottostante e rimuovere le relazioni create tramite Progettazione vista origine dati dalle relazioni di chiave esterna esistenti nell'origine dei dati sottostante.  
  
 Le relazioni hanno una direzione. Per ogni valore nella colonna di origine esiste un valore corrispondente nella colonna di destinazione. In un diagramma vista origine dati, ad esempio nei diagrammi visualizzati nel riquadro **Diagramma** , una freccia sulla linea tra due tabelle indica la direzione della relazione.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Per aggiungere una relazione tra tabelle, query denominate o viste](#bkmk_addRel)  
  
 [Per visualizzare o modificare una relazione nel riquadro Diagramma](#bkmk_diagrampane)  
  
 [Per visualizzare o modificare una relazione nel riquadro Tabelle](#bkmk_tablespane)  
  
##  <a name="bkmk_addRel"></a> Per aggiungere una relazione tra tabelle, query denominate o viste  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si vuole aggiungere una relazione logica.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** e quindi fare doppio clic sulla vista origine dati per aprirla in **Progettazione vista origine dati**.  
  
3.  Fare clic con il pulsante destro del mouse sulla tabella, sulla query denominata o sulla vista a cui si vuole aggiungere una relazione nel riquadro **Tabelle** e quindi scegliere **Nuova relazione**.  
  
    > [!NOTE]  
    >  Per individuare una tabella, una vista o una query denominata, è possibile usare l'opzione **Trova tabella** scegliendola dal menu **Vista origine dati** o facendo clic con il pulsante destro del mouse su un'area vuota nel riquadro **Tabella** o **Diagramma** .  
  
4.  Nella finestra di dialogo **Specifica relazione** eseguire le operazioni seguenti:  
  
    1.  Selezionare la tabella, la query denominata o la vista appropriata nell'elenco **Tabella di origine (chiave esterna)** .  
  
    2.  Selezionare la tabella, la query denominata o la vista appropriata negli elenchi **Tabella di destinazione (chiave primaria)** .  
  
    3.  Selezionare le colonne negli elenchi **Colonne di origine** e **Colonne di destinazione** per creare una relazione tra le due tabelle.  
  
         Se durante il campionamento dei dati della query denominata, della vista o della tabella sottostante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] rileva che la relazione è stata definita nella direzione errata, ovvero dalla chiave primaria alla chiave esterna anziché dalla chiave esterna alla chiave primaria, verrà richiesto di invertire l'ordine. Per invertire rapidamente l'ordine, fare clic su **Inverti**.  
  
         Viene anche segnalato se [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] rileva che esiste già una relazione per le colonne selezionate. Non è possibile definire relazioni duplicate.  
  
    4.  Facoltativamente, digitare una descrizione per la relazione nella casella **Descrizione** .  
  
##  <a name="bkmk_diagrampane"></a> Per visualizzare o modificare una relazione nel riquadro Diagramma  
  
-   Nel riquadro **Diagramma** di **Progettazione vista origine dati**fare clic con il pulsante destro del mouse sulla relazione da visualizzare e scegliere **Modifica relazione** oppure fare semplicemente doppio clic sulla freccia della relazione.  Usare la finestra di dialogo **Modifica relazione** per modificare la relazione.  
  
##  <a name="bkmk_tablespane"></a> Per visualizzare o modificare una relazione nel riquadro Tabelle  
  
1.  Nel riquadro **Tabelle** di **Progettazione vista origine dati**individuare e quindi espandere la tabella, la vista o la query denominata contenente la relazione da visualizzare o modificare.  
  
2.  Espandere la cartella **Relazioni** .  Le relazioni tra la tabella, la vista o la query denominata selezionata e altre tabelle, viste e query denominate vengono visualizzate con un elenco delle colonne delle relazioni.  
  
3.  Fare clic con il pulsante destro del mouse sulla relazione da modificare e quindi scegliere **Modifica relazione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
