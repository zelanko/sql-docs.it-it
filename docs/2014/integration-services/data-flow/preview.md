---
title: Anteprima | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 551494c4-9e27-4592-9200-c6bf19e80c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0b0f81c5de267d6e85525714d19999920ba9c71
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393619"
---
# <a name="preview"></a>Anteprima
  Utilizzare la finestra di dialogo **Anteprima** per visualizzare in anteprima i dati che verranno estratti dall'origine SAP BW.  
  
> [!IMPORTANT]  
>  Con l'opzione **Anteprima** , disponibile nella pagina **Gestione connessione** dell' **Editor di origine SAP BW**, vengono effettivamente estratti i dati. Se è stato configurato SAP Netweaver BW per estrarre solo i dati modificati dall'estrazione precedente, la selezione di **Anteprima** escluderà i dati visualizzati in anteprima dall'estrazione successiva.  
  
 Per altre informazioni sul componente di origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 **Per aprire la finestra di dialogo Anteprima.**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Configurare l'origine SAP BW.  
  
5.  Dopo aver configurato l'origine SAP BW, nella pagina **Gestione connessione** fare clic su **Anteprima** per visualizzare in anteprima i dati nella finestra di dialogo **Anteprima** .  
  
    > [!NOTE]  
    >  Quando si fa clic su **Anteprima** , inoltre, viene aperta la finestra di dialogo **Log richieste** . Per altre informazioni su questa finestra di dialogo, vedere [Request Log](request-log.md).  
  
## <a name="options"></a>Opzioni  
 Nella finestra di dialogo **Anteprima** vengono visualizzate le righe richieste dal sistema SAP Netweaver BW. Le colonne visualizzate sono le colonne definite nei dati di origine.  
  
 In questa finestra di dialogo non sono presenti altre opzioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
