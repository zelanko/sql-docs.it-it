---
title: Definire le condizioni di ricerca
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: e1541a4602c53c96dfad36c549bc75c8cf76fae5
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999263"
---
# <a name="specify-search-conditions-visual-database-tools"></a>Definizione di condizioni di ricerca (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
È possibile indicare le righe di dati da inserire nella query specificando delle condizioni di ricerca. Se ad esempio si desidera eseguire una query su una tabella `employee` , è possibile limitare la ricerca ai soli dipendenti che lavorano in una particolare area.  
  
Le condizioni di ricerca vanno specificate mediante un'espressione, che generalmente è costituita da un operatore e da un valore di ricerca. Per trovare, ad esempio, un dipendente di una determinata area di vendita, è possibile specificare il seguente criterio di ricerca nella colonna `region` :  
  
```  
='UK'  
```  
  
> [!NOTE]  
> Se si lavora su più tabelle, in Progettazione query e Progettazione viste verrà esaminata ciascuna condizione di ricerca per stabilire se il confronto avrà come risultato un join. In tal caso, la condizione di ricerca verrà convertita automaticamente in un join. Per altre informazioni, vedere [Unione di tabelle in modo automatico &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/join-tables-automatically-visual-database-tools.md).  
  
### <a name="to-specify-search-conditions"></a>Per specificare le condizioni di ricerca  
  
1.  Se necessario, aggiungere nel riquadro Criteri le colonne o le espressioni da utilizzare nella condizione di ricerca.  
  
    Se si sta creando una query di selezione e si preferisce che le colonne o le espressioni di ricerca non siano visualizzate nell'output della query, deselezionare la colonna **Output** per tutte le colonne o espressioni da rimuovere dall'output.  
  
2.  Individuare la riga contenente la colonna di dati o l'espressione da includere nella ricerca e immettere una condizione di ricerca nella colonna **Filtro** .  
  
    > [!NOTE]  
    > Se non si specifica un operatore, in Progettazione query e Progettazione viste verrà inserito automaticamente l'operatore di uguaglianza "=".  
  
In Progettazione query e Progettazione viste l'istruzione SQL verrà aggiornata nel [riquadro SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) tramite l’aggiunta o la modifica della clausola WHERE.  
  
## <a name="see-also"></a>Vedere anche  
[Regole per l'immissione di valori di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Specifica dei criteri di ricerca &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
