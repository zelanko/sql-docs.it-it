---
title: Impostare le proprietà di una gestione connessione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], modifying
- modifying connection managers
ms.assetid: 54793114-2198-4d80-8091-e241d5a5d13c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c8581771394ed40f740ea83407b9acd47c6f4ddd
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963238"
---
# <a name="set-the-properties-of-a-connection-manager"></a>Impostazione delle proprietà di una gestione connessione
  Tutti i tipi di gestione connessione possono essere configurati nella finestra **Proprietà** .  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include anche finestre di dialogo personalizzate per la modifica dei vari tipi di gestione connessione in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Queste finestre di dialogo includono opzioni diverse a seconda del tipo di gestione connessione.  
  
### <a name="to-modify-a-connection-manager-using-the-properties-window"></a>Per modificare una gestione connessione utilizzando la finestra Proprietà  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione SSIS fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Fare clic con il pulsante destro del mouse sulla gestione connessione e quindi scegliere **Proprietà**.  
  
5.  Nella finestra **Proprietà** modificare i valori delle proprietà. La finestra **Proprietà** consente di accedere ad alcune proprietà che non è possibile configurare nell'editor standard di una gestione connessione.  
  
6.  Fare clic su **OK**.  
  
7.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
### <a name="to-modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Per modificare una gestione connessione tramite la relativa finestra di dialogo  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] fare clic sulla scheda **Flusso di controllo** , **Flusso di dati** o **Gestore evento** in modo da rendere disponibile l'area **Gestioni connessioni** .  
  
4.  Nell'area **Gestioni connessioni** fare doppio clic sulla gestione connessione desiderata. Verrà visualizzata la finestra di dialogo **Gestione connessione** . Per informazioni su tipi di gestione connessione specifici e sulle opzioni disponibili per ogni tipo di gestione connessione, vedere la tabella seguente.  
  
    |Gestione connessione|Opzioni|  
    |------------------------|-------------|  
    |[Gestione connessione ADO](connection-manager/ado-connection-manager.md)|[Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gestione connessione ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configura gestione connessione ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Gestione connessione Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione Excel](connection-manager/excel-connection-manager.md)|[Editor gestione connessione Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Gestione connessione file](connection-manager/file-connection-manager.md)|[Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Gestione connessione per più file](connection-manager/multiple-files-connection-manager.md)|[Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gestione connessione file flat](connection-manager/flat-file-connection-manager.md)|[Editor gestione connessione file flat &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione per più file flat](connection-manager/multiple-flat-files-connection-manager.md)|[Editor gestione connessione per più file flat &#40;pagina Generale&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Colonne&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor gestione connessione per più file flat &#40;pagina Anteprima&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gestione connessione FTP](connection-manager/ftp-connection-manager.md)|[Editor gestione connessione FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Gestione connessione HTTP](connection-manager/http-connection-manager.md)|[Editor gestione connessione HTTP &#40;pagina Server&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor gestione connessione HTTP &#40;pagina Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Gestione connessione MSMQ](connection-manager/msmq-connection-manager.md)|[Editor gestione connessione MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Gestione connessione ODBC](connection-manager/odbc-connection-manager.md)|[Riferimento all'interfaccia utente di Gestione connessione ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md)|[Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gestione connessione SMO](connection-manager/smo-connection-manager.md)|[Editor gestione connessione SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Gestione connessione SMTP](connection-manager/smtp-connection-manager.md)|[Editor gestione connessione SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Gestione connessione SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor gestione connessione SQL Server Compact Edition &#40;pagina Connessione&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor gestione connessione SQL Server Compact Edition &#40;pagina Tutte&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gestione connessione WMI](connection-manager/wmi-connection-manager.md)|[Editor gestione connessione WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
5.  Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;connessioni SSIS&#41;](connection-manager/integration-services-ssis-connections.md)   
 [Aggiunta, eliminazione o condivisione di una gestione connessione in un pacchetto](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
  
