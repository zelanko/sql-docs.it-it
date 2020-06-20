---
title: Aprire Progettazione query e Progettazione viste (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: e0459679a9be1d124a7c9dfacaebe7f1a2e02d34
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85001196"
---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>Aprire Progettazione query e Progettazione viste (Visual Database Tools)
  Progettazione query e Progettazione viste viene aperto quando si apre la definizione di una vista, si visualizzano i risultati di una query o di una vista oppure si crea o si apre una query. È costituito da quattro riquadri separati:  
  
-   Il riquadro Diagramma contiene una rappresentazione grafica delle tabelle o degli oggetti con valori di tabella selezionati dalla connessione dati. Mostra inoltre le eventuali relazioni di join da cui sono collegati.  
  
-   Il riquadro Criteri consente di specificare le opzioni per le query, ad esempio le colonne di dati da visualizzare, come ordinare i risultati e quali righe selezionare, immettendo le proprie scelte in una griglia simile a un foglio di calcolo.  
  
-   Utilizzando il riquadro SQL è possibile creare un'istruzione SQL personalizzata. Per creare un'istruzione, è anche possibile utilizzare i riquadri Criteri e Diagramma, ma in questo caso le istruzioni SQL verranno comunque create nel riquadro SQL. Mentre si compila la query, il riquadro SQL viene aggiornato e riformattato automaticamente in modo da semplificarne la lettura.  
  
-   Nel riquadro Risultati vengono visualizzati i risultati dell'ultima query di selezione (Select) eseguita. I risultati di altri tipi di query vengono visualizzati in finestre di messaggio.  
  
-   Questi riquadri sono utili mentre si lavora sia nel caso delle query che delle viste.  
  
-   Quando si apre una vista o una query, vengono aperti anche alcuni o tutti i riquadri, a seconda delle impostazioni effettuate nella finestra di dialogo **Opzioni** e del sistema di gestione di database a cui si è connessi. Per impostazione predefinita, vengono aperti tutti e quattro i riquadri.  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>Per aprire Progettazione query e Progettazione viste per una vista  
  
1.  In Esplora oggetti, fare clic con il pulsante destro del mouse sulla vista da aprire e selezionare **Progetta** o **Apri vista**.  
  
     Se si sceglie **Progetta**, i riquadri di Progettazione query e Progettazione viste verranno visualizzati in base alle opzioni selezionate nella finestra di dialogo **Opzioni** . Se invece si sceglie **Apri vista**, per impostazione predefinita verrà visualizzato solo il riquadro Risultati.  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>Per aprire Progettazione query e Progettazione viste per una query esistente  
  
1.  In Esplora soluzioni espandere la cartella **Query** .  
  
2.  Fare doppio clic sulla query che si desidera aprire.  
  
3.  Evidenziare le istruzioni della query, fare clic con il pulsante destro del mouse sull'area evidenziata e scegliere **Progetta query in Editor**.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Strumenti di progettazione di query e viste &#40;Visual Database Tools&#41;](query-and-view-designer-tools-visual-database-tools.md)  
  
  
