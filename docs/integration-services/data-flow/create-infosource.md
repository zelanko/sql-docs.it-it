---
description: Crea InfoSource
title: Crea InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4672ce48890af7202445d283d15c2c167550f5a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495930"
---
# <a name="create-infosource"></a>Crea InfoSource

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare la finestra di dialogo **Crea InfoSource** per creare un nuovo InfoSource. Per creare il nuovo InfoSource, usare la finestra di dialogo **Crea InfoSource per dati transazione** o **Crea InfoSource per dati master** .  
  
 È possibile aprire la finestra di dialogo **Crea InfoSource** dalla pagina **Gestione connessione** dell' **Editor destinazione SAP BW**. Per ulteriori informazioni sulla destinazione SAP BW, vedere [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Crea InfoSource**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella casella di gruppo **Crea oggetti SAP BW** della pagina **Gestione connessione** selezionare **InfoSource**, quindi fare clic su **Crea**.  
  
## <a name="options"></a>Opzioni  
 **Dati transazione**  
 Creare un nuovo InfoSource per i dati della transazione.  
  
 Se si seleziona questa opzione, viene visualizzata la finestra di dialogo **Crea InfoSource per dati transazione** . Usare la finestra di dialogo **Crea InfoSource per dati transazione** per creare il nuovo InfoSource. Per altre informazioni su questa finestra di dialogo, vedere [Crea InfoSource per dati transazione](../../integration-services/data-flow/create-infosource-for-transaction-data.md).  
  
 **Dati master**  
 Creare un nuovo InfoSource per i dati master.  
  
 Se si seleziona questa opzione, viene visualizzata la finestra di dialogo **Crea InfoSource per dati master** . Usare la finestra di dialogo **Crea InfoSource per dati master** per creare il nuovo InfoSource. Per altre informazioni su questa finestra di dialogo, vedere [Crea InfoSource per dati master](../../integration-services/data-flow/create-infosource-for-master-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
