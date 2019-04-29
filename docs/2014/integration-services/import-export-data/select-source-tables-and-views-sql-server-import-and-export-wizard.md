---
title: Selezione tabelle e viste di origine (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 479cc0e650c598e0a253caca796b854dc4eb69cd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62892669"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Selezione tabelle e viste di origine (Importazione/Esportazione guidata SQL Server)
  Usare la **selezionare le tabelle di origine e le viste** pagina per specificare le tabelle e viste da copiare dall'origine dati nella destinazione.  
  
> [!NOTE]  
>  Non è necessario copiare tutte le colonne in una tabella quando si seleziona l'opzione Copia tabella. Dopo aver selezionato una tabella di destinazione, fare clic su Modifica mapping per visualizzare il **mapping delle colonne** nella finestra di dialogo. Selezionare  **\<ignorare >** nel **destinazione** colonna della **mapping colonne** finestra di dialogo per le colonne che si desidera ignorare.  
  
 Per altre informazioni su questa procedura guidata, vedere [SQL Server importazione / esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per altre informazioni sulle opzioni per l'avvio della procedura guidata e sulle autorizzazioni necessarie per eseguire correttamente la procedura guidata, vedere [esecuzione di SQL Server importazione / esportazione guidata](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
  
### <a name="tables-and-views-list"></a>Elenco Tabelle e viste  
 **Origine**  
 Mediante le caselle di controllo, selezionare dall'elenco di tabelle e viste disponibili quelle da copiare nella destinazione. Se si seleziona una tabella o una vista di origine e non si eseguono altre azioni, lo schema e i dati dell'origine verranno copiati senza essere modificati.  
  
 **Destinazione**  
 Consente di selezionare una tabella di destinazione dall'elenco per ogni tabella di origine.  
  
> [!NOTE]  
>  Se la procedura guidata viene sospesa a questo punto per creare una tabella di destinazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o un altro strumento, la nuova tabella non verrà immediatamente visualizzata nell'elenco delle tabelle di destinazione disponibili. Per aggiornare l'elenco delle tabelle di destinazione, un passo indietro di due pagine per il **scegliere una destinazione** pagina, selezionare di nuovo il database di destinazione e quindi avanzare fino alle **selezionare le tabelle di origine e le viste**.  
  
### <a name="other-options"></a>Altre opzioni  
 **Modifica mapping**  
 Usare la **mapping delle colonne** finestra di dialogo per specificare le colonne di destinazione per ricevere i dati di origine. È possibile copiare solo un subset di colonne selezionando \<Ignora > nella **destinazione** colonna del **i mapping delle colonne** finestra di dialogo per le colonne che si desidera ignorare.  
  
 **Anteprima**  
 Anteprima origine dati nella **Anteprima dati** finestra di dialogo per verificarli prima di eseguire l'importazione o esportazione. Il **Anteprima dati** nella finestra di dialogo consente di visualizzare fino a 200 righe dei dati.  
  
 Dopo avere visualizzato un'anteprima dei dati, potrebbe essere necessario modificare le opzioni selezionate per l'origine e la destinazione dei dati. Per apportare queste modifiche, nella pagina **Seleziona tabelle e viste di origine** fare clic su **Indietro** per tornare alle pagine precedenti e modificare le opzioni selezionate.  
  
  
