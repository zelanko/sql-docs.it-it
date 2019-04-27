---
title: Dettagli di traduzione (scheda traduzioni, progettazione dimensioni) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.translations.translationpane.tranlationdetails.f1
ms.assetid: 0aa61df3-f2b0-4703-a63b-124da672dcc3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbeaebfc7eab6041bb547f18dacfc01aef3d5117
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756334"
---
# <a name="translation-details-translations-tab-dimension-designer-analysis-services---multidimensional-data"></a>Dettagli di traduzione (Scheda traduzione, Progettazione dimensioni) (Analysis Services –Dati multidimensionali)
  Usare il pannello **Dettagli di traduzione** nella scheda **Traduzioni** di Progettazione dimensioni per definire e gestire le traduzioni relative alla dimensione attualmente selezionata.  
  
 **Per visualizzare il riquadro dettagli di traduzione**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , quindi aprire la dimensione che si desidera utilizzare.  
  
2.  Fare clic sulla scheda **Traduzioni** .  
  
## <a name="options"></a>Opzioni  
 **Lingua predefinita**  
 Consente di impostare i nomi degli oggetti dimensione nella lingua predefinita.  
  
 **Tipo di oggetto**  
 Consente di visualizzare la proprietà che verrà tradotta. Possono essere tradotti soltanto oggetti e proprietà di cui sono stati specificati i valori. È possibile tradurre le proprietà seguenti:  
  
-   Dimension  
  
     Proprietà `Caption` e `AttributeAllMember`  
  
-   attribute  
  
     Proprietà `Caption`, `AttributeHierarchyDisplayFolder` e `NamingTemplate`.  
  
    > [!NOTE]  
    >  La proprietà `NamingTemplate` è disponibile solo per gli attributi padre.  
  
-   Gerarchia  
  
     Proprietà `Caption` e `AllMemberName`  
  
-   Level  
  
     Proprietà `Caption`  
  
 **\<Lingua >**  
 Consente di digitare o selezionare il valore della proprietà dell'oggetto dimensione nella lingua selezionata. Fare clic sul pulsante con i puntini di sospensione (**...**) per visualizzare altre finestre di dialogo, a seconda della proprietà che si sta modificando:  
  
-   Proprietà `NamingTemplate`  
  
     Consente di visualizzare la [Finestra di dialogo Modello denominazione livelli &#40;Analysis Services - Dati multidimensionali&#41;](level-naming-template-dialog-box-analysis-services-multidimensional-data.md).  
  
-   Proprietà `Caption` (per attributi)  
  
     Consente di visualizzare la [Finestra di dialogo Traduzione dati attributo &#40;Analysis Services - Dati multidimensionali&#41;](attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="shortcut-menu"></a>Menu di scelta rapida  
 Se si fa clic con il pulsante destro del mouse su una traduzione nel riquadro **Dettagli di traduzione** , verrà visualizzato un menu di scelta rapida in cui sono disponibili le opzioni seguenti:  
  
 **Nuova traduzione**  
 Selezionare questa opzione per visualizzare la finestra di dialogo **Seleziona lingua** e creare una nuova traduzione. La traduzione verrà visualizzata sotto forma di nuova colonna all'interno della griglia **Dettagli di traduzione** .  
  
 **Elimina traduzione**  
 Selezionare questa opzione per eliminare la traduzione selezionata.  
  
> [!NOTE]  
>  Questa opzione è attivata solo se si fa clic con il pulsate destro del mouse su una cella per eliminare la traduzione.  
  
 **Nuova colonna didascalia**  
 Selezionare questa opzione per visualizzare la finestra di dialogo **Traduzione dati attributo** e definire una nuova colonna di didascalia durante la modifica di un attributo nella griglia **Dettagli di traduzione** . Per abilitare questa opzione, è necessario selezionare una cella di una colonna per la traduzione relativa a un attributo nella griglia **dettagli traduzione**.  
  
> [!NOTE]  
>  Questa opzione è attivata solo se si fa clic con il pulsante destro del mouse su una cella per eliminare la colonna per la traduzione di un attributo.  
  
 **Modifica colonna didascalia**  
 Selezionare per visualizzare la finestra di dialogo **Traduzione dati attributo** e per modificare una colonna di didascalia già esistente durante la modifica di un attributo nella griglia **Dettagli di traduzione** .  
  
> [!NOTE]  
>  Questa opzione è abilitata solo se nella griglia relativa ai **dettagli di traduzione** è selezionata una cella di una colonna per la traduzione contenente una colonna didascalia per un attributo.  
  
 **Elimina colonna didascalia**  
 Selezionare questa opzione per eliminare la colonna di didascalia per l'attributo selezionato nella griglia **Dettagli di traduzione** .  
  
> [!NOTE]  
>  Questa opzione è attivata solo se si fa clic con il pulsante destro del mouse su una cella di una colonna per la traduzione contenente una colonna didascalia per un attributo.  
  
 **Mostra tutti gli attributi**  
 Selezionare o deselezionare questa opzione per attivare o disabilitare la visualizzazione di tutti gli attributi definiti per la dimensione selezionata, inclusi gli attributi per i quali le gerarchie sono disattivate.  
  
## <a name="see-also"></a>Vedere anche  
 [Le traduzioni &#40;progettazione dimensioni&#41; &#40;Analysis Services - dati multidimensionali&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
