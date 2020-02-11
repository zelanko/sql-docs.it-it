---
title: Impostazione delle relazioni tra attributi in una gerarchia definita dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 456c2a47-d395-45f9-9efa-89f3fa2ac621
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 838185def1d562f51d810cebdf79684f341a5903
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "69493857"
---
# <a name="specifying-attribute-relationships-between-attributes-in-a-user-defined-hierarchy"></a>Impostazione delle relazioni tra gli attributi in una gerarchia definita dall'utente
  Come è già stato illustrato in questa esercitazione, è possibile organizzare le gerarchie degli attributi in livelli all'interno delle gerarchie utente in modo da offrire agli utenti percorsi di navigazione in un cubo. Una gerarchia utente può rappresentare una gerarchia naturale, ad esempio una città, uno stato e un paese, oppure un percorso di navigazione, ad esempio il nome di un dipendente, la funzione e il reparto di appartenenza. Ai fini della navigazione, non esiste differenza tra questi due tipi di gerarchie utente.  
  
 Nel caso di una gerarchia naturale, se vengono definite relazioni tra gli attributi che costituiscono i livelli, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] consente di utilizzare un'aggregazione di un attributo per ottenere i risultati di un attributo correlato. Se non esistono relazioni definite tra gli attributi, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] tutti gli attributi non chiave verranno aggregati dall'attributo chiave. Pertanto, se i dati sottostanti le supportano, è consigliabile definire relazioni tra gli attributi. La definizione di relazioni tra attributi consente di migliorare le prestazioni di elaborazione di dimensioni, partizioni e query. Per altre informazioni, vedere [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md) e [Relazioni tra attributi](multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 Quando si definisce una relazione tra attributi, è possibile specificare se tale reazione è flessibile o rigida. Se viene definita una relazione rigida, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] consente di mantenere le aggregazioni quando la dimensione viene aggiornata. Quando una relazione rigida viene modificata, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene generato un errore durante l'elaborazione se la dimensione non viene elaborata completamente. L'impostazione corretta delle relazioni e delle rispettive proprietà determina un miglioramento delle prestazioni durante l'esecuzione di query e i processi di elaborazione. Per altre informazioni, vedere [definire le relazioni tra attributi](multidimensional-models/attribute-relationships-define.md)e [proprietà della gerarchia utente](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md).  
  
 Nelle attività di questo argomento verranno illustrate le procedure per definire le relazioni tra gli attributi contenuti nelle gerarchie utente naturali del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial. Tali gerarchie includono la gerarchia **Customer Geography** della dimensione **Customer**, la gerarchia **Sales Territory** della dimensione **Sales Territory** , la gerarchia **Product Model Lines** della dimensione **Product** e le gerarchie **Fiscal Date** e **Calendar Date** della dimensione **Date** . Queste gerarchie utente sono tutte gerarchie naturali.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-customer-geography-hierarchy"></a>Definizione delle relazioni tra gli attributi della gerarchia Customer Geography  
  
1.  Passare a Progettazione dimensioni per la dimensione Customer e fare clic sulla scheda **Struttura dimensione** .  
  
     Nel riquadro **Gerarchie** si notino i livelli della gerarchia **Customer Geography** definita dall'utente. Questa gerarchia corrisponde attualmente solo a un percorso di drill-down per gli utenti, in quanto non è stata definita alcuna relazione tra livelli o attributi.  
  
2.  Fare clic sulla scheda **Relazioni tra attributi** .  
  
     Si notino le quattro relazioni tra attributi che collegano gli attributi non chiave nella tabella **Geography** all'attributo chiave nella tabella **Geography** . L'attributo **Geography** è correlato all'attributo **Full Name** . L'attributo **Postal Code** è indirettamente collegato all'attributo **Full Name** tramite l'attributo **Geography** , in quanto **Postal Code** è collegato a **Geography** e **Geography** è collegato a **Full Name** . A questo punto le relazioni tra attributi verranno modificate in modo da non usare l'attributo **Geography** .  
  
3.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Full Name** e scegliere **Nuova relazione tra attributi**.  
  
4.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Full Name**. Impostare **Attributo correlato** su **Postal Code**. Nell'elenco **Tipo di relazione** lasciare il tipo di relazione impostato su **Flessibile** perché le relazioni tra i membri potrebbero cambiare nel corso del tempo.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Nel diagramma viene visualizzata un'icona di avviso perché la relazione è ridondante. La relazione **Full Name** -> **geography**-> **Postal Code** esisteva già ed è appena stata creata la relazione **Full Name** -> **Postal Code**. La relazione **geography**-> **Postal Code** è ora ridondante, quindi verrà rimossa.  
  
6.  Nel riquadro **Relazioni tra attributi** fare clic con il pulsante destro del mouse su **Geography**-> **Postal Code** e selezionare **Elimina**.  
  
7.  Quando viene visualizzata la finestra di dialogo **Elimina oggetti** , fare clic su **OK**.  
  
8.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Postal Code** e scegliere **Nuova relazione tra attributi**.  
  
9. Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Postal Code**. Impostare **Attributo correlato** su **City**. Nell'elenco **Tipo di relazione** lasciare il tipo di relazione impostato su **Flessibile**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     La relazione **geography**-> **City** è ora ridondante, quindi verrà eliminata.  
  
11. Nel riquadro relazioni tra attributi fare clic con il pulsante destro del mouse su **geography**-> **City** , quindi scegliere **Elimina**.  
  
12. Quando viene visualizzata la finestra di dialogo **Elimina oggetti** , fare clic su **OK**.  
  
13. Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **City** e scegliere **Nuova relazione tra attributi**.  
  
14. Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **City**. Impostare **Attributo correlato** su **State-Province**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida** perché la relazione tra una città e uno stato non cambia nel corso del tempo.  
  
15. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
16. Fare clic con il pulsante destro del mouse sulla freccia tra **Geography** e **State-Province** e scegliere **Elimina**.  
  
17. Quando viene visualizzata la finestra di dialogo **Elimina oggetti** , fare clic su **OK**.  
  
18. Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **State-Province** e quindi scegliere **Nuova relazione tra attributi**.  
  
19. Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **State-Province**. Impostare **Attributo correlato** su **Country-Region**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida** perché la relazione tra uno stato-provincia e un paese-regione non cambia nel corso del tempo.  
  
20. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
21. Nel riquadro relazioni tra attributi fare clic con il pulsante destro del mouse su **geography**-> **Country-Region** e scegliere **Elimina**.  
  
22. Quando viene visualizzata la finestra di dialogo **Elimina oggetti** , fare clic su **OK**.  
  
23. Fare clic sulla scheda **Struttura dimensione** .  
  
     Si noti che quando si elimina l'ultima relazione tra l'attributo **Geography** e gli altri attributi, viene eliminato anche l'attributo **Geography** stesso, poiché non viene più utilizzato.  
  
24. Scegliere **Salva tutto**dal menu File.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-sales-territory-hierarchy"></a>Definizione delle relazioni tra gli attributi della gerarchia Sales Territory  
  
1.  Aprire Progettazione dimensioni per la dimensione **Sales Territory** e fare clic sulla scheda **Relazioni tra attributi** .  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Sales Territory Country** e scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Sales Territory Country**. Impostare **Attributo correlato** su **Sales Territory Group**. Nell'elenco **Tipo di relazione** lasciare il tipo di relazione impostato su **Flessibile**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     **Sales Territory Group** è ora collegato a **Sales Territory Country**e **Sales Territory Country** è ora collegato a **Sales Territory Region**. La proprietà **RelationshipType** per ognuna di queste relazioni è impostata su **Flessibile** dal momento che i raggruppamenti delle regioni all'interno di un paese e i raggruppamenti stessi dei paesi possono cambiare nel corso del tempo.  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-product-model-lines-hierarchy"></a>Definizione delle relazioni tra gli attributi della gerarchia Product Model Lines  
  
1.  Aprire Progettazione dimensioni per la dimensione **Product** e fare clic sulla scheda **Relazioni tra attributi** .  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Model Name** e scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Model Name**. Impostare **Attributo correlato** su **Product Line**. Nell'elenco **Tipo di relazione** lasciare il tipo di relazione impostato su **Flessibile**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-fiscal-date-hierarchy"></a>Definizione delle relazioni tra attributi nella gerarchia Fiscal Date  
  
1.  Passare a Progettazione dimensioni per la dimensione **Date** e quindi fare clic sulla scheda **Relazioni tra attributi** .  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Month Name** , quindi scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Month Name**. Impostare **Attributo correlato** su **Fiscal Quarter**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Fiscal Quarter** e scegliere **Nuova relazione tra attributi**.  
  
6.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Fiscal Quarter**. Impostare **Attributo correlato** su **Fiscal Semester**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Fiscal Semester** e scegliere **Nuova relazione tra attributi**.  
  
9. Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Fiscal Semester**. Impostare **Attributo correlato** su **Fiscal Year**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-calendar-date-hierarchy"></a>Definizione delle relazioni tra attributi nella gerarchia Calendar Date  
  
1.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Month Name** , quindi scegliere **Nuova relazione tra attributi**.  
  
2.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Month Name**. Impostare **Attributo correlato** su **Calendar Quarter**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Calendar Quarter** , quindi scegliere **Nuova relazione tra attributi**.  
  
5.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Calendar Quarter**. Impostare **Attributo correlato** su **Calendar Semester**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Calendar Semester** e scegliere **Nuova relazione tra attributi**.  
  
8.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Calendar Semester**. Impostare **Attributo correlato** su **Calendar Year**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="defining-attribute-relationships-for-attributes-in-the-geography-hierarchy"></a>Definizione delle relazioni tra gli attributi della gerarchia Geography  
  
1.  Aprire Progettazione dimensioni per la dimensione Geography e fare clic sulla scheda **Relazioni tra attributi** .  
  
2.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Postal Code** e scegliere **Nuova relazione tra attributi**.  
  
3.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **Postal Code**. Impostare **Attributo correlato** su **City**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Flessibile**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **City** e scegliere **Nuova relazione tra attributi**.  
  
6.  Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **City**. Impostare **Attributo correlato** su **State-Province**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **State-Province** e quindi scegliere **Nuova relazione tra attributi**.  
  
9. Nella finestra di dialogo **Crea relazione tra attributi** l'opzione **Attributo di origine** è impostata su **State-Province**. Impostare **Attributo correlato** su **Country-Region**. Nell'elenco **Tipo di relazione** impostare il tipo di relazione su **Rigida**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Nel diagramma fare clic con il pulsante destro del mouse sull'attributo **Geography Key** e scegliere **Proprietà**.  
  
12. Impostare la proprietà **AttributeHierarchyOptimizedState** su **NotOptimized**, la proprietà **AttributeHierarchyOrdered** su **False**e la proprietà **AttributeHierarchyVisible** su **False**.  
  
13. Scegliere **Salva tutti** dal menu **File**.  
  
14. Scegliere **Distribuisci Analysis Services Tutorial** dal menu [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Compila **di**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Definizione delle proprietà UnknownMember e NullProcessing](lesson-4-7-defining-the-unknown-member-and-null-processing-properties.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Definire relazioni tra attributi](multidimensional-models/attribute-relationships-define.md)   
 [Proprietà delle gerarchie definite dall'utente](multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
