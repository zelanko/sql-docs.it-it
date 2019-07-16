---
title: Definire chiavi primarie logiche in una vista origine dati (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90684f55414fa9e3f0d68a8ec90884fdae4d2c0a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178740"
---
# <a name="define-logical-primary-keys-in-a-data-source-view-analysis-services"></a>Definire chiavi primarie logiche in una vista origine dati (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La Creazione guidata vista origine dati e Progettazione vista origine dati consentono di definire automaticamente una chiave primaria per una tabella che viene aggiunta a una vista origine dati in base alla tabella di database sottostante.  
  
 Talvolta, può essere necessario definire manualmente una chiave primaria nella vista origine dati. Ad esempio, per motivi correlati alle prestazioni o alla progettazione, nelle tabelle di un'origine dati potrebbero non essere incluse colonne chiave primarie definite in modo esplicito. La colonna chiave primaria per una tabella può inoltre essere omessa in viste e query denominate. Se in una tabella, in una vista o in una query denominata non è inclusa una chiave primaria fisica definita, è possibile definire manualmente una chiave primaria logica tramite Progettazione vista origine dati.  
  
## <a name="set-a-logical-primary-key"></a>Impostare una chiave primaria logica  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le chiavi primarie sono necessarie per identificare in modo univoco i record in una tabella, identificare le colonne chiave nelle tabelle delle dimensioni e supportare le relazioni tra tabelle, viste e query denominate. Tali relazioni vengono utilizzate per costruire query per il recupero di dati e metadati dalle origini dati sottostanti e per sfruttare caratteristiche avanzate di Business Intelligence.  
  
 Per la chiave primaria logica è possibile utilizzare qualsiasi colonna, incluso un calcolo denominato. Durante la creazione di una chiave primaria logica, nella vista origine dati viene creato un vincolo UNIQUE contrassegnato come vincolo di chiave primaria. Ogni altra chiave primaria logica esistente specificata nella tabella selezionata verrà eliminata.  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto o connettersi al database contenente la vista origine dati in cui si desidera impostare una chiave primaria logica.  
  
2.  In Esplora soluzioni espandere la cartella **Viste origine dati** e quindi fare doppio clic sulla vista origine dati.  
  
     Per individuare una tabella o una vista, è possibile usare l'opzione **Trova tabella** scegliendola dal menu **Vista origine dati**  o facendo clic con il pulsante destro del mouse su un'area vuota nel riquadro **Tabelle** o **Diagramma** .  
  
3.  Nel riquadro **Tabelle** o **Diagramma** fare clic con il pulsante destro del mouse sulle colonne da usare per definire una chiave primaria logica, quindi scegliere **Imposta chiave primaria logica**.  
  
     L'opzione per impostare una chiave primaria logica è disponibile solo per le tabelle in cui non è inclusa alcuna chiave primaria.  
  
     Una volta impostata la chiave, le colonne chiave primaria saranno identificate da un'icona a forma di chiave.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Definire calcoli denominati in una vista origine dati &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
  
