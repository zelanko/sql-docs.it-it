---
title: Rappresentazione di join in Progettazione query e Progettazione viste (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL pane [Visual Database Tools]
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 20a99dcb-83bd-4aa6-9139-92e2e5ba4887
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abd8dd7c3c23a13b1cdff7a2d6f76fb99375a641
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63155273"
---
# <a name="how-the-query-and-view-designer-represents-joins-visual-database-tools"></a>Rappresentazione di join in Progettazione query e Progettazione viste (Visual Database Tools)
  Se due o più tabelle sono unite tramite join, in [Progettazione query e Progettazione viste](visual-database-tools.md) il join verrà rappresentato in forma grafica all'interno del [riquadro Diagramma](diagram-pane-visual-database-tools.md) e mediante la sintassi SQL all'interno del [riquadro SQL](sql-pane-visual-database-tools.md).  
  
## <a name="diagram-pane"></a>Riquadro Diagramma  
 Nel riquadro Diagramma verrà visualizzata una linea di join fra le colonne di dati coinvolte nel join. In Progettazione query e Progettazione viste verrà visualizzata una linea di join per ogni condizione di join. La seguente figura mostra, ad esempio, una linea di join fra due tabelle unite in join:  
  
 ![Linea di join che illustra la relazione tra le due tabelle](../../database-engine/media//dv3wbig.gif "Linea di join che illustra la relazione tra le due tabelle")  
  
 Se le tabelle sono unite da più condizioni di join, verranno visualizzate più linee di join, come nel seguente esempio:  
  
 ![Tabelle unite con più di una condizione di join](../../database-engine/media//dv3w9n1.gif "Tabelle unite con più di una condizione di join")  
  
 Se le colonne di dati unite in join non vengono visualizzate, ad esempio perché il rettangolo che rappresenta la tabella o l'oggetto con struttura a tabella è ridotto a icona o il join utilizza un'espressione, in Progettazione query e Progettazione viste viene inserita la linea di join nella barra del titolo del rettangolo che rappresenta la tabella o l'oggetto con struttura a tabella.  
  
 La forma dell'icona al centro della linea di join indica come le tabelle o gli oggetti con struttura a tabella sono uniti in join. Se la clausola di join utilizza un operatore diverso da uguale (=), tale operatore verrà visualizzato nell'icona della linea di join. Nella seguente tabella sono elencate le icone visualizzate nella linea di join.  
  
|**Icona della linea di join**|**Descrizione**|  
|------------------------|---------------------|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbih.gif "Icona di Visual Database Tools")|Inner join (creato con il segno di uguale).|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbii.gif "Icona di Visual Database Tools")|Inner join basato sull'operatore "maggiore di".|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbij.gif "Icona di Visual Database Tools")|Outer join in cui verranno incluse tutte le righe della tabella rappresentata a sinistra, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbik.gif "Icona di Visual Database Tools")|Outer join in cui verranno incluse tutte le righe della tabella rappresentata a destra, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbil.gif "Icona di Visual Database Tools")|Full outer join in cui verranno incluse tutte le righe di entrambe le tabelle, anche se non hanno alcuna corrispondenza nella tabella correlata.|  
  
 I simboli alle estremità della linea di join indicano il tipo di join. Nella seguente tabella sono elencati i tipi di join e le icone visualizzate alle estremità della linea di join.  
  
|**Icona alle estremità di una linea di join**|**Tipo di join**|  
|-----------------------------------|----------------------|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbim.gif "Icona di Visual Database Tools")|Join uno-a-uno.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbin.gif "Icona di Visual Database Tools")|Join uno-a-molti.|  
|![Icona di Visual Database Tools](../../database-engine/media//dv3wbio.gif "Icona di Visual Database Tools")|In Progettazione query e Progettazione viste non è possibile determinare il tipo di join. Questa situazione si verifica perlopiù con join creati manualmente.|  
  
## <a name="sql-pane"></a>riquadro SQL  
 Un join può essere rappresentato in vari modi all'interno di un'istruzione SQL. La sintassi esatta dipende dal database utilizzato e dalla modalità di definizione del join.  
  
 Le opzioni della sintassi per il join di tabelle comprendono:  
  
-   **Qualificatore JOIN per la clausola FROM**.   Le parole chiave INNER e OUTER specificano il tipo di join. La sintassi è quella standard per ANSI 92 SQL.  
  
     Se, ad esempio, si esegue il join delle tabelle `publishers` e `pub_info` in base alla colonna `pub_id` di ciascuna tabella, l'istruzione SQL risultante potrebbe essere simile alla seguente:  
  
    ```  
    SELECT *  
    FROM publishers INNER JOIN pub_info ON  
       publishers.pub_id = pub_info.pub_id  
    ```  
  
     Se si crea un outer join, verranno utilizzate le parole LEFT OUTER o RIGHT OUTER al posto di INNER.  
  
-   **Clausola WHERE che confronta colonne di entrambe le tabelle**.   La clausola WHERE viene utilizzata quando il database non supporta la sintassi JOIN oppure in caso di immissione manuale. Se il join viene creato nella clausola WHERE, nella clausola FROM saranno indicati i nomi di entrambe le tabelle.  
  
     Ad esempio, la seguente istruzione esegue il join delle tabelle `publishers` e `pub_info` .  
  
    ```  
    SELECT *  
    FROM publishers, pub_info  
    WHERE publishers.pub_id = pub_info.pub_id  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire query con join &#40;Visual Database Tools&#41;](query-with-joins-visual-database-tools.md)   
 [Finestra di dialogo Join &#40;Visual Database Tools&#41;](join-dialog-box-visual-database-tools.md)  
  
  
