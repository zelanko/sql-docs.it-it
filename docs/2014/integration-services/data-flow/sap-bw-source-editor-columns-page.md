---
title: Editor origine SAP BW (pagina Colonne) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c2ec8bb7-be9b-4783-ad88-32512de784b0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 066e50249d8f39303e98ff7647c3cf88b8202095
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437738"
---
# <a name="sap-bw-source-editor-columns-page"></a>Editor origine SAP BW (pagina Colonne)
  Usare la pagina **Colonne** della finestra di dialogo **Editor origine SAP BW** per eseguire il mapping di una colonna di output a ogni colonna esterna (di origine).  
  
 Per altre informazioni sul componente di origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 **Per aprire la pagina Colonne**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Colonne** per aprire la pagina **Colonne** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare l'origine, può essere necessario consultare l'amministratore SAP.  
  
 **Colonne esterne disponibili**  
 Visualizzare l'elenco delle colonne esterne disponibili nell'origine dati, quindi selezionare le colonne da includere nel flusso di dati.  
  
 Per includere una colonna nel flusso di dati, selezionare la casella di controllo corrispondente a tale colonna. L'ordine di selezione delle caselle di controllo determina l'ordine di restituzione delle colonne. La prima casella di controllo selezionata sarà la prima colonna di output, la seconda casella di controllo sarà la seconda colonna di output e così via.  
  
 **Colonna esterna**  
 Visualizzare le colonne (di origine) esterne selezionate. Le colonne selezionate sono visualizzate nell'ordine di visualizzazione delle colonne di output corrispondenti quando si configurano i componenti a valle che utilizzano i dati di tale origine.  
  
 Per modificare l'ordine delle colonne, nell'elenco **Colonne esterne disponibili** deselezionare le caselle di controllo per tutte le colonne. Selezionare quindi le colonne nell'ordine in cui si desidera visualizzarle.  
  
 **Colonna di output**  
 Consente di specificare un nome univoco per ogni colonna di output. L'impostazione predefinita è il nome della colonna (di origine) esterna selezionata. Tuttavia, è possibile immettere qualsiasi nome descrittivo univoco. [!INCLUDE[ssIS](../../includes/ssis-md.md)] verranno visualizzati i nomi di **Colonna di output** per le colonne quando si configurano i componenti a valle che utilizzano i dati di questa origine.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor origine SAP BW &#40;pagina Output degli errori&#41;](sap-bw-source-editor-error-output-page.md)   
 [Editor origine SAP BW &#40;pagina Avanzate&#41;](sap-bw-source-editor-advanced-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
