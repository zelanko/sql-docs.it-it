---
title: Opzioni (ambiente-pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Environment.SQLEnvironmentOptions
ms.assetid: c32ccdb8-2cf8-4c78-b474-a3abd3dbbd13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a96b77c3f1243bc3d95cf38242463724348134b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68188507"
---
# <a name="options-environment-general-page"></a>Opzioni (pagina Ambiente/Generale)
  Utilizzare la finestra di dialogo **Opzioni** per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] configurare le azioni di avvio, le opzioni generali di gestione della finestra e altre impostazioni generali. Scegliere **Opzioni** dal menu **Strumenti**, espandere la cartella **Ambiente** e quindi fare clic su **Generale**.  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **All'avvio**  
 Consente di selezionare l'azione che deve essere eseguita da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] all'avvio. Le opzioni disponibili sono le seguenti:  
  
-   **Aprire Esplora oggetti** richiede una connessione e quindi apre Esplora oggetti.  
  
-   **Apri nuova finestra query** richiede una connessione e quindi apre l'editor di query SQL.  
  
-   **Aprire Esplora oggetti e la nuova query** richiede una connessione, quindi apre sia Esplora oggetti che l'editor di query SQL con tale connessione.  
  
-   **Apri ambiente vuoto** viene [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aperto senza una finestra dell'editor di query SQL e senza connessione Esplora oggetti a un server.  
  
 **Nascondi oggetti di sistema in Esplora oggetti**  
 Selezionare questa casella di controllo per rimuovere database, tabelle, viste e stored procedure di sistema dalla visualizzazione dell'albero in Esplora oggetti. Le funzioni e i tipi di dati di sistema non vengono nascosti. Questa opzione si applica solo alle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non ha alcun effetto sui server già connessi in Esplora oggetti.  
  
## <a name="environment-layout"></a>Layout ambiente  
 Per passare dalla modalità di ambiente a documenti a schede a quella a interfaccia per documenti multipli (MDI, Multiple-Document Interface) è necessario chiudere e riaprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **Documenti a schede**  
 Selezionare questa opzione per visualizzare le finestre di documento a schede raggruppate all'interno degli editor. Le finestre di documento a schede sono utili per organizzare i documenti aperti e passare da un documento all'altro.  
  
 **Ambiente MDI**  
 Selezionare questa opzione per aprire i documenti in un ambiente MDI. Le finestre di documento MDI sono utili per risparmiare lo spazio sullo schermo che in un ambiente a documenti a schede è occupato dalle schede. Quando è abilitata la modalità MDI, è possibile spostarsi tra i documenti premendo CTRL+TAB oppure usando le opzioni di affiancamento nel menu **Finestra** .  
  
## <a name="docked-tool-window-behavior"></a>Comportamento finestra degli strumenti ancorata  
 **Il pulsante Chiudi ha effetto solo sulla scheda attiva**  
 Quando questa casella di controllo è selezionata, viene chiusa solo la finestra degli strumenti attiva e non tutte le finestre degli strumenti presenti nel set ancorato. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **Il pulsante Nascondi automaticamente ha effetto solo sulla scheda attiva**  
 Quando questa casella di controllo è selezionata, viene nascosta automaticamente solo la finestra degli strumenti attiva e non tutte le finestre degli strumenti presenti nel set ancorato. Per impostazione predefinita, tale casella di controllo è deselezionata.  
  
## <a name="display"></a>Visualizzazione  
 **Visualizza n file nell'elenco degli ultimi file usati**  
 Consente di scegliere il numero di progetti e file recenti da visualizzare nel menu **File** . Digitare un numero compreso tra 1 e 24. Il valore predefinito è 4. Questa opzione consente di recuperare con facilità i file e i progetti script utilizzati più di recente.  
  
  
