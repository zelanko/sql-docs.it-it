---
title: Opzioni (editor di testo-Transact-SQL-pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.General
dev_langs:
- TSQL
ms.assetid: 7021ecb7-8fb5-4d8c-b984-3d34fcde8be2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f32377fffb26ac622dc4045d108e491adc2b0342
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089166"
---
# <a name="options-text-editor---transact-sql--general-page"></a>Opzioni (editor di testo-Transact-SQL-pagina generale)
  Utilizzare la finestra di dialogo delle opzioni **Generale** per cambiare il comportamento di modifica generale dell'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] utilizzato per modificare gli script [!INCLUDE[tsql](../includes/tsql-md.md)] . Per visualizzare le impostazioni scegliere **Opzioni** dal menu **Strumenti**, espandere la sottocartella **Transact-SQL** e quindi fare clic su **Generale**.  
  
## <a name="setting-options-in-multiple-locations"></a>Opzioni di impostazione in più posizioni  
 Le opzioni per l'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] possono essere impostate anche nella finestra di dialogo **Tutti i linguaggi - Generale** . Se si utilizza la finestra di dialogo **Tutti i linguaggi** per impostare opzioni diverse per gli altri editor di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , ad esempio DMX o MDX, è necessario reimpostare le opzioni dell'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] tramite questa finestra di dialogo.  
  
## <a name="statement-completion"></a>Completamento istruzioni  
 **Elenco automatico membri**  
 Quando questa casella di controllo è selezionata, nell'editor vengono visualizzati gli elenchi di database e oggetti di schema, le colonne, le funzioni con valori di tabella o le funzioni disponibili durante la digitazione. Scegliere l'elemento desiderato nell'elenco popup per inserirlo nel codice.  
  
 **Nascondi membri avanzati**  
 Questa casella di controllo non è disponibile.  
  
 **Informazioni sui parametri**  
 Quando questa casella di controllo è selezionata, vengono visualizzate le informazioni sui parametri per una stored procedure o una funzione che si trova immediatamente a sinistra del punto di inserimento (cursore). Le informazioni includono un elenco dei parametri disponibili con i relativi nomi e i tipi di dati.  
  
## <a name="settings"></a>Impostazioni  
 **Abilita spazio virtuale**  
 Se questa casella di controllo è selezionata, è possibile fare clic in un punto qualsiasi oltre la fine di una riga di codice ed effettuare la digitazione. Selezionare la casella di controllo per inserire i commenti sempre nel medesimo punto accanto al codice. Se si seleziona questa casella di controllo, la casella di controllo **A capo automatico** viene disabilitata.  
  
 **A capo automatico**  
 Se questa casella di controllo è selezionata, le parti di una riga che si estendono orizzontalmente oltre l'area visibile dell'editor vengono visualizzate automaticamente nella riga successiva. Selezionando questa casella di controllo, la casella di controllo **Mostra icone per ritorno a capo automatico** viene abilitata e la casella di controllo **Attiva spazio virtuale** viene disabilitata.  
  
 **Mostra icone per ritorno a capo automatico**  
 Se questa casella di controllo è selezionata, viene visualizzato un simbolo di ritorno a capo nel punto in cui una riga lunga va a capo sulla riga successiva.  
  
 **Applica comandi Taglia o Copia a righe vuote in assenza di selezione**  
 Questa casella di controllo consente di impostare il comportamento dell'editor nei casi in cui si posiziona il punto di inserimento in una riga vuota senza selezionare alcun elemento e quindi si fa clic su **Copia** o **Taglia**.  
  
 Se la casella di controllo è selezionata, la riga vuota viene copiata o incollata. Se quindi si fa clic su **Incolla**, viene inserita una nuova riga vuota.  
  
 Se la casella di testo è deselezionata, non viene copiato o tagliato alcun elemento. Se quindi si fa clic su **Incolla**, viene incollato il contenuto copiato più di recente. Se non è stata eseguita alcuna operazione di copia, non viene incollato alcun elemento.  
  
 Questa impostazione non ha alcun effetto sui comandi **Copia** o **Taglia** applicati a righe non vuote. Se non è selezionato alcun elemento, viene copiata o tagliata la riga intera. Se quindi si fa clic su **Incolla**, vengono incollati la riga intera e il relativo carattere di ritorno a capo.  
  
## <a name="display"></a>Visualizzazione  
 **Numeri di riga**  
 Se questa casella di controllo è selezionata, accanto a ogni riga del codice viene visualizzato un numero.  
  
> [!NOTE]  
>  I numeri di riga non vengono aggiunti al codice, né stampati. Si tratta esclusivamente di elementi di riferimento.  
  
 **Consenti navigazione URL con clic singolo**  
 Se questa casella di controllo è selezionata, il cursore si trasforma in un puntatore a forma di mano quando viene posizionato su un URL nell'editor. È possibile fare clic sull'URL per visualizzare nel browser la pagina indicata.  
  
 **Barra di navigazione**  
 Questa casella di controllo non è disponibile.  
  
  
