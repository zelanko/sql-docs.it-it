---
title: Proprietà della tabella (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.tableprop.f1
ms.assetid: 16d3347b-7e43-4a6b-9956-fdd6ede092e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97d6731c5e85c3b37facc7172ecacbd2c7c74176
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66066466"
---
# <a name="table-properties-ssas-tabular"></a>Table Properties (SSAS Tabular)
  In questo argomento vengono descritte le proprietà delle tabelle dei modelli tabulari. Le proprietà descritte differiscono da quelle presenti nella finestra di dialogo Modifica proprietà tabella, che consentono di definire quali colonne vengono importate dall'origine.  
  
 Sezioni dell'argomento:  
  
-   [Table Properties](#bkmk_properties)  
  
-   [Per configurare le impostazioni delle proprietà delle tabelle](#bkmk_config_prop)  
  
##  <a name="bkmk_properties"></a>Proprietà tabella  
 **Base**  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Nome connessione**|\<nome della connessione>|Nome della connessione all'origine dati della tabella.<br /><br /> Per modificare la connessione, fare clic sul pulsante.|  
|**Nascosto**|False|Viene specificato se la tabella è nascosta dalla visualizzazione negli elenchi dei campi del client di creazione report.|  
|**Partizioni**||Le partizioni per la tabella non possono essere visualizzate nella finestra **Proprietà** . Per visualizzare, creare o modificare partizioni, fare clic sul pulsante per aprire Gestione partizioni.|  
|**Dati di origine**||I dati di origine per la tabella non possono essere visualizzati nella finestra **Proprietà** . Per visualizzare o modificare i dati di origine, fare clic sul pulsante per aprire la finestra di dialogo Modifica proprietà tabella.|  
|**Descrizione tabella**||Descrizione di testo per la tabella.<br /><br /> In [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)], se un utente finale posiziona il cursore su questa tabella nell'elenco dei campi, la descrizione viene visualizzata come descrizione comando.|  
|**Nome tabella**|\<nome descrittivo>|Specifica il nome descrittivo della tabella. È possibile specificare il nome di tabella quando una tabella viene importata utilizzando l'Importazione guidata tabella oppure in qualsiasi momento dopo l'importazione. Il nome della tabella nel modello può essere diverso dalla tabella associata nell'origine. Il nome descrittivo della tabella viene visualizzato nell'elenco di campi dell'applicazione client di creazione report, nonché nel database modello in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
  
 **Proprietà report**  
  
 Per descrizioni dettagliate e informazioni sulla configurazione per le proprietà di creazione dei report, vedere [Proprietà report Power View &#40;SSAS tabulare&#41;](properties-ssas-tabular.md).  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Set di campi predefiniti**|||  
|Comportamento tabella|||  
  
###  <a name="bkmk_config_prop"></a>Per configurare le impostazioni delle proprietà delle tabelle  
  
1.  In Progettazione modelli, in Vista dati fare clic su una tabella (scheda) oppure in Vista diagramma fare clic su un'intestazione di tabella.  
  
2.  Nella finestra **Proprietà** fare clic su una proprietà, quindi digitare un valore oppure fare clic sul pulsante per ulteriori opzioni di configurazione.  
  
  
