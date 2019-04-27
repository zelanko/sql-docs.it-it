---
title: Salvare i dati di Data Mining finestra di dialogo risultati di Query (visualizzazione stima modello di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dm.savedataminingqueryresult.f1
helpviewer_keywords:
- Save Data Mining Query Result dialog box
ms.assetid: 112fb527-7466-4fd4-9cf1-75596135648f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6b5c5f74ba8951bae27193b6796f09dcbdb8302
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748003"
---
# <a name="save-data-mining-query-result-dialog-box-mining-model-prediction-view"></a>Finestra di dialogo Salva risultati query di data mining (visualizzazione Stima modello di data mining)
  Utilizzare la finestra di dialogo **Salva risultati query di data mining** per salvare i risultati di una query di data mining in una nuova tabella.  
  
 La nuova tabella verrà creata nel database definito dall'origine dati.  
  
## <a name="options"></a>Opzioni  
 **Data Source**  
 Consente di selezionare un'origine dati nel progetto corrente. Se l'origine dati corretta non esiste, fare clic su **Nuova** per creare una nuova origine dati.  
  
 **Nuova**  
 Consente di avviare la **Creazione guidata origine dati**.  
  
 **Nome tabella**  
 Consente di digitare un nome per la nuova tabella.  
  
 **Sovrascrivi se esistente**  
 Selezionare questa opzione se si desidera sovrascrivere una tabella esistente con lo stesso nome.  
  
 La sovrascrittura della tabella esistente è necessaria se si verificano una o più delle condizioni seguenti:  
  
-   Sono state aggiunte colonne alla query di stima.  
  
-   Sono stati modificati i nomi o i tipi di dati di tutte le colonne nella query di stima.  
  
-   È stata eseguita un'istruzione ALTER nella tabella di destinazione.  
  
 In caso di più colonne con lo stesso nome, ad esempio diverse colonne derivate con il nome di colonna predefinito **Espressione**, è necessario creare un alias per ogni colonna con un nome duplicato. Se i nomi delle colonne non sono univoci, verrà generato un errore quando il progettista tenta di salvare i risultati in SQL Server, in quanto i nomi delle colonne di una tabella devono essere univoci.  
  
 **Aggiungi a vista origine dati**  
 (Facoltativo) Selezionare una vista origine dati inclusa nel progetto per aggiungere la tabella a un'origine dati esistente.  
  
 Questa opzione è utile se si desidera mantenere tutte le tabelle correlate per un modello, ad esempio dati di training, dati di origine di stima e query risultati aggiuntivo alla stessa origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Generatore delle query di stima &#40;Data Mining&#41;](prediction-query-builder-data-mining.md)   
 [Data Mining nuove interfacce Query](data-mining/data-mining-query-tools.md)   
 [Guida di riferimento alle istruzioni DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
