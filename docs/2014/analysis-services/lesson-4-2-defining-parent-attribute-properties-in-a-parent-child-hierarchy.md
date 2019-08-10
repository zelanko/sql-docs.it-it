---
title: Definizione delle proprietà degli attributi padre in una gerarchia padre-figlio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2d78fa73-a13b-4e12-bbd0-43e5307f760c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8688e40fc0075bded60069bea24e8114dd51fa0f
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888383"
---
# <a name="defining-parent-attribute-properties-in-a-parent-child-hierarchy"></a>Definizione delle proprietà degli attributi padre in una gerarchia padre-figlio
  Una gerarchia padre-figlio è una gerarchia in una dimensione basata su due colonne di tabella. Nell'insieme, queste colonne definiscono le relazioni gerarchiche tra i membri della dimensione. La prima colonna, denominata *colonna chiave membro*, identifica ogni membro della dimensione. L'altra colonna, denominata *colonna padre*, identifica l'elemento padre di ogni membro della dimensione. La proprietà **NamingTemplate** di un attributo padre consente di determinare il nome di ogni livello nella gerarchia padre-figlio e la proprietà **MembersWithData** consente di determinare se i dati del membro padre devono essere visualizzati.  
  
 Per ulteriori informazioni, vedere [gerarchia padre-figlio](multidimensional-models/parent-child-dimension.md), [attributi nelle gerarchie padre-figlio](multidimensional-models/parent-child-dimension-attributes.md)  
  
> [!NOTE]  
>  Quando si utilizza la Creazione guidata dimensione per creare una dimensione, vengono riconosciute le tabelle che presentano relazioni padre-figlio e viene definita automaticamente la gerarchia padre-figlio.  
  
 Questo argomento illustra le attività che consentono di creare un modello di denominazione con il quale definire il nome di ogni livello nella gerarchia padre-figlio della dimensione **Employee** . L'attributo padre verrà quindi configurato per nascondere tutti i dati padre in modo da visualizzare solo le vendite dei membri al livello foglia.  
  
## <a name="browsing-the-employee-dimension"></a>Visualizzazione della dimensione Employee  
  
1.  In Esplora soluzioni fare doppio clic su **Employee.dim** nella cartella **Dimensioni** per aprire Progettazione dimensioni per la dimensione Employee.  
  
2.  Fare clic sulla scheda **Esplorazione** e verificare che **Employees** sia selezionato nell'elenco **Gerarchia** ed espandere il membro **All Employees** .  
  
     Si noti che **Ken J. Sánchez** è il responsabile principale in questa gerarchia padre-figlio.  
  
3.  Selezionare il membro **Ken J. Sánchez** .  
  
     Si noti che il nome del livello di questo membro è **Livello 02**. Il nome del livello viene visualizzato dopo **Livello corrente:** immediatamente sopra il membro **All Employees**. Nell'attività successiva verranno definiti nomi più descrittivi per ogni livello.  
  
4.  Espandere **Ken J. Sánchez** per visualizzare i nomi dei dipendenti che fanno riferimento a questo responsabile e selezionare **Brian S. Welcker** per visualizzare il nome di questo livello.  
  
     Si noti che il nome del livello di questo membro è **Livello 03**.  
  
5.  In Esplora soluzioni fare doppio clic su **Analysis Services Tutorial.cube** nella cartella **Cubi** per aprire Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.  
  
6.  Fare clic sulla scheda **Esplorazione** .  
  
7.  Fare clic sull'icona Excel e selezionare **Abilita** quando richiesto per abilitare le connessioni.  
  
8.  Nell'elenco dei campi della tabella pivot espandere **Reseller Sales**. Trascinare **Reseller Sales-Sales Amount** nell'area Valori.  
  
9. Nell'elenco di campi della tabella pivot espandere **Employee**e trascinare la gerarchia **Employees** nell'area **Righe** .  
  
     Tutti i membri della gerarchia Employees verranno aggiunti alla colonna A del report di tabella pivot.  
  
     Nell'immagine seguente viene illustrata la gerarchia Employees espansa.  
  
