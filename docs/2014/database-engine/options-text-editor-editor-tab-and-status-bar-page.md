---
title: 'Opzioni (editor di testo: pagina scheda Editor e barra di stato) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqleditors.editorcontextsettings
- VS.ToolsOptionsPages.Text_Editor.EditorTabAndStatusBar
ms.assetid: e4815678-7885-4631-878f-c6a2b857ee05
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 01098f2181085f17788429608afb7bdda15fb504
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089235"
---
# <a name="options-text-editor-editor-tab-and-status-bar-page"></a>Opzioni (pagina Editor di testo: Scheda editor e barra di stato)
  Nella **pagina Scheda editor e barra di stato** è possibile personalizzare le informazioni visualizzate dagli editor di query di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . È possibile specificare il livello di informazioni da visualizzare nella scheda e sulla barra di stato della finestra dell'editor di query, nonché specificare se la barra di stato viene visualizzata nella parte superiore o inferiore della finestra dell'editor.  
  
## <a name="option-settings-by-editor"></a>Impostazioni delle opzioni in base all'editor  
 La scheda dell'editor e la barra di stato sono disponibili in tutti gli editor di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , ma offrono livelli di funzionalità diversi.  
  
 L'editor di query del Motore di database è in grado di eseguire la connessione a un gruppo di server e in tal caso vengono aperte connessioni a tutte le istanze nel gruppo di server e la stessa query può venire eseguita contemporaneamente in ogni connessione. È possibile usare questa finestra di dialogo per specificare che la barra di stato ha un colore diverso quando viene stabilita una connessione a più istanze anziché a un'unica istanza. Per modificare le opzioni relative ai risultati multiserver, usare la pagina [Opzioni (Risultati query/SQL Server/Multiserver)](../../2014/database-engine/options-query-results-sql-server-multi-server.md) .  
  
## <a name="status-bar-content"></a>Contenuto della barra di stato  
 Consente di specificare le informazioni visualizzate nella barra di stato dell'editor di query.  
  
 **Visualizza tempo di esecuzione**  
 Consente di indicare il tempo di esecuzione degli script. Sono disponibili le impostazioni seguenti:  
  
 **Nessuno**  
 Sulla barra di stato non viene visualizzata alcuna informazione relativa alla durata dell'esecuzione.  
  
 **Fine**  
 Sulla barra di stato viene visualizzata l'ora corrente del giorno in cui è in corso l'esecuzione dello script. Quando lo script viene completato, viene visualizzata l'ora corrente del giorno del completamento dello script.  
  
 **Trascorso**  
 Sulla barra di stato viene visualizzata la quantità di tempo trascorso da quando lo script è stato eseguito. Quando lo script viene completato, viene visualizzata la quantità di tempo utilizzata per l'esecuzione dello script.  
  
 **Includi nome database**  
 Consente di includere il nome del database corrente per la connessione. Quando l'editor di query viene aperto per la prima volta, viene visualizzato il database predefinito per l'account di accesso. Il contesto del database può essere modificato successivamente mediante l'istruzione Transact-SQL USE.  
  
 **Includi nome account di accesso**  
 Consente di includere il nome dell'account di accesso.  
  
 **Includi conteggio righe**  
 Consente di includere un conteggio delle righe elaborate dallo script eseguito.  
  
 **Includi nome server**  
 Consente di includere il nome del server. Per le connessioni locali, si tratta del nome dell'istanza. Per le connessioni remote, si tratta del nome del computer remoto e del nome dell'istanza.  
  
## <a name="status-bar-layout-and-colors"></a>Layout e colori barra di stato  
 Consente di specificare i colori per gli elementi visualizzati sulla barra di stato dell'editor di query.  
  
 **Connessioni di gruppo**  
 Consente di impostare il colore della barra di stato quando l'editor di query dispone di più di una connessione.  
  
 **Connessioni a un unico server**  
 Consente di impostare il colore della barra di stato quando l'editor di query dispone di un'unica connessione.  
  
 **Posizione della barra di stato**  
 Consente di specificare la posizione della barra di stato. Sono disponibili le impostazioni seguenti:  
  
 **In alto**  
 La barra di stato viene visualizzata nella parte superiore della finestra dell'editor di query.  
  
 **Parte inferiore**  
 La barra di stato viene visualizzata nella parte inferiore della finestra dell'editor di query.  
  
## <a name="tab-text"></a>Testo scheda  
 Consente di specificare il testo visualizzato nella scheda nella parte superiore di una finestra dell'editor di query. Se il testo è troppo lungo da visualizzare, è possibile visualizzare la stringa completa in una descrizione comando, spostando il puntatore del mouse sulla scheda.  
  
 **Includi nome database**  
 Consente di includere il nome del database corrente per la connessione. Quando l'editor di query viene aperto per la prima volta, viene visualizzato il database predefinito per l'account di accesso. Il contesto del database può essere modificato successivamente mediante l'istruzione Transact-SQL USE.  
  
 **Includi nome file**  
 Consente di includere il nome del file in cui è archiviato lo script.  
  
 **Includi nome cartella**  
 Consente di includere il percorso della cartella in cui è archiviato il file di script.  
  
 **Includi nome account di accesso**  
 Consente di includere il nome dell'account di accesso.  
  
 **Includi nome server**  
 Consente di includere il nome del server. Per le connessioni locali, si tratta del nome dell'istanza. Per le connessioni remote, si tratta del nome del computer remoto e del nome dell'istanza.  
  
## <a name="see-also"></a>Vedi anche  
 [Opzioni &#40;ambiente: pagina tipi di carattere e colori&#41;](../ssms/menu-help/options-environment-fonts-and-colors-page.md)   
 [Codifica con colori negli editor di query](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
