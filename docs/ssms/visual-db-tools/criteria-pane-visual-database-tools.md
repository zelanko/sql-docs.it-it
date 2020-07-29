---
title: Riquadro Criteri
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 6f1df4856844b162560f562e487f970dc1974d04
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999960"
---
# <a name="criteria-pane-visual-database-tools"></a>Riquadro Criteri (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Il riquadro Criteri consente di specificare le opzioni per le query, ad esempio le colonne di dati da visualizzare, come ordinare i risultati e quali righe selezionare, immettendo le proprie scelte in una griglia simile a un foglio di calcolo. Nel riquadro Criteri è possibile specificare quanto segue:  
  
-   Le colonne da visualizzare e gli alias dei nomi delle colonne.  
  
-   La tabella a cui appartiene una colonna.  
  
-   Le espressioni per le colonne calcolate.  
  
-   Il criterio di ordinamento della query.  
  
-   Le condizioni di ricerca.  
  
-   I criteri di raggruppamento, incluse le funzioni di aggregazione da utilizzare per i report di riepilogo.  
  
-   I nuovi valori per le query UPDATE e INSERT INTO.  
  
-   I nomi delle colonne di destinazione per le query INSERT FROM.  
  
Le modifiche apportate nel riquadro Criteri vengono applicate automaticamente anche nei riquadri Diagramma e SQL. In modo analogo, il riquadro Criteri viene aggiornato automaticamente in base alle modifiche apportate negli altri riquadri.  
  
## <a name="about-the-criteria-pane"></a>Informazioni sul riquadro Criteri  
Le righe del riquadro Criteri rappresentano le colonne di dati utilizzate nella query. Le colonne del riquadro Criteri rappresentano invece le opzioni della query.  
  
Le informazioni specifiche visualizzate nel riquadro Criteri dipendono dal tipo di query creato.  
  
Se il riquadro Criteri non è visibile, fare clic con il pulsante destro del mouse sulla finestra di progettazione, scegliere **Riquadro**e fare clic su **Criteri**.  
  
## <a name="options"></a>Opzioni  
  
|**Colonna**|**Tipo di query**|**Descrizione**|  
|--------------|------------------|-------------------|  
|Colonna|Tutti|Visualizza il nome di una colonna di dati utilizzata per la query o l'espressione per una colonna calcolata. Questa colonna è bloccata in modo da essere sempre visibile quando si scorre orizzontalmente.|  
|Alias|SELECT, INSERT FROM, UPDATE, MAKE TABLE|Specifica un nome alternativo per una colonna o il nome che è possibile utilizzare per una colonna calcolata.|  
|Tabella|SELECT, INSERT FROM, UPDATE, MAKE TABLE|Specifica il nome della tabella o dell'oggetto con struttura a tabella per la colonna di dati associata. Questa colonna è vuota per le colonne calcolate.|  
|Output|SELECT, INSERT FROM, MAKE TABLE|Specifica se una colonna di dati viene inserita nell'output della query.<br /><br />Nota: se il database lo consente, è possibile usare una colonna di dati per le clausole di ricerca o di ordinamento senza visualizzarla nel set di risultati.|  
|Tipo di ordinamento|SELECT, INSERT FROM|Specifica che la colonna di dati associata viene utilizzata per ordinare i risultati della query e indica se l'ordinamento è crescente o decrescente.|  
|Ordinamento|SELECT, INSERT FROM|Specifica la priorità di ordinamento delle colonne di dati utilizzate per ordinare il set di risultati. Quando si modifica il criterio di ordinamento di una colonna di dati, il criterio di ordinamento di tutte le altre colonne verrà aggiornato di conseguenza.|  
|Group By|SELECT, INSERT FROM, MAKE TABLE|Specifica che la colonna di dati associata viene utilizzata per creare una query di aggregazione. Questa colonna della griglia viene visualizzata solo se è stato scelto **Raggruppa** dal menu **Strumenti** o se è stata aggiunta una clausola GROUP BY al riquadro SQL.<br /><br />Per impostazione predefinita, il valore di questa colonna è impostato su **Group By**e la colonna fa parte della clausola GROUP BY.<br /><br />Quando ci si sposta in una cella di questa colonna e si seleziona una funzione di aggregazione da applicare alla colonna di dati associata, in base all'impostazione predefinita l'espressione risultante viene aggiunta come colonna di output al set di risultati.|  
|Criteri|Tutti|Specifica una condizione di ricerca (un filtro) per la colonna di dati associata. Immettere un operatore (quello predefinito è "=") e il valore da cercare. Racchiudere i valori di testo tra virgolette singole.<br /><br />Se la colonna di dati associata fa parte di una clausola GROUP BY, l'espressione immessa viene utilizzata per una clausola HAVING.<br /><br />Se si immettono valori per più celle nella colonna della griglia **Criteri**, le condizioni di ricerca risultanti verranno collegate automaticamente con un operatore AND logico.<br /><br />Per specificare più espressioni di condizione di ricerca per un'unica colonna del database, ad esempio (fname > 'A') AND (fname < 'M'), aggiungere due volte la colonna di dati al riquadro Criteri e specificare nella colonna **Criteri** della griglia valori separati per ogni istanza della colonna di dati.|  
|Or...|Tutti|Specifica un'ulteriore espressione di condizione di ricerca per la colonna di dati, collegata alle espressioni precedenti con un operatore OR logico. È possibile aggiungere più colonne **Or...** nella griglia premendo TAB nella colonna **Or...** all'estrema destra.|  
|Accoda|INSERT FROM|Specifica il nome della colonna di dati di destinazione per la colonna di dati associata. Quando si crea una query di accodamento, in Progettazione query e Progettazione viste si tenta di associare l'origine a una colonna di dati di destinazione appropriata. Se non è possibile scegliere una corrispondenza, sarà necessario specificare il nome della colonna.|  
|Nuovo valore|UPDATE, INSERT INTO|Specifica il valore da inserire nella colonna associata. Immettere un valore letterale o un'espressione.|  
  
## <a name="see-also"></a>Vedere anche  
[Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Riquadro Diagramma &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Regole per l'immissione di valori di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Ordinare e raggruppare i risultati delle query &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Riquadro Risultati &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[Riquadro SQL &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  
