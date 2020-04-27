---
title: Definizione di un cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8aa4ac2d-857f-4048-baa0-0f314e207cf6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 167121188939bcf82ed359ac3f8cf7e3aae47635
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079062"
---
# <a name="defining-a-cube"></a>Definizione di un cubo
  La Creazione guidata cubo consente di definire i gruppi di misure e le dimensioni per un cubo. Nell'attività seguente si utilizzerà la Creazione guidata cubo per compilare un cubo.  
  
### <a name="to-define-a-cube-and-its-properties"></a>Per definire un cubo e le relative proprietà  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse su **Cubi**e quindi scegliere **Nuovo cubo**. Verrà visualizzata la Creazione guidata cubo.  
  
2.  Nella pagina **Creazione guidata cubo** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di creazione** verificare che l'opzione **Usa tabelle esistenti** sia selezionata, quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Selezione tabelle del gruppo di misure** verificare che la vista origine dati **Adventure Works DW 2012** sia selezionata.  
  
5.  Fare clic su **Suggerisci** per visualizzare le tabelle consigliate per la creazione di gruppi di misure.  
  
     Nel corso della procedura guidata vengono esaminate le tabelle e viene suggerita **InternetSales** come tabella del gruppo di misure. Le tabelle del gruppo di misure, anche dette tabelle dei fatti, contengono le misure a cui si è interessati, ad esempio il numero di unità vendute.  
  
6.  Fare clic su **Avanti**.  
  
7.  Nella pagina **Selezione misure** esaminare le misure selezionate nel gruppo di misure **Internet Sales** , quindi deselezionare le caselle di controllo per le misure seguenti:  
  
    -   **Promotion Key**  
  
    -   **Currency Key**  
  
    -   **Sales Territory Key**  
  
    -   **Revision Number**  
  
     Per impostazione predefinita, la procedura guidata seleziona come misure tutte le colonne numeriche della tabella dei fatti che non sono collegate a dimensioni. Tuttavia, queste quattro colonne non sono effettive misure. Le prime tre sono valori chiave che collegano la tabella dei fatti alle tabelle delle dimensioni che non sono utilizzate nella versione iniziale di questo cubo.  
  
8.  Fare clic su **Avanti**.  
  
9. Nella pagina **Selezione dimensioni esistenti** assicurarsi che la dimensione **Date** creata in precedenza sia selezionata, quindi fare clic su **Avanti**.  
  
10. Nella pagina **Seleziona nuove dimensioni** selezionare le nuove dimensioni da creare. A tale scopo, verificare che le caselle di controllo **Customer**, **Geography**e **Product** siano selezionate, quindi deselezionare la casella di controllo **InternetSales** .  
  
11. Fare clic su **Avanti**.  
  
12. Nella pagina **Completamento procedura guidata** modificare il nome del cubo in `Analysis Services Tutorial`. Nel riquadro Anteprima è possibile visualizzare il gruppo di misure **InternetSales** e le relative misure. È inoltre possibile visualizzare le dimensioni **Date**, **Customer** e **Product** .  
  
13. Fare clic su **Fine** per completare la procedura guidata.  
  
     In Esplora soluzioni, nel progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial viene visualizzato nella cartella **Cubi** e le dimensioni del database Customer e Product vengono visualizzate nella cartella **Dimensions** . Il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial viene inoltre visualizzato al centro dell'ambiente di sviluppo nella scheda Struttura cubo.  
  
14. Sulla barra degli strumenti della scheda Struttura cubo modificare il livello di **Zoom** portandolo al 50% in modo da poter visualizzare più agevolmente le dimensioni e le tabelle dei fatti del cubo. Si noti che la tabella dei fatti è gialla e le tabelle delle dimensioni sono blu.  
  
15. Scegliere **Salva tutti** dal menu **File**.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Aggiunta di attributi alle dimensioni](lesson-2-3-adding-attributes-to-dimensions.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Cubi nei modelli multidimensionali](multidimensional-models/cubes-in-multidimensional-models.md)   
 [Dimensioni nei modelli multidimensionali](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
