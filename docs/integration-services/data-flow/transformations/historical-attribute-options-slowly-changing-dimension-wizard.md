---
title: Opzioni attributi cronologici (Configurazione guidata dimensioni a modifica lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03d045cddeb2da31a3a9c3e4e3cef9f17d10d0f8
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726057"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>Opzioni attributi cronologici (Configurazione guidata dimensioni a modifica lenta)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la finestra di dialogo **Opzioni attributi cronologici** per visualizzare gli attributi cronologici in base a date di inizio e fine o per registrare gli attributi cronologici in una colonna creata appositamente a questo scopo.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Usa una singola colonna per mostrare i record correnti e scaduti**  
 Se si sceglie di utilizzare una sola colonna per registrare lo stato degli attributi cronologici, saranno disponibili le opzioni seguenti:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Colonna per l'indicazione del record corrente**|Consente di selezionare una colonna da utilizzare per l'indicazione del record corrente.|  
|**Valore se corrente**|Utilizzare **Vero** o **Corrente** per indicare se si tratta del record corrente.|  
|**Valore se scaduto**|Utilizzare **Falso** o **Scaduto** per indicare se il record è un valore cronologico.|  
  
 **Usa colonne Data inizio e Data fine per identificare i record correnti e scaduti**  
 La tabella della dimensione per questa opzione deve includere una colonna data. Se si sceglie di visualizzare gli attributi cronologici in base alle date di inizio e fine, saranno disponibili le opzioni seguenti:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Colonna Data inizio**|Consente di selezionare la colonna della tabella della dimensione che conterrà la data di inizio.|  
|**Colonna Data fine**|Consente di selezionare la colonna della tabella della dimensione che conterrà la data di fine.|  
|**Variabile per l'impostazione dei valori di data**|Consente di selezionare una variabile per la data nell'elenco.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione degli output tramite Configurazione guidata dimensioni a modifica lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
