---
title: Finestra di dialogo Sfoglia tutte le entità | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 46d6fd5d4ecd821a3ccfeb35679e8fa7bab6104e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771721"
---
# <a name="browse-all-principals-dialog-box"></a>Finestra di dialogo Sfoglia tutte le entità
  Usare la finestra di dialogo **Sfoglia tutte le entità** per selezionare un'entità di database per modificare le autorizzazioni dell'entità per il progetto selezionato o per tutti i progetti contenuti in una cartella selezionata.  
  
 **Per saperne di più**  
  
-   [Aprire la finestra di dialogo Sfoglia tutte le entità](#open_dialog)  
  
-   [Configurare le opzioni](#options)  
  
##  <a name="open_dialog"></a> Aprire la finestra di dialogo Sfoglia tutte le entità  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il catalogo SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Per modificare le autorizzazioni dell'entità per tutti i progetti contenuti in una cartella selezionata, fare clic con il pulsante destro del mouse sulla cartella, quindi scegliere **Proprietà**.  
  
     Per modificare le autorizzazioni dell'entità per un progetto selezionato, espandere la cartella che contiene il progetto, fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Proprietà**.  
  
5.  Selezionare la pagina **Autorizzazioni** , quindi fare clic su **Sfoglia**.  
  
##  <a name="options"></a> Configurare le opzioni  
 In questa pagina vengono visualizzate le entità della vista del catalogo sys.database_principals del database SSISDB.  
  
 Tramite la selezione le entità vengono aggiunte all'elenco **Account di accesso o ruoli** nella pagina **Autorizzazioni** della finestra di dialogo padre quando si fa clic su **OK** e si chiude la finestra di dialogo **Sfoglia tutte le entità** . Dopo aver aggiunto le entità all'elenco **Account di accesso o ruoli** , è possibile modificare le autorizzazioni per il progetto selezionato.  
  
 **Colonna Selezione**  
 Selezionare per aggiungere l'entità all'elenco **Account di accesso o ruoli** nella pagina **Autorizzazioni** della finestra di dialogo padre.  
  
 **Colonna Icona**  
 Icona che corrisponde al **Tipo** di entità.  
  
 **Name**  
 Nome dell'entità.  
  
 **Tipo**  
 Tipo dell'entità. I tipi comuni sono:  
  
-   Utente SQL  
  
-   Utente di Windows  
  
-   Ruolo del database  
  
  
