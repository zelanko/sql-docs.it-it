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
ms.openlocfilehash: aee638291a4aee2c4ea5d60a69fc206af613e15d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965551"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Selezione tabelle e viste di origine (Importazione/Esportazione guidata SQL Server)
  Utilizzare la pagina **Selezione tabelle e viste di origine** per specificare le tabelle e le viste da copiare dall'origine dati alla destinazione.  
  
> [!NOTE]  
>  Non è necessario copiare tutte le colonne in una tabella quando si seleziona l'opzione Copia tabella. Dopo aver selezionato una tabella di destinazione, fare clic su Modifica mapping per visualizzare la finestra di dialogo **Mapping colonne** . Selezionare **\<ignore>** nella colonna **destinazione** della finestra di dialogo **Mapping colonne** per le colonne che si desidera ignorare.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [SQL Server importazione/esportazione guidata](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Per informazioni sulle opzioni per avviare la procedura guidata e sulle autorizzazioni necessarie per eseguire la procedura guidata, vedere [eseguire l'importazione/esportazione guidata SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 Lo scopo di Importazione/Esportazione guidata SQL Server è la copia di dati da un'origine a una destinazione. La procedura guidata può inoltre creare automaticamente un database di destinazione e le tabelle di destinazione. Se tuttavia è necessario copiare più database o tabelle, o altri tipi di oggetti di database, è preferibile utilizzare Copia guidata database. Per altre informazioni, vedere [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opzioni  
  
### <a name="tables-and-views-list"></a>Elenco Tabelle e viste  
 **origine**  
 Mediante le caselle di controllo, selezionare dall'elenco di tabelle e viste disponibili quelle da copiare nella destinazione. Se si seleziona una tabella o una vista di origine e non si eseguono altre azioni, lo schema e i dati dell'origine verranno copiati senza essere modificati.  
  
 **Destinazione**  
 Consente di selezionare una tabella di destinazione dall'elenco per ogni tabella di origine.  
  
> [!NOTE]  
>  Se la procedura guidata viene sospesa a questo punto per creare una tabella di destinazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o un altro strumento, la nuova tabella non verrà immediatamente visualizzata nell'elenco delle tabelle di destinazione disponibili. Per aggiornare l'elenco delle tabelle di destinazione, tornare indietro di due pagine alla pagina **scelta destinazione** , selezionare di nuovo il database di destinazione, quindi eseguire di nuovo l'istruzione di **Selezione tabelle e viste di origine**.  
  
### <a name="other-options"></a>Altre opzioni  
 **Modifica mapping**  
 Utilizzare la finestra di dialogo **Mapping colonne** per specificare le colonne di destinazione per la ricezione dei dati di origine. È possibile copiare solo un subset di colonne selezionando \<ignore> la colonna **destinazione** della finestra di dialogo **Mapping colonne** per le colonne che si desidera ignorare.  
  
 **Anteprima**  
 Visualizzare l'anteprima dei dati di origine nella finestra di dialogo **Anteprima dati** per verificarlo prima di eseguire l'importazione o l'esportazione. La finestra di dialogo **Anteprima dati** Visualizza fino a 200 righe di dati.  
  
 Dopo avere visualizzato un'anteprima dei dati, potrebbe essere necessario modificare le opzioni selezionate per l'origine e la destinazione dei dati. Per apportare queste modifiche, nella pagina **Seleziona tabelle e viste di origine** fare clic su **Indietro** per tornare alle pagine precedenti e modificare le opzioni selezionate.  
  
  
