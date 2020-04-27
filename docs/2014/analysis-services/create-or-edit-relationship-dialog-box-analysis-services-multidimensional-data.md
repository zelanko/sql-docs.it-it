---
title: Finestra di dialogo Crea relazione o modifica relazione (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createrelationship.f1
helpviewer_keywords:
- Create Relationship dialog box
ms.assetid: da3c7074-623e-4ddf-a707-d3276a47cf1c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de19592ec5a94e99cc87c40dac476e75546c7968
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086781"
---
# <a name="create-or-edit-relationship-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Crea relazione o Modifica relazione (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Create/Edit Relationship** (Crea/Modifica relazione) in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per definire o modificare una relazione in una vista origine dati. È possibile visualizzare la finestra di dialogo **Create/Edit Relationship** (Crea/Modifica relazione) nei modi seguenti:  
  
-   Fare clic su **Nuova relazione** nel riquadro **Barra degli strumenti** di **Data Source View Designer**(Progettazione vista origine dati).  
  
-   Fare clic con il pulsante destro del mouse su una tabella nel riquadro **Tabelle** o nel riquadro **Diagramma** di **Data Source View Designer** (Progettazione vista origine dati) e selezionare **Nuova relazione**.  
  
-   Fare clic con il pulsante destro del mouse su una relazione nel riquadro **Diagramma** di **Data Source View Designer** (Progettazione vista origine dati) e selezionare **Modifica relazione**.  
  
> [!NOTE]  
>  In **Data Source View Designer** (Progettazione vista origine dati) è possibile creare relazioni che non esistono nell'origine dei dati sottostante e rimuovere le relazioni create tramite **Data Source View Designer** (Progettazione vista origine dati) dalle relazioni di chiave esterna esistenti nell'origine dei dati sottostante.  
  
## <a name="options"></a>Opzioni  
 **Tabella di origine (chiave esterna)**  
 Consente di selezionare la tabella o la query denominata contenente il riferimento a una o più colonne nella tabella di destinazione.  
  
 **Tabella di destinazione (chiave primaria)**  
 Consente di selezionare la tabella contenente una o più colonne a cui fa riferimento la tabella di origine. Per i self join, selezionare la stessa tabella selezionata in **Tabella di origine (chiave esterna)**.  
  
 **Colonne di origine**  
 Consente di selezionare le colonne che fanno riferimento alle colonne nella tabella di destinazione.  
  
 **Colonne di destinazione**  
 Consente di selezionare le colonne a cui fanno riferimento le colonne nella tabella di origine.  
  
 **Inverso**  
 Fare clic su questa opzione per invertire la direzione della relazione.  
  
 **Descrizione**  
 Consente di digitare una descrizione facoltativa per la relazione.  
  
## <a name="see-also"></a>Vedi anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Progettazione vista origine dati &#40;Analysis Services - Dati multidimensionali&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
