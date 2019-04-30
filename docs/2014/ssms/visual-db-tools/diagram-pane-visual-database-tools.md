---
title: Riquadro Diagramma (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 79ddfb40d33c8585b94ccc9718100e771da5e92e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126598"
---
# <a name="diagram-pane-visual-database-tools"></a>Riquadro Diagramma (Visual Database Tools)
  Il riquadro Diagramma contiene una rappresentazione grafica delle tabelle o degli oggetti con valori di tabella selezionati dalla connessione dati. Mostra inoltre le eventuali relazioni di join da cui sono collegati.  
  
 Nel riquadro Diagramma è possibile:  
  
-   Aggiungere o rimuovere tabelle e oggetti con valori di tabella e specificare le colonne di dati per l'output.  
  
-   Creare o modificare i join fra le tabelle e gli oggetti con valore di tabella.  
  
 Quando si apporta una modifica nel riquadro Diagramma, i riquadri Criteri e SQL vengono aggiornati di conseguenza. Se ad esempio si seleziona una colonna per l'output nella finestra di una tabella o di un oggetto con valori di tabella nel riquadro Diagramma, in Progettazione query e Progettazione viste la colonna di dati verrà aggiunta al riquadro Criteri e all'istruzione SQL del riquadro SQL.  
  
 Nel riquadro Diagramma ogni tabella o oggetto con valori di tabella viene visualizzato all'interno di una finestra separata. L'icona nella barra del titolo di ciascun rettangolo indica il tipo di oggetto rappresentato dal rettangolo, come illustrato nella seguente tabella.  
  
## <a name="options"></a>Opzioni  
 **Tabelle**  
 Elenca le tabelle che è possibile aggiungere al riquadro Diagramma. Per aggiungere una tabella, selezionarla e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più tabelle, selezionarle e fare clic su **Aggiungi**.  
  
 **Viste**  
 Elenca le viste che è possibile aggiungere al riquadro Diagramma. Per aggiungere una vista, selezionarla e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più viste, selezionarle e fare clic su **Aggiungi**.  
  
 **Funzioni**  
 Elenca le funzioni definite dall'utente che è possibile aggiungere al riquadro Diagramma. Per aggiungere una funzione, selezionarla e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più funzioni, selezionarle e fare clic su **Aggiungi**.  
  
 **Tabelle locali**  
 Elenca le tabelle create dalle query anziché le tabelle appartenenti al database  
  
 **Sinonimi**  
 Elenca i sinonimi che è possibile aggiungere al riquadro Diagramma. Per aggiungere un sinonimo, selezionarlo e fare clic su **Aggiungi**. Per aggiungere contemporaneamente più sinonimi, selezionarli e fare clic su **Aggiungi**.  
  
|Icona|Tipo oggetto|  
|----------|-----------------|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbi1.gif "Icona di Visual Database Tools")|Tabella|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbi2.gif "Icona di Visual Database Tools")|Query o vista|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbi3.gif "Icona di Visual Database Tools")|Tabella collegata|  
|![Icona di Visual Database Tools](../../database-engine/media//dvudficon.gif "Icona di Visual Database Tools")|Funzione definita dall'utente|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbi5.gif "Icona di Visual Database Tools")|Vista collegata|  
  
 Ogni rettangolo mostra le colonne di dati della tabella o dell'oggetto con valori di tabella. Accanto ai nomi delle colonne sono presenti simboli e caselle di controllo che indicano le modalità di utilizzo delle colonne nella query. Le descrizioni comandi forniscono informazioni quali il tipo di dati e la dimensione delle colonne.  
  
 Nella seguente tabella sono elencati i simboli e le caselle di controllo utilizzati nel rettangolo per ogni tabella o oggetto con valori di tabella.  
  
|Casella di controllo o simbolo|Descrizione|  
|-------------------------|-----------------|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbi7.gif "Icona di Visual Database Tools")<br /><br /> ![Icona di Visual Database Tools](../../database-engine/media//dv3wbi8.gif "Icona di Visual Database Tools")<br /><br /> ![Icona di Visual Database Tools](../../database-engine/media//dv3wbi9.gif "Icona di Visual Database Tools")<br /><br /> ![Icona di Visual Database Tools](../../database-engine/media//dv3wbia.gif "Icona di Visual Database Tools")|Specifica se una colonna di dati viene visualizzata nel set di risultati di una query di selezione o viene utilizzata in una query di aggiornamento, accodamento, creazione tabella o accodamento valori. Per aggiungere la colonna ai risultati è sufficiente selezionarla. Se si è selezionato **(Tutte le colonne)** , nell'output verranno visualizzate tutte le colonne di dati.<br /><br /> L'icona utilizzata con la casella di controllo varia in base al tipo di query creato. Quando si crea una query di eliminazione, non è possibile selezionare singole colonne.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbib.gif "Icona di Visual Database Tools")<br /><br /> ![Icona di Visual Database Tools](../../database-engine/media//dv3wbic.gif "Icona di Visual Database Tools")|Indica che la colonna di dati viene utilizzata per ordinare i risultati della query (ovvero fa parte di una clausola ORDER BY). L'icona indica A-Z se l'ordinamento è crescente o Z-A se l'ordinamento è decrescente.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbid.gif "Icona di Visual Database Tools")|Indica che la colonna di dati viene utilizzata per creare un set di risultati raggruppato (ovvero fa parte di una clausola GROUP BY) in una query di aggregazione.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbie.gif "Icona di Visual Database Tools")|Indica che la colonna di dati è inclusa in una condizione di ricerca per la query (ovvero fa parte di una clausola WHERE o HAVING).|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbif.gif "Icona di Visual Database Tools")|Indica che il contenuto della colonna di dati viene riepilogato per l'output (ovvero è incluso in una funzione SUM, AVG o un'altra funzione di aggregazione).|  
  
> [!NOTE]  
>  Se non si dispone di diritti di accesso sufficienti o se il driver di database non è in grado di restituire le informazioni necessarie, in Progettazione query e Progettazione viste non verrà visualizzata alcuna colonna di dati per una tabella o oggetto con valori di tabella. In tali situazioni viene visualizzata solo la barra del titolo della tabella o dell'oggetto con struttura a tabella.  
  
## <a name="joined-tables-on-the-diagram-pane"></a>Join di tabelle nel riquadro Diagramma  
 Se la query implica un join, verrà visualizzata una linea di join fra le colonne di dati coinvolte nel join. Se le colonne di dati coinvolte nel join non vengono visualizzate, ad esempio perché la finestra della tabella o dell'oggetto con valori di tabella è ridotta a icona o il join utilizza un'espressione, in Progettazione query e Progettazione viste la linea di join viene inserita nella barra del titolo del rettangolo che rappresenta la tabella o l'oggetto con valori di tabella. In Progettazione query e Progettazione viste verrà visualizzata una linea di join per ogni condizione di join.  
  
 La forma dell'icona al centro della linea di join indica come le tabelle o gli oggetti con struttura a tabella sono uniti in join. Se la clausola di join utilizza un operatore diverso da uguale (=), tale operatore verrà visualizzato nell'icona della linea di join. Nella seguente tabella sono elencate le icone che possono essere visualizzate in una linea di join.  
  
|Icona della linea di join|Descrizione|  
|--------------------|-----------------|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbih.gif "Icona di Visual Database Tools")|Inner join (creato con il segno di uguale).|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbii.gif "Icona di Visual Database Tools")|Inner join basato sull'operatore "maggiore di". L'operatore visualizzato nell'icona della linea di join corrisponde all'operatore utilizzato nel join.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbij.gif "Icona di Visual Database Tools")|Outer join in cui verranno incluse tutte le righe della tabella rappresentata a sinistra, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbik.gif "Icona di Visual Database Tools")|Outer join in cui verranno incluse tutte le righe della tabella rappresentata a destra, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbil.gif "Icona di Visual Database Tools")|Full outer join in cui verranno incluse tutte le righe di entrambe le tabelle, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
  
 Le icone alle estremità della linea di join indicano il tipo di join. Nella seguente tabella sono elencati i tipi di join e le icone che possono essere visualizzate alle estremità della linea di join.  
  
|Icona alle estremità di una linea di join|Descrizione|  
|-------------------------------|-----------------|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbim.gif "Icona di Visual Database Tools")|Join uno-a-uno|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbin.gif "Icona di Visual Database Tools")|Join uno-a-molti|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbio.gif "Icona di Visual Database Tools")|In Progettazione query e Progettazione viste non è possibile determinare il tipo di join|  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per le query e visualizzazioni di progettazione &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Riquadro Criteri &#40;Visual Database Tools&#41;](criteria-pane-visual-database-tools.md)   
 [Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
