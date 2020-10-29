---
description: Riquadro Diagramma (Visual Database Tools)
title: Riquadro Diagramma
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: eaba2d8acd2a0443bfe2ed97fc53b50fcb667629
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439385"
---
# <a name="diagram-pane-visual-database-tools"></a>Riquadro Diagramma (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Il riquadro Diagramma contiene una rappresentazione grafica delle tabelle o degli oggetti con valori di tabella selezionati dalla connessione dati. Mostra inoltre le eventuali relazioni di join da cui sono collegati.  
  
Nel riquadro Diagramma è possibile:  
  
-   Aggiungere o rimuovere tabelle e oggetti con valori di tabella e specificare le colonne di dati per l'output.  
  
-   Creare o modificare i join fra le tabelle e gli oggetti con valore di tabella.  
  
Quando si apporta una modifica nel riquadro Diagramma, i riquadri Criteri e SQL vengono aggiornati di conseguenza. Se ad esempio si seleziona una colonna per l'output nella finestra di una tabella o di un oggetto con valori di tabella nel riquadro Diagramma, in Progettazione query e Progettazione viste la colonna di dati verrà aggiunta al riquadro Criteri e all'istruzione SQL del riquadro SQL.  
  
Nel riquadro Diagramma ogni tabella o oggetto con valori di tabella viene visualizzato all'interno di una finestra separata. L'icona nella barra del titolo di ciascun rettangolo indica il tipo di oggetto rappresentato dal rettangolo, come illustrato nella seguente tabella.  
  
## <a name="options"></a>Opzioni  
**Tabelle**  
Elenca le tabelle che è possibile aggiungere al riquadro Diagramma. Per aggiungere una tabella, selezionarla e fare clic su **Aggiungi** . Per aggiungere contemporaneamente più tabelle, selezionarle e fare clic su **Aggiungi** .  
  
**Visualizzazioni**  
Elenca le viste che è possibile aggiungere al riquadro Diagramma. Per aggiungere una vista, selezionarla e fare clic su **Aggiungi** . Per aggiungere contemporaneamente più viste, selezionarle e fare clic su **Aggiungi** .  
  
**Funzioni**  
Elenca le funzioni definite dall'utente che è possibile aggiungere al riquadro Diagramma. Per aggiungere una funzione, selezionarla e fare clic su **Aggiungi** . Per aggiungere contemporaneamente più funzioni, selezionarle e fare clic su **Aggiungi** .  
  
**Tabelle locali**  
Elenca le tabelle create dalle query anziché le tabelle appartenenti al database  
  
**Sinonimi**  
Elenca i sinonimi che è possibile aggiungere al riquadro Diagramma. Per aggiungere un sinonimo, selezionarlo e fare clic su **Aggiungi** . Per aggiungere contemporaneamente più sinonimi, selezionarli e fare clic su **Aggiungi** .  
  
|Icona|Tipo oggetto|  
|--------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi1.gif":::|Tabella|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi2.gif":::|Query o vista|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi3.gif":::|Tabella collegata|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dvudficon.gif":::|Funzione definita dall'utente|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi5.gif":::|Vista collegata|  
  
Ogni rettangolo mostra le colonne di dati della tabella o dell'oggetto con valori di tabella. Accanto ai nomi delle colonne sono presenti simboli e caselle di controllo che indicano le modalità di utilizzo delle colonne nella query. Le descrizioni comandi forniscono informazioni quali il tipo di dati e la dimensione delle colonne.  
  
Nella seguente tabella sono elencati i simboli e le caselle di controllo utilizzati nel rettangolo per ogni tabella o oggetto con valori di tabella.  
  
|Casella di controllo o simbolo|Descrizione|  
|-----------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi7.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi8.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi9.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbia.gif":::|Specifica se una colonna di dati viene visualizzata nel set di risultati di una query di selezione o viene utilizzata in una query di aggiornamento, accodamento, creazione tabella o accodamento valori. Per aggiungere la colonna ai risultati è sufficiente selezionarla. Se si è selezionato **(Tutte le colonne)** , nell'output verranno visualizzate tutte le colonne di dati.<br /><br />L'icona utilizzata con la casella di controllo varia in base al tipo di query creato. Quando si crea una query di eliminazione, non è possibile selezionare singole colonne.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbib.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbic.gif":::|Indica che la colonna di dati viene utilizzata per ordinare i risultati della query (ovvero fa parte di una clausola ORDER BY). L'icona indica A-Z se l'ordinamento è crescente o Z-A se l'ordinamento è decrescente.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbid.gif":::|Indica che la colonna di dati viene utilizzata per creare un set di risultati raggruppato (ovvero fa parte di una clausola GROUP BY) in una query di aggregazione.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbie.gif":::|Indica che la colonna di dati è inclusa in una condizione di ricerca per la query (ovvero fa parte di una clausola WHERE o HAVING).|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbif.gif":::|Indica che il contenuto della colonna di dati viene riepilogato per l'output (ovvero è incluso in una funzione SUM, AVG o un'altra funzione di aggregazione).|  
  
> [!NOTE]  
> Se non si dispone di diritti di accesso sufficienti o se il driver di database non è in grado di restituire le informazioni necessarie, in Progettazione query e Progettazione viste non verrà visualizzata alcuna colonna di dati per una tabella o oggetto con valori di tabella. In tali situazioni viene visualizzata solo la barra del titolo della tabella o dell'oggetto con struttura a tabella.  
  
## <a name="joined-tables-on-the-diagram-pane"></a>Join di tabelle nel riquadro Diagramma  
Se la query implica un join, verrà visualizzata una linea di join fra le colonne di dati coinvolte nel join. Se le colonne di dati coinvolte nel join non vengono visualizzate, ad esempio perché la finestra della tabella o dell'oggetto con valori di tabella è ridotta a icona o il join utilizza un'espressione, in Progettazione query e Progettazione viste la linea di join viene inserita nella barra del titolo del rettangolo che rappresenta la tabella o l'oggetto con valori di tabella. In Progettazione query e Progettazione viste verrà visualizzata una linea di join per ogni condizione di join.  
  
La forma dell'icona al centro della linea di join indica come le tabelle o gli oggetti con struttura a tabella sono uniti in join. Se la clausola di join utilizza un operatore diverso da uguale (=), tale operatore verrà visualizzato nell'icona della linea di join. Nella seguente tabella sono elencate le icone che possono essere visualizzate in una linea di join.  
  
|Icona della linea di join|Descrizione|  
|------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbih.gif":::|Inner join (creato con il segno di uguale).|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbii.gif":::|Inner join basato sull'operatore "maggiore di". L'operatore visualizzato nell'icona della linea di join corrisponde all'operatore utilizzato nel join.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbij.gif":::|Outer join in cui verranno incluse tutte le righe della tabella rappresentata a sinistra, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbik.gif":::|Outer join in cui verranno incluse tutte le righe della tabella rappresentata a destra, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbil.gif":::|Full outer join in cui verranno incluse tutte le righe di entrambe le tabelle, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
  
Le icone alle estremità della linea di join indicano il tipo di join. Nella seguente tabella sono elencati i tipi di join e le icone che possono essere visualizzate alle estremità della linea di join.  
  
|Icona alle estremità di una linea di join|Descrizione|  
|-----------------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbim.gif":::|Join uno-a-uno|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbin.gif":::|Join uno-a-molti|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbio.gif ":::|In Progettazione query e Progettazione viste non è possibile determinare il tipo di join|  
  
## <a name="see-also"></a>Vedere anche  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Riquadro Criteri &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
