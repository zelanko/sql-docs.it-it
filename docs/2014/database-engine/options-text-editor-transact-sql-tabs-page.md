---
title: Opzioni (editor di testo-Transact-SQL-pagina tabulazioni) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 761c84612c207397e33ae96dfcfb088b05bc24b8
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000666"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a>Opzioni (editor di testo-Transact-SQL-pagina tabulazioni)
  Utilizzare questa finestra di dialogo per cambiare il comportamento di tabulazione dell'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] utilizzato per programmare gli script [!INCLUDE[tsql](../includes/tsql-md.md)]. Per visualizzare queste impostazioni, scegliere **Opzioni** dal menu **Strumenti**, espandere la cartella **Editor di testo**, espandere la sottocartella **Transact-SQL** e quindi fare clic su **Schede**.  
  
## <a name="setting-options-in-multiple-locations"></a>Opzioni di impostazione in più posizioni  
 Le opzioni per l'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] possono essere impostate anche nella finestra di dialogo **Tutti i linguaggi - Schede**. Se si utilizza la finestra di dialogo **Tutti i linguaggi** per impostare opzioni diverse per gli altri editor di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , ad esempio DMX o MDX, è necessario reimpostare le opzioni dell'editor di query del [!INCLUDE[ssDE](../includes/ssde-md.md)] tramite questa finestra di dialogo.  
  
## <a name="indenting"></a>Stili rientri  
 **Nessuno**  
 Quando questa opzione è selezionata, la nuova riga creata in seguito alla pressione di INVIO non viene rientrata. Il cursore viene posizionato in corrispondenza della prima colonna della nuova riga.  
  
 **Bloccato**  
 Quando è selezionata questa opzione la nuova riga creata premendo INVIO viene rientrata automaticamente della stessa distanza della riga precedente.  
  
 **Intelligenti**  
 Questa opzione non è disponibile.  
  
## <a name="tabs"></a>Schede  
 **Dimensione tabulazione**  
 Consente di impostare la distanza in spazi tra le tabulazioni. Il valore predefinito è quattro spazi.  
  
 **Dimensione rientro**  
 Consente di impostare la dimensione in spazi di un rientro automatico. Il valore predefinito è quattro spazi. Per riempire il rientro specificato verranno inseriti caratteri di tabulazione, caratteri di spazio o entrambi.  
  
 **Inserisci spazi**  
 Quando questa opzione è selezionata, durante le operazioni di rientro vengono inseriti solo caratteri spazio, non caratteri di tabulazione. Se la **dimensione del rientro** è impostata su 5, ad esempio, verranno inseriti cinque caratteri di spazio ogni volta che si preme il tasto TAB o si fa clic sul pulsante **Aumenta rientro** sulla barra degli strumenti della [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] finestra principale.  
  
 **Mantieni tabulazioni**  
 Quando questa opzione è selezionata, durante le operazioni di rientro viene inserito il numero massimo di caratteri di tabulazione possibile. Ogni carattere di tabulazione riempie il numero di spazi specificato in **Dimensione tabulazione**. Se il valore specificato per l'opzione **Dimensione rientro** non è un multiplo pari del valore specificato per l'opzione **Dimensione tabulazione**, per riempire la differenza vengono aggiunti caratteri spazio.  
  
  
