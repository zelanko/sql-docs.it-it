---
description: Finestra di dialogo Sfoglia tutte le entità
title: Finestra di dialogo Sfoglia tutte le entità | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f5ec280020b966a1d23b5ebb9dfb2c740692a6d1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123789"
---
# <a name="browse-all-principals-dialog-box"></a>Finestra di dialogo Sfoglia tutte le entità

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare la finestra di dialogo **Sfoglia tutte le entità** per selezionare un'entità di database per modificare le autorizzazioni dell'entità per il progetto selezionato o per tutti i progetti contenuti in una cartella selezionata.  
  
 **Per saperne di più**  
  
-   [Aprire la finestra di dialogo Sfoglia tutte le entità](#open_dialog)  
  
-   [Configurare le opzioni](#options)  
  
##  <a name="open-the-browse-all-principals-dialog-box"></a><a name="open_dialog"></a> Aprire la finestra di dialogo Sfoglia tutte le entità  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Verrà eseguita la connessione all'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] in cui è ospitato il catalogo SSISDB.  
  
2.  In Esplora oggetti espandere l'albero per visualizzare il nodo dei **cataloghi di Integration Services** .  
  
3.  Espandere il nodo **SSISDB** .  
  
4.  Per modificare le autorizzazioni dell'entità per tutti i progetti contenuti in una cartella selezionata, fare clic con il pulsante destro del mouse sulla cartella, quindi scegliere **Proprietà**.  
  
     Per modificare le autorizzazioni dell'entità per un progetto selezionato, espandere la cartella che contiene il progetto, fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Proprietà**.  
  
5.  Selezionare la pagina **Autorizzazioni** , quindi fare clic su **Sfoglia**.  
  
##  <a name="configure-the-options"></a><a name="options"></a> Configurare le opzioni  
 In questa pagina vengono visualizzate le entità della vista del catalogo sys.database_principals del database SSISDB.  
  
 Tramite la selezione le entità vengono aggiunte all'elenco **Account di accesso o ruoli** nella pagina **Autorizzazioni** della finestra di dialogo padre quando si fa clic su **OK** e si chiude la finestra di dialogo **Sfoglia tutte le entità** . Dopo aver aggiunto le entità all'elenco **Account di accesso o ruoli** , è possibile modificare le autorizzazioni per il progetto selezionato.  
  
 **Colonna Selezione**  
 Selezionare per aggiungere l'entità all'elenco **Account di accesso o ruoli** nella pagina **Autorizzazioni** della finestra di dialogo padre.  
  
 **Colonna Icona**  
 Icona che corrisponde al **Tipo** di entità.  
  
 **Nome**  
 Nome dell'entità.  
  
 **Tipo**  
 Tipo dell'entità. I tipi comuni sono:  
  
-   Utente SQL  
  
-   Utente di Windows  
  
-   Ruolo del database  
  
  
