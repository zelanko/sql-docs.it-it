---
title: Opzioni query-risultati (pagina della griglia) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.grid.f1
ms.assetid: 764bf435-3aab-4c62-b4e0-64fe020a5a95
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c50957f59ef4e4743ca1667d6eb7a97869bec18
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089011"
---
# <a name="query-options-results-grid-page"></a>Risultati di Opzioni query (pagina Griglia)
  Utilizzare questa pagina per specificare le opzioni di visualizzazione di un set di risultati di query in formato griglia.  
  
## <a name="options"></a>Opzioni  
 **Includi la query nel set di risultati**  
 Restituisce il testo della query come parte del set di risultati.  
  
 **Includi intestazioni di colonna nelle operazioni di copia o salvataggio dei risultati**  
 Consente di includere le intestazioni di colonna (titoli) durante la copia dei risultati negli Appunti o il salvataggio in un file. Deselezionare questa casella di controllo se si desidera che i risultati salvati o copiati contengano solo i dati senza le intestazioni di colonna.  
  
 **Elimina risultati dopo l'esecuzione**  
 Consente di liberare memoria eliminando i risultati delle query dopo la loro visualizzazione.  
  
 **Visualizza risultati in una scheda separata**  
 Consente di visualizzare il set dei risultati in una nuova finestra del documento anziché nella parte inferiore della finestra del documento della query.  
  
 **Passa alla scheda dei risultati al termine della query**  
 Consente di impostare automaticamente lo stato attivo dello schermo sul set dei risultati.  
  
 **Dimensioni massime caratteri recuperati**  
 **Dati non XML**:  
  
 Consente di immettere un valore compreso tra 1 e 65535 per specificare il numero massimo di caratteri che sarà possibile visualizzare in ogni cella.  
  
> [!NOTE]  
>  Se si specifica un numero elevato di caratteri, i dati nel set di risultati potrebbero non essere visualizzati completamente. Il numero massimo di caratteri visualizzati in ogni cella dipende dalle dimensioni del carattere. Se si specifica un valore elevato in questa casella e vengono restituiti set di risultati di notevoli dimensioni, la memoria per [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] potrebbe risultare insufficiente con effetti negativi sulle prestazioni del sistema.  
  
 **Dati XML**:  
  
 Consente di selezionare i valori **1 MB**, **2 MB**o **5 MB**. Selezionare **Illimitate** per recuperare tutti i caratteri.  
  
 **Ripristina predefiniti**  
 Reimposta le impostazioni predefinite originali per tutti i valori nella pagina.  
  
  
