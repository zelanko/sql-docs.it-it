---
description: Editor destinazione SAP BW (pagina Mapping)
title: Editor destinazione SAP BW (pagina Mapping) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.columns.f1
ms.assetid: dfa1f1d6-6b64-4331-bdc5-eaa8b7aa41a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f1c92a8976e22648768c3f4986d9c1ff13a35f55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430803"
---
# <a name="sap-bw-destination-editor-mappings-page"></a>Editor destinazione SAP BW (pagina Mapping)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Usare la pagina **Mapping** dell' **Editor destinazione SAP BW** per eseguire il mapping delle colonne di input alle colonne di destinazione.  
  
 Per altre informazioni sulla destinazione SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Destinazione SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la pagina Mapping**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Mapping** per aprire la pagina **Mapping** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare la destinazione, può essere necessario consultare l'amministratore SAP.  
  
 La pagina **Mapping** dell' **Editor destinazione SAP BW** contiene due sezioni:  
  
-   Nella sezione superiore sono visualizzate le colonne di input e di destinazione disponibili ed è possibile creare mapping tra i due tipi di colonne.  
  
-   Nella sezione inferiore è riportata una tabella che mostra i mapping tra le colonne di input e le colonne di output.  
  
### <a name="upper-section-options"></a>Opzioni della sezione superiore  
 Nella sezione superiore sono presenti le seguenti opzioni:  
  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili.  
  
 Per eseguire il mapping di una colonna di input a una colonna di destinazione, trascinare una colonna dall'elenco **Colonne di input disponibili** su una colonna dell'elenco **Colonne di destinazione disponibili** .  
  
 **Colonne di destinazione disponibili**  
 Consente di visualizzare l'elenco delle colonne di destinazione disponibili.  
  
 Per eseguire il mapping di una colonna di input a una colonna di destinazione, trascinare una colonna dall'elenco **Colonne di input disponibili** su una colonna dell'elenco **Colonne di destinazione disponibili** .  
  
 Nella sezione superiore è inoltre presente un menu di scelta rapida che è possibile aprire facendo clic con il pulsante destro del mouse sullo sfondo. Nel menu di scelta rapida sono presenti le opzioni seguenti:  
  
-   **Seleziona tutti i mapping**  
  
-   **Elimina mapping selezionati**  
  
-   **Mappa elementi tramite corrispondenza nomi**  
  
### <a name="lower-section-columns"></a>Colonne della sezione inferiore  
 La sezione inferiore è una tabella dei mapping e contiene le colonne seguenti:  
  
 **Colonna di input**  
 Visualizzare le colonne di input selezionate.  
  
 Per eseguire il mapping di un'altra colonna di input alla stessa colonna di destinazione, selezionare un'altra colonna di input nell'elenco. Per rimuovere un mapping, selezionare **\<ignore>** per escludere la colonna di input dall'output.  
  
 **Colonna di destinazione**  
 Visualizzare ogni colonna di destinazione disponibile, indipendentemente dal fatto che ne venga eseguito il mapping.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Editor destinazione SAP BW &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Editor destinazione SAP BW &#40;pagina Avanzate&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
