---
title: Editor destinazione SAP BW (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwdestination.connection.f1
ms.assetid: 04ae38f8-5287-45a3-826a-8aac5dd15a91
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 66365c942bc3f996d834f0217f29bd82cc911457
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298110"
---
# <a name="sap-bw-destination-editor-connection-manager-page"></a>Editor destinazione SAP BW (pagina Gestione connessione)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione SAP BW** per selezionare la gestione connessione SAP BW che verrà usata dalla destinazione SAP BW. In questa pagina vengono inoltre selezionati i parametri per il caricamento dei dati nel sistema SAP Netweaver BW.  
  
 Per altre informazioni sulla destinazione SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Destinazione SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
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
  
 **Nuovo**  
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
  
|valore|Descrizione|  
|-----------|-----------------|  
|**D**|Dati transazione|  
|**M**|Dati master|  
|**T**|Testi|  
|**H**|Dati gerarchia|  
  
 **Sistema logico**  
 Immettere il nome del sistema logico associato all'InfoPackage.  
  
 **Cerca**  
 Individuare l'InfoPackage usando la finestra di dialogo **Cerca InfoPackage** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca InfoPackage](../../integration-services/data-flow/look-up-infopackage.md).  
  
### <a name="rfc-destination-options"></a>Opzioni della destinazione RFC  
 Non è necessario conoscere e immettere questi valori in anticipo. Usare il pulsante **Ricerca** per individuare e selezionare la destinazione RFC appropriata. Dopo aver selezionato una destinazione RFC, il componente inserisce i valori appropriati per queste opzioni.  
  
 **Host gateway**  
 Immettere il nome server o l'indirizzo IP dell'host gateway. In genere, il nome o l'indirizzo IP è uguale a quello del server applicazioni SAP.  
  
 **Servizio gateway**  
 Immettere il nome del servizio del gateway, nel formato **sapgwNN**, dove **NN** è il numero del sistema.  
  
 **ID programma**  
 Immettere l'ID programma associato alla destinazione RFC.  
  
 **Cerca**  
 Individuare la destinazione RFC usando la finestra di dialogo **Cerca destinazione RFC** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca destinazione RFC](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
### <a name="create-sap-bw-objects-options"></a>Opzioni di Crea oggetti SAP BW  
 **Seleziona il tipo di oggetto**  
 Selezionare il tipo di oggetto SAP Netweaver BW che si desidera creare. È possibile selezionare uno dei tipi seguenti:  
  
-   InfoObject  
  
-   InfoCube  
  
-   InfoSource  
  
-   InfoPackage  
  
 **Creare**  
 Creare il tipo selezionato di oggetto SAP Netweaver BW.  
  
|Tipo di oggetto|Risultato|  
|-----------------|------------|  
|**InfoObject**|Creare un nuovo InfoObject usando la finestra di dialogo **Crea nuovo InfoObject** . Per altre informazioni su questa finestra di dialogo, vedere [Crea nuovo InfoObject](../../integration-services/data-flow/create-new-infoobject.md).|  
|**InfoCube**|Creare un nuovo InfoCube usando la finestra di dialogo **Crea InfoCube per dati transazione** . Per altre informazioni su questa finestra di dialogo, vedere [Crea InfoCube per dati transazione](../../integration-services/data-flow/create-infocube-for-transaction-data.md).|  
|**InfoSource**|Creare un nuovo InfoSource usando la finestra di dialogo **Crea InfoSource** e quindi la finestra di dialogo **Crea InfoSource per dati transazione** o **Crea InfoSource per dati master** . Per altre informazioni su queste finestre di dialogo, vedere [Crea InfoSource](../../integration-services/data-flow/create-infosource.md), [Crea InfoSource per dati transazione](../../integration-services/data-flow/create-infosource-for-transaction-data.md) e [Crea InfoSource per dati master](../../integration-services/data-flow/create-infosource-for-master-data.md).|  
|**InfoPackage**|Creare un nuovo InfoPackage usando la finestra di dialogo **Crea InfoPackage** . Per altre informazioni su questa finestra di dialogo, vedere [Crea InfoPackage](../../integration-services/data-flow/create-infopackage.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione SAP BW &#40;pagina Mapping&#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [Editor destinazione SAP BW &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)   
 [Editor destinazione SAP BW &#40;pagina Avanzate&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