10. ![Tabella pivot che mostra la gerarchia Employees](../../2014/tutorials/media/l4-employee-1.gif "Tabella pivot che mostra la gerarchia Employees")  
  
     Si noti che le vendite di ogni responsabile nel Livello 03 vengono visualizzate anche nel Livello 04. dal momento che ogni responsabile è anche un dipendente di altri responsabili. Nell'attività successiva gli importi delle vendite verranno nascosti.  
  
## <a name="modifying-parent-attribute-properties-in-the-employee-dimension"></a>Modifica delle proprietà degli attributi padre della dimensione Employee  
  
1.  Passare a Progettazione dimensioni per la dimensione **Employee** .  
  
2.  Fare clic sulla scheda **Struttura dimensione** e selezionare la gerarchia dell'attributo **Employees** nel riquadro **Attributi** .  
  
     Si noti l'icona particolare dell'attributo. Tale icona indica che l'attributo rappresenta la chiave del padre in una gerarchia padre-figlio. Si noti anche che nella finestra Proprietà la proprietà **Usage** è definita come **Padre**. Questa proprietà è stata impostata con la Creazione guidata dimensione durante la progettazione della dimensione. La procedura guidata ha rilevato automaticamente la relazione padre-figlio.  
  
3.  Nella finestra Proprietà fare clic sul pulsante con i puntini di sospensione ( **...** ) nella cella della proprietà **NamingTemplate** .  
  
     Nella finestra di dialogo **Modello denominazione livelli** viene definito il modello di denominazione dei livelli che consente di determinare i nomi dei livelli nella gerarchia padre-figlio visualizzati durante l'esplorazione dei cubi.  
  
4.  Nella seconda riga, ovvero nella riga contenente **\*** , digitare **Employee Level \*** nella colonna **Nome** e fare clic sulla terza riga.  
  
     Si noti che alla voce **Risultato** ogni livello verrà denominato "Employee Level" seguito da un numero progressivo.  
  
     La figura seguente illustrale modifiche apportate nella finestra di dialogo **Modello denominazione livelli** .  
  
     Finestra di ![dialogo Modello denominazione livelli] Finestra di (../../2014/tutorials/media/l4-namingtemplate.gif "dialogo Modello denominazione livelli")  
  
5.  Fare clic su **OK**.  
  
6.  Nella cella della proprietà **MembersWithData** della finestra Proprietà dell'attributo **Employees** selezionare **NonLeafDataHidden** per modificare questo valore per l'attributo **Employees** .  
  
     In questo modo i dati correlati ai membri non a livello foglia nella gerarchia padre-figlio verranno nascosti.  
  
## <a name="browsing-the-employee-dimension-with-the-modified-attributes"></a>Visualizzazione della dimensione Employee con gli attributi modificati  
  
1.  Scegliere **Deploy Analysis Services Tutorial** (Distribuisci Analysis Services Tutorial) dal menu **Compila** di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Dopo aver completato la distribuzione, passare a Progettazione cubi per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial e fare clic sul pulsante **Riconnetti** sulla barra degli strumenti della scheda **Esplorazione** .  
  
3.  Fare clic sull'icona Excel e selezionare **Abilita**.  
  
4.  Trascinare **Reseller Sales-Sales Amount** nell'area Valori.  
  
5.  Trascinare la gerarchia **Employees** nell'area Etichette di riga.  
  
     Nella figura seguente vengono illustrate le modifiche apportate alla gerarchia Employee. Si noti che tephen Y. Jiang non viene più visualizzato come dipendente di se stesso.  
  
     ![Gerarchia Employees modificata](../../2014/tutorials/media/l4-employee-2.png "Gerarchia Employees modificata")  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Raggruppamento automatico dei membri degli attributi](https://docs.microsoft.com/analysis-services/lesson-4-3-automatically-grouping-attribute-members)  
  
## <a name="see-also"></a>Vedere anche  
 [Gerarchia padre-figlio](multidimensional-models/parent-child-dimension.md)   
 [Attributi nelle gerarchie padre-figlio](multidimensional-models/parent-child-dimension-attributes.md)  
  
  
