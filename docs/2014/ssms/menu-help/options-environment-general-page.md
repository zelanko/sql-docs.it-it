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
ms.openlocfilehash: f82a6ff79bfc9fbd1fb2d97036fa83c0b3f5d22b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067431"
---
# <a name="options-environment-general-page"></a>Opzioni (pagina Ambiente/Generale)
  Usare la finestra di dialogo **Opzioni** per configurare le azioni di avvio di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], le opzioni generali di gestione della finestra e altre impostazioni generali. Scegliere **Opzioni** dal menu **Strumenti**, espandere la cartella **Ambiente** e quindi fare clic su **Generale**.  
  
## <a name="ui-element-list"></a>Elenco elementi dell'interfaccia utente  
 **All'avvio**  
 Consente di selezionare l'azione che deve essere eseguita da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] all'avvio. Le opzioni disponibili sono:  
  
-   **Apri Esplora oggetti** richiede di stabilire una connessione e quindi apre Esplora oggetti.  
  
-   **Apri nuova finestra Query** richiede di stabilire una connessione e quindi apre Editor di query SQL.  
  
-   **Apri Esplora oggetti e nuova finestra Query** richiede di stabilire una connessione e quindi la usa per aprire sia Esplora oggetti sia Editor di query SQL.  
  
-   **Apri ambiente vuoto** apre [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] senza visualizzare una finestra dell'editor di query SQL né connettere Esplora oggetti a un server.  
  
 **Nascondi oggetti di sistema in Esplora oggetti**  
 Selezionare questa casella di controllo per rimuovere database, tabelle, viste e stored procedure di sistema dalla visualizzazione dell'albero in Esplora oggetti. Le funzioni e i tipi di dati di sistema non vengono nascosti. Questa opzione si applica solo alle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non ha alcun effetto sui server già connessi in Esplora oggetti.  
  
## <a name="environment-layout"></a>Layout ambiente  
 Per passare dalla modalità di ambiente a documenti a schede a quella a interfaccia per documenti multipli (MDI, Multiple-Document Interface) è necessario chiudere e riaprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **Documenti a schede**  
 Selezionare questa opzione per visualizzare le finestre di documento a schede raggruppate all'interno degli editor. Le finestre di documento a schede sono utili per organizzare i documenti aperti e passare da un documento all'altro.  
  
 **Ambiente MDI**  
 Selezionare questa opzione per aprire i documenti in un ambiente MDI. Le finestre di documento MDI sono utili per risparmiare lo spazio sullo schermo che in un ambiente a documenti a schede è occupato dalle schede. Quando è abilitata la modalità MDI, è possibile spostarsi tra i documenti premendo CTRL+TAB oppure usando le opzioni di affiancamento nel menu **Finestra** .  
  
## <a name="docked-tool-window-behavior"></a>Comportamento finestra degli strumenti ancorata  
 **Pulsante Chiudi valido solo per la scheda attiva**  
 Quando questa casella di controllo è selezionata, viene chiusa solo la finestra degli strumenti attiva e non tutte le finestre degli strumenti presenti nel set ancorato. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **Pulsante Nascondi automaticamente valido solo per la scheda attiva**  
 Quando questa casella di controllo è selezionata, viene nascosta automaticamente solo la finestra degli strumenti attiva e non tutte le finestre degli strumenti presenti nel set ancorato. Per impostazione predefinita, questa casella di controllo è deselezionata.  
  
## <a name="display"></a>Schermo  
 **Visualizza n file nell'elenco degli ultimi file usati**  
 Consente di scegliere il numero di progetti e file recenti da visualizzare nel menu **File** . Digitare un numero compreso tra 1 e 24. Il valore predefinito è 4. Questa opzione consente di recuperare con facilità i file e i progetti script utilizzati più di recente.  
  
  
