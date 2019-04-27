---
title: Editor destinazione SAP BW (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04ae38f8-5287-45a3-826a-8aac5dd15a91
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e4e23849b50e8cfa0a0e8d3ef6def4fbd159381c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770847"
---
# <a name="sap-bw-destination-editor-connection-manager-page"></a>Editor destinazione SAP BW (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione SAP BW** per selezionare la gestione connessione SAP BW che verrà usata dalla destinazione SAP BW. In questa pagina vengono inoltre selezionati i parametri per il caricamento dei dati nel sistema SAP Netweaver BW.  
  
 Per altre informazioni sulla destinazione SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Destinazione SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la pagina Gestione connessione**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare la destinazione, può essere necessario consultare l'amministratore SAP.  
  
 **Gestione connessione SAP BW**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Creare una nuova gestione connessione usando la finestra di dialogo **Gestione connessione SAP BW** .  
  
 **Test del carico**  
 Eseguire un test del processo di caricamento che utilizzi le impostazioni selezionate e carichi zero righe.  
  
### <a name="infopackageinfosource-options"></a>Opzioni di InfoPackage/InfoSource  
 Non è necessario conoscere e immettere questi valori in anticipo. Usare il pulsante **Ricerca** per individuare e selezionare l'InfoPackage appropriato. Dopo aver selezionato un InfoPackage, il componente inserisce i valori appropriati per queste opzioni.  
  
 **InfoPackage**  
 Immettere il nome dell'InfoPackage.  
  
 **InfoSource**  
 Immettere il nome dell'InfoSource.  
  
 **Tipo**  
 Immettere il carattere singolo che identifica il tipo di InfoSource. Nella tabella seguente sono elencati i valori a carattere singolo accettabili.  
  
|Valore|Descrizione|  
|-----------|-----------------|  
|**D**|Dati transazione|  
|**M**|Dati master|  
|**T**|Testi|  
|**H**|Dati gerarchia|  
  
 **Sistema logico**  
 Immettere il nome del sistema logico associato all'InfoPackage.  
  
 **Cerca**  
 Individuare l'InfoPackage usando la finestra di dialogo **Cerca InfoPackage** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca InfoPackage](look-up-infopackage.md).  
  
### <a name="rfc-destination-options"></a>Opzioni della destinazione RFC  
 Non è necessario conoscere e immettere questi valori in anticipo. Usare il pulsante **Ricerca** per individuare e selezionare la destinazione RFC appropriata. Dopo aver selezionato una destinazione RFC, il componente inserisce i valori appropriati per queste opzioni.  
  
 **Host gateway**  
 Immettere il nome server o l'indirizzo IP dell'host gateway. In genere, il nome o l'indirizzo IP è uguale a quello del server applicazioni SAP.  
  
 **Servizio gateway**  
 Immettere il nome del servizio gateway, nel formato `sapgwNN`, dove `NN` è il numero del sistema.  
  
 **ID programma**  
 Immettere l'ID programma associato alla destinazione RFC.  
  
 **Cerca**  
 Individuare la destinazione RFC usando la finestra di dialogo **Cerca destinazione RFC** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca InfoPackage](look-up-rfc-destination.md).  
  
### <a name="create-sap-bw-objects-options"></a>Opzioni di Crea oggetti SAP BW  
 **Seleziona il tipo di oggetto**  
 Selezionare il tipo di oggetto SAP Netweaver BW che si desidera creare. È possibile selezionare uno dei tipi seguenti:  
  
-   InfoObject  
  
-   InfoCube  
  
-   InfoSource  
  
-   InfoPackage  
  
 **Creare**  
 Creare il tipo selezionato di oggetto SAP Netweaver BW.  
  
|Tipo oggetto|Risultato|  
|-----------------|------------|  
|**InfoObject**|Creare un nuovo InfoObject usando la finestra di dialogo **Crea nuovo InfoObject** . Per altre informazioni su questa finestra di dialogo, vedere [Crea nuovo InfoObject](create-new-infoobject.md).|  
|**InfoCube**|Creare un nuovo InfoCube usando la finestra di dialogo **Crea InfoCube per dati transazione** . Per altre informazioni su questa finestra di dialogo, vedere [Crea InfoCube per dati transazione](create-infocube-for-transaction-data.md).|  
|**InfoSource**|Creare un nuovo InfoSource usando la finestra di dialogo **Crea InfoSource** e quindi la finestra di dialogo **Crea InfoSource per dati transazione** o **Crea InfoSource per dati master** . Per altre informazioni su queste finestre di dialogo, vedere [Crea InfoSource](create-infosource.md), [Crea InfoSource per dati transazione](create-infosource-for-transaction-data.md) e [Crea InfoSource per dati master](create-infosource-for-master-data.md).|  
|**InfoPackage**|Creare un nuovo InfoPackage usando la finestra di dialogo **Crea InfoPackage** . Per altre informazioni su questa finestra di dialogo, vedere [Crea InfoPackage](create-infopackage.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione SAP BW &#40;pagina Mapping&#41;](sap-bw-destination-editor-mappings-page.md)   
 [Editor destinazione SAP BW &#40;pagina Output degli errori&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Editor destinazione SAP BW &#40;pagina Avanzate&#41;](sap-bw-destination-editor-advanced-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
