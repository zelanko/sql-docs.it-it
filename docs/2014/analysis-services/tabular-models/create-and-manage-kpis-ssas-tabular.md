---
title: Creare e gestire indicatori KPI (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc0bd941392c208ad693be21a391d7b9e3f587a1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067505"
---
# <a name="create-and-manage-kpis-ssas-tabular"></a>Creare e gestire indicatori KPI (SSAS tabulare)
  In questo argomento viene descritto come creare, modificare o eliminare un indicatore di prestazioni chiave (KPI) in un modello tabulare. Per creare un indicatore KPI, si seleziona una misura che restituisca un valore di Base dell'indicatore KPI. Successivamente, utilizzare la finestra di dialogo Indicatore di prestazioni chiave per selezionare una seconda misura o un valore assoluto tramite cui venga restituito un valore di destinazione. È quindi possibile definire le soglie dello stato tramite cui si misurano le prestazioni tra le misure di base e di destinazione.  
  
 In questo argomento sono incluse le attività seguenti:  
  
-   [Per creare un indicatore KPI](#bkmk_create_KPI)  
  
-   [Per modificare un indicatore KPI](#bkmk_edit_KPI)  
  
-   [Per eliminare un indicatore KPI e la misura base](#bkmk_delete)  
  
-   [Per eliminare un indicatore KPI e mantenere la misura base](#bkmk_delete_KPI)  
  
## <a name="tasks"></a>Attività  
  
> [!IMPORTANT]  
>  Prima di creare un indicatore KPI, è innanzitutto necessario creare una misura di base che consenta la restituzione di un valore. Estendere quindi la misura di base a un indicatore KPI. La procedura per creare misure è descritta in un altro argomento, [Create and Manage Measures &#40;SSAS Tabular&#41;](measures-ssas-tabular.md). Un indicatore KPI richiede inoltre un valore di destinazione, che può essere il valore di un'altra misura predefinita o un valore assoluto. Dopo aver esteso una misura di base a un indicatore KPI, sarà possibile selezionare il valore di destinazione e definire le soglie dello stato nella finestra di dialogo Indicatore di prestazioni chiave.  
  
###  <a name="bkmk_create_KPI"></a> Per creare un indicatore KPI  
  
1.  Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che verrà usata come misura di base (valore), quindi scegliere **Crea KPI**.  
  
2.  In **Definisci valore di destinazione** della finestra di dialogo **Indicatore di prestazioni chiave**selezionare una delle opzioni seguenti:  
  
     Selezionare **Misura**, quindi una misura di destinazione dalla casella di riepilogo.  
  
     Selezionare **Valore assoluto**, quindi digitare un valore numerico.  
  
3.  In **Definisci soglie stato**scegliere e trascinare i valori soglia minimo e massimo.  
  
4.  In **Seleziona stile icona**fare clic su un tipo di immagine.  
  
5.  Fare clic su **Descrizioni**, quindi digitare le descrizioni per l'indicatore KPI, il valore, lo stato e la destinazione.  
  
> [!TIP]  
>  È possibile utilizzare la funzionalità Analizza in Excel per testare l'indicatore KPI. Per altre informazioni, vedere la sezione [Analizzare in Excel &#40;SSAS tabulare&#41;](analyze-in-excel-ssas-tabular.md).  
  
###  <a name="bkmk_edit_KPI"></a> Per modificare un indicatore KPI  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che viene usata come misura di base (valore) dell'indicatore KPI, quindi scegliere **Modifica impostazioni KPI**.  
  
###  <a name="bkmk_delete"></a> Per eliminare un indicatore KPI e la misura base  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che viene usata come misura di base (valore) dell'indicatore KPI, quindi scegliere **Elimina**.  
  
###  <a name="bkmk_delete_KPI"></a> Per eliminare un indicatore KPI e mantenere la misura base  
  
-   Nella griglia delle misure fare clic con il pulsante destro del mouse sulla misura che viene usata come misura di base (valore) dell'indicatore KPI, quindi scegliere **Elimina KPI**.  
  
## <a name="alt-shortcuts"></a>Tasti di scelta rapida  
  
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
 [Indicatori KPI &#40;SSAS tabulare&#41;](kpis-ssas-tabular.md)   
 [Misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md)   
 [Creare e gestire misure &#40;SSAS tabulare&#41;](create-and-manage-measures-ssas-tabular.md)  
  
  
