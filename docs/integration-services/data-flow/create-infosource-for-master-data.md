---
title: Crea InfoSource per dati master | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1fb9be98dbbdf2935fe79c6f579be7ab0e357624
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71293204"
---
# <a name="create-infosource-for-master-data"></a>Crea InfoSource per dati master

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Usare la finestra di dialogo **Crea InfoSource per dati master** per creare un nuovo InfoSource per i dati master nel sistema SAP Netweaver BW.  
  
 È possibile aprire la finestra di dialogo **Crea InfoSource per dati master** dalla pagina **Gestione connessione** dell' **Editor destinazione SAP BW**. Per ulteriori informazioni sulla destinazione SAP BW, vedere [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Crea InfoSource per dati master**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella casella di gruppo **Crea oggetti SAP BW** della pagina **Gestione connessione** selezionare **InfoSource**, quindi fare clic su **Crea**.  
  
5.  Nella finestra di dialogo **Crea InfoSource** selezionare **Dati master**, quindi fare clic su **OK**.  
  
## <a name="options"></a>Opzioni  
 **Nome InfoObject**  
 Immettere il nome dell'InfoObject su cui deve essere basato il nuovo InfoSource.  
  
 **Cerca**  
 Cercare l'InfoObject. Tramite questa opzione viene visualizzata la finestra di dialogo **Cerca InfoObject** in cui è possibile selezionare l'InfoObject. Per altre informazioni su questa finestra di dialogo, vedere [Cerca InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 Dopo aver selezionato un InfoObject, la casella di testo **Nome InfoObject** viene compilata dal componente con il nome dell'InfoObject selezionato.  
  
 **Nuovo**  
 Creare un nuovo InfoObject. Tramite questa opzione viene visualizzata la finestra di dialogo **Crea nuovo InfoObject** in cui è possibile creare il nuovo InfoObject. Per altre informazioni su questa finestra di dialogo, vedere [Crea nuovo InfoObject](../../integration-services/data-flow/create-new-infoobject.md).  
  
 Dopo aver creato un InfoObject, la casella di testo **Nome InfoObject** viene compilata dal componente con il nome del nuovo InfoObject.  
  
 **Descrizione breve**  
 Immettere una breve descrizione per il nuovo InfoSource.  
  
 **Descrizione lunga**  
 Immettere una descrizione lunga per il nuovo InfoSource.  
  
 **Sistema di origine**  
 Selezionare il sistema di origine da associare al nuovo InfoSource.  
  
 **Applicazione**  
 Immettere il nome dell'applicazione da associare al nuovo InfoSource.  
  
 **Attributes (Attributi)**  
 Indica che i dati master sono costituiti da attributi.  
  
 **Testi**  
 Indica che i dati master sono costituiti da attributi.  
  
 **Salva e attiva**  
 Salvare e attivare il nuovo InfoSource.  
  
## <a name="see-also"></a>Vedere anche  
 [Crea InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
