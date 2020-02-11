---
title: Selezione calendari (creazione guidata dimensione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.serverSpecialCalendars.f1
ms.assetid: 6e28a020-2586-4b13-9333-b499fb1b33af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fde8172abbebe08fc4aae4cc0282955c2a582d02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069684"
---
# <a name="select-calendars-dimension-wizard"></a>Selezione calendari (Creazione guidata dimensione)
  Usare la pagina **Selezione calendari** per creare gerarchie aggiuntive che rappresentano calendari fiscali, di report, di produzione o ISO 8601 per la dimensione temporale.  
  
> [!NOTE]  
>  Questa pagina viene visualizzata solo se è stata selezionata l'opzione **Dimensione temporale del server** nella pagina **Selezione tipo di dimensione** oppure se sono state selezionate le opzioni **Compila dimensione senza usare un'origine dei dati** nella pagina **Selezione metodo di creazione** e **Dimensione temporale** nella pagina **Selezione tipo di dimensione** .  
  
## <a name="options"></a>Opzioni  
 **Calendario fiscale**  
 Selezionare questa opzione per creare una gerarchia temporale basata su un calendario fiscale.  
  
 **Giorno e mese di inizio**  
 Consente di selezionare il giorno e il mese di inizio del calendario fiscale.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo quando si seleziona **Calendario fiscale** .  
  
 **Convenzione di denominazione calendario fiscale**  
 Consente di selezionare la convenzione di denominazione utilizzata dal calendario fiscale. Selezionare **Nome anno calendario** oppure **Nome anno calendario +1**.  
  
> [!NOTE]  
>  Questa opzione è disponibile solo quando si seleziona **Calendario fiscale** .  
  
 **Calendario report (o marketing)**  
 Selezionare questa opzione per creare una gerarchia temporale basata su un calendario di report.  
  
 **Settimana e mese di inizio**  
 Consente di selezionare la settimana e il mese di inizio del calendario di report.  
  
> [!NOTE]  
>  Questa opzione è disponibile se è stata selezionata l'opzione **Calendario report (o marketing)** .  
  
 **Schema di settimane per mese**  
 Consente di selezionare lo schema di settimane per mese utilizzato dal calendario di report.  
  
> [!NOTE]  
>  Questa opzione è disponibile se è stata selezionata l'opzione **Calendario report (o marketing)** .  
  
 nella tabella riportata di seguito vengono elencate le opzioni disponibili per lo schema di settimane per mese.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Settimana 445**|Il primo mese del trimestre è composto da 4 settimane, il secondo mese da 4 settimane e il terzo mese da 5 settimane.|  
|**Settimana 454**|Il primo mese del trimestre è composto da 4 settimane, il secondo mese da 5 settimane e il terzo mese da 4 settimane.|  
|**544**|Il primo mese del trimestre è composto da 5 settimane, il secondo mese da 4 settimane e il terzo mese 4 settimane.|  
  
 **Calendario produzione**  
 Selezionare questa opzione per creare una gerarchia temporale basata su un calendario di produzione.  
  
 **Settimana e mese di inizio**  
 Consente di selezionare la settimana e il mese di inizio del calendario di produzione.  
  
> [!NOTE]  
>  Questa opzione è disponibile se è stata selezionata l'opzione **Calendario produzione** .  
  
 **Trimestre con periodi aggiuntivi**  
 Consente di selezionare o digitare il trimestre che conterrà i periodi aggiuntivi.  
  
> [!NOTE]  
>  Questa opzione è disponibile se è stata selezionata l'opzione **Calendario produzione** .  
  
 **Calendario ISO 8601**  
 Selezionare questa opzione per creare una gerarchia basata sul calendario ISO 8601.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della creazione guidata dimensione](dimension-wizard-f1-help.md)   
 [Dimensioni &#40;Analysis Services Dati multidimensionali&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensioni nei modelli multidimensionali](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
