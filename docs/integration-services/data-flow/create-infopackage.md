---
description: Crea InfoPackage
title: Crea InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9cd4a848-409f-4681-a390-1c49a2aadbd7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38c7183853dcac7043672d5e4a622362af08c10b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127280"
---
# <a name="create-infopackage"></a>Crea InfoPackage

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare la finestra di dialogo **Crea InfoPackage** per creare un nuovo InfoPackage nel sistema SAP Netweaver BW.  
  
 È possibile aprire la finestra di dialogo **Crea InfoPackage** dalla pagina **Gestione connessione** dell' **Editor destinazione SAP BW**. Per ulteriori informazioni sulla destinazione SAP BW, vedere [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Crea InfoPackage**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW** fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella casella di gruppo **Crea oggetti SAP BW** della pagina **Gestione connessione** selezionare **InfoPackage** e quindi fare clic su **Crea**.  
  
## <a name="options"></a>Opzioni  
 **InfoSource**  
 Immettere il nome dell'InfoSource su cui deve essere basato il nuovo InfoPackage.  
  
 **Breve descrizione**  
 Immettere una descrizione per il nuovo InfoPackage.  
  
 **Sistema di origine**  
 Selezionare il sistema di origine con cui deve essere associato il nuovo InfoPackage.  
  
 **Attributes (Attributi)**  
 Indica che l'InfoPackage caricherà i dati dell'attributo.  
  
 **Testi**  
 Indica che l'InfoPackage caricherà i dati del testo.  
  
 **Transazione**  
 Indica che l'InfoPackage caricherà i dati della transazione.  
  
 **Salva e attiva**  
 Salvare e attivare il nuovo InfoPackage.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
