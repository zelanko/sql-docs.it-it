---
title: Editor form KPI (scheda KPI, Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpidefinitionpane.f1
ms.assetid: 45c6453a-bbe2-4ca5-836e-c7ef11cfcb65
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca81dda4ce34a498aa471ceed5ea86729b1df508
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079445"
---
# <a name="kpi-form-editor-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor form KPI (scheda KPI, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro **Editor form KPI** della scheda **KPI** in Progettazione cubi per creare o modificare l'indicatore di prestazioni chiave (KPI) selezionato.  
  
> [!NOTE]  
>  Questo riquadro viene visualizzato solo in visualizzazione Form.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Consente di digitare il nome dell'indicatore KPI.  
  
 **Gruppo di misure associato**  
 Consente di selezionare il gruppo di misure associato all'indicatore KPI. Queste informazioni possono essere utilizzate dall'applicazione client per determinare quali dimensioni sono disponibili quando l'utente visualizza l'indicatore KPI.  
  
 **Espressione valore**  
 Espandere questa casella per visualizzare o modificare l'espressione MDX (Multidimensional Expression) per il valore dell'indicatore KPI.  
  
 Digitare l'espressione MDX che restituisce il valore dell'indicatore KPI.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 **Espressione obiettivo**  
 Espandere questa casella per visualizzare o modificare l'espressione MDX per il valore obiettivo dell'indicatore KPI.  
  
 Digitare l'espressione MDX che restituisce il valore obiettivo dell'indicatore KPI quando questo viene eseguito.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 **Stato**  
 Espandere questa casella per visualizzare le opzioni **Icona stato** ed **Espressione stato** .  
  
 **Icona stato**  
 Consente di selezionare l'icona che deve essere utilizzata dall'applicazione client per rappresentare graficamente il valore di stato.  
  
> [!NOTE]  
>  L'applicazione client può supportare l'icona selezionata o sostituirla con un'alternativa adatta.  
  
 **Espressione stato**  
 Consente di digitare l'espressione MDX che restituisce il valore di stato dell'indicatore KPI quando questo viene eseguito.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 È consigliabile che questa espressione restituisca un numero decimale compreso tra-1 e 1. Un numero minore rappresenta una situazione negativa, mentre numero maggiore rappresenta una situazione positiva.  
  
> [!NOTE]  
>  I valori inferiori a-1 e superiori a 1 sono possibili ma non possono essere interpretati correttamente da applicazioni client di terze parti.  
  
 **Tendenza**  
 Espandere questa casella per visualizzare le opzioni **Icona tendenza** ed **Espressione tendenza** .  
  
 **Icona tendenza**  
 Consente di selezionare l'icona che deve essere utilizzata dall'applicazione client per rappresentare graficamente il valore di tendenza.  
  
> [!NOTE]  
>  L'applicazione client può supportare l'icona selezionata o sostituirla con un'alternativa adatta.  
  
 **Espressione tendenza**  
 Consente di digitare l'espressione MDX che restituisce il valore di tendenza dell'indicatore KPI.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 L'espressione di tendenza può essere basata su qualsiasi criterio temporale adatto al contesto aziendale. È consigliabile che questa espressione restituisca un numero decimale compreso tra-1 e 1. Un numero minore rappresenta una tendenza negativa nel tempo, mentre un numero maggiore rappresenta una tendenza positiva nel tempo.  
  
> [!NOTE]  
>  I valori inferiori a-1 e superiori a 1 sono possibili ma non possono essere interpretati correttamente da applicazioni client di terze parti.  
  
 **Proprietà aggiuntive**  
 Espandere questa casella per visualizzare le opzioni **Cartella di visualizzazione**, **KPI padre**, **Membro temporale corrente**, **Peso**e **Descrizione** .  
  
 **Cartella di visualizzazione**  
 Consente di digitare la categorizzazione dell'indicatore KPI che deve essere utilizzata dall'applicazione client per la visualizzazione.  
  
 Usare una barra rovesciata (\\) per separare i nomi delle cartelle in una cartella di visualizzazione e il punto e virgola (;) per separare più cartelle di visualizzazione. Ad esempio digitare `Category\Goal\Scientific;Category\Goal\Metric`.  
  
 **KPI padre**  
 Consente di selezionare un indicatore KPI esistente sotto il quale categorizzare gli indicatori KPI che devono essere utilizzati dall'applicazione client.  
  
> [!NOTE]  
>  Se questa opzione è impostata su un indicatore KPI esistente, l'opzione **Cartella di visualizzazione** viene ignorata.  
  
 **Membro temporale corrente**  
 Consente di digitare l'espressione MDX che restituisce il membro che identifica il contesto temporale dell'indicatore KPI.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
> [!IMPORTANT]  
>  L'espressione MDX deve restituire il nome univoco di un membro all'interno di una dimensione temporale associata al gruppo di misure specificato in **Gruppo di misure associato**.  
  
 **Peso**  
 Espandere questa casella per visualizzare o modificare l'espressione MDX per il fattore di ponderazione dell'indicatore KPI.  
  
 Trascinare gli elementi selezionati dal riquadro **Strumenti di calcolo** alla casella di questa opzione per includere la sintassi MDX per l'elemento selezionato.  
  
 **Descrizione**  
 Consente di digitare una descrizione facoltativa dell'indicatore KPI.  
  
## <a name="see-also"></a>Vedi anche  
 [Indicatori KPI &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
