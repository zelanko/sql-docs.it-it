---
title: Creare e gestire indicatori KPI nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ae17e727367b702967ec879ed8469973ab3b812
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072088"
---
# <a name="create-and-manage-kpis"></a>Creare e gestire indicatori KPI 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive come creare, modificare o eliminare un indicatore KPI (Key Performance Indicator) in un modello tabulare. Per creare un indicatore KPI, si seleziona una misura che restituisca un valore di Base dell'indicatore KPI. Successivamente, utilizzare la finestra di dialogo Indicatore di prestazioni chiave per selezionare una seconda misura o un valore assoluto tramite cui venga restituito un valore di destinazione. È quindi possibile definire le soglie dello stato tramite cui si misurano le prestazioni tra le misure di base e di destinazione.  
  
## <a name="tasks"></a>Attività  
  
> [!IMPORTANT]  
>  Prima di creare un indicatore KPI, è innanzitutto necessario creare una misura di base che consenta la restituzione di un valore. Estendere quindi la misura di base a un indicatore KPI. Come creare le misure sono descritte in un altro argomento, [creare e gestire misure](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md). Un indicatore KPI richiede inoltre un valore di destinazione, che può essere il valore di un'altra misura predefinita o un valore assoluto. Dopo aver esteso una misura di base a un indicatore KPI, sarà possibile selezionare il valore di destinazione e definire le soglie dello stato nella finestra di dialogo Indicatore di prestazioni chiave.  
  
###  <a name="bkmk_create_KPI"></a> Per creare un indicatore KPI  
  
1.  Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che verrà usata come misura di base (valore), quindi scegliere **Crea KPI**.  
  
2.  In **Definisci valore di destinazione** della finestra di dialogo **Indicatore di prestazioni chiave**selezionare una delle opzioni seguenti:  
  
     Selezionare **Misura**, quindi una misura di destinazione dalla casella di riepilogo.  
  
     Selezionare **Valore assoluto**, quindi digitare un valore numerico.  
  
3.  In **Definisci soglie stato**scegliere e trascinare i valori soglia minimo e massimo.  
  
4.  In **Seleziona stile icona**fare clic su un tipo di immagine.  
  
5.  Fare clic su **Descrizioni**, quindi digitare le descrizioni per l'indicatore KPI, il valore, lo stato e la destinazione.  
  
> [!TIP]  
>  È possibile utilizzare la funzionalità Analizza in Excel per testare l'indicatore KPI. Per altre informazioni, vedere [analizza in Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
###  <a name="bkmk_edit_KPI"></a> Per modificare un indicatore KPI  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che viene usata come misura di base (valore) dell'indicatore KPI, quindi scegliere **Modifica impostazioni KPI**.  
  
###  <a name="bkmk_delete"></a> Per eliminare un indicatore KPI e la misura base  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che viene usata come misura di base (valore) dell'indicatore KPI, quindi scegliere **Elimina**.  
  
###  <a name="bkmk_delete_KPI"></a> Per eliminare un indicatore KPI e mantenere la misura base  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che viene usata come misura di base (valore) dell'indicatore KPI, quindi scegliere **Elimina KPI**.  
  
## <a name="alt-shortcuts"></a>Tasti di scelta rapida ALT  
  
|Sezione interfaccia utente|Comando tramite tasto|  
|----------------|-----------------|  
|Misura di base KPI|ALT+B|  
|Stato KPI|ALT+S|  
|Misura|ALT+M|  
|Valore assoluto|ALT+A|  
|Definisci soglie stato|ALT+U|  
|Seleziona stile icona|ALT+I|  
|Tendenza|ALT+T|  
|Descrizioni|ALT+D|  
|Tendenza|ALT+T|  
  
## <a name="see-also"></a>Vedere anche  
 [Indicatori KPI](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Misure](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Creare e managemeasures](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)  
  
  
