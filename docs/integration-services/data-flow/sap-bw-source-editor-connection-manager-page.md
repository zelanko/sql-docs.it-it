---
title: Editor origine SAP BW (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.connection.f1
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 041f05a2d7ae623ee40db320676555dad5468459
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726393"
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>Editor origine SAP BW (pagina Gestione connessione)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor origine SAP BW** per selezionare la gestione connessione SAP BW per l'origine SAP BW. In questa pagina vengono inoltre selezionati la modalità di esecuzione e i parametri per estrarre i dati dal sistema SAP Netweaver BW.  
  
 Per altre informazioni sul componente di origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 **Per aprire la pagina Gestione connessione**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
## <a name="static-options"></a>Opzioni statiche  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare l'origine, può essere necessario consultare l'amministratore SAP.  
  
 **Gestione connessione SAP BW**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Creare una nuova gestione connessione usando la finestra di dialogo **Gestione connessione SAP BW** .  
  
 Per altre informazioni sulla questa finestra di dialogo, vedere [Editor gestione connessione SAP BW](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md).  
  
 **Destinazione OHS**  
 Selezionare la destinazione OHS (Open Hub Service) da utilizzare per estrarre i dati dall'origine.  
  
 **Modalità di esecuzione**  
 Specificare il metodo per l'estrazione dei dati dall'origine.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**P - Attivazione catena processi**|Attivare una catena di processi. In questo caso, il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] avvia il processo di estrazione.|  
|**W - Attesa notifica**|Attendere la notifica dal sistema SAP Netweaver BW per avviare l'estrazione dei dati. In questo caso, il sistema SAP Netweaver BW avvia il processo di estrazione.|  
|**E - Solo estrazione**|Recuperare i dati associati a un ID richiesta specifico. In questo caso, il sistema SAP Netweaver BW ha già estratto i dati in una tabella interna e il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] legge solo i dati.|  
  
 **Anteprima**  
 Aprire la finestra di dialogo **Anteprima** in cui è possibile visualizzare i risultati in anteprima. Per altre informazioni, vedere [Anteprima](../../integration-services/data-flow/preview.md).  
  
> [!IMPORTANT]  
>  Con l'opzione **Anteprima** , disponibile nella pagina **Gestione connessione** dell'Editor di origine SAP BW, vengono effettivamente estratti i dati. Se è stato configurato SAP Netweaver BW per estrarre solo i dati modificati dall'estrazione precedente, la selezione di **Anteprima** escluderà i dati visualizzati in anteprima dall'estrazione successiva.  
  
 Quando si fa clic su **Anteprima**, viene inoltre aperta la finestra di dialogo **Log richieste** . È possibile utilizzare questa finestra di dialogo per visualizzare gli eventi registrati durante la richiesta fatta al sistema SAP Netweaver BW per i dati di esempio. Per altre informazioni, vedere [Log richieste](../../integration-services/data-flow/request-log.md).  
  
## <a name="execution-mode-dynamic-options"></a>Opzioni dinamiche della modalità di esecuzione  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare l'origine, può essere necessario consultare l'amministratore SAP.  
  
### <a name="execution-mode--p---trigger-process-chain"></a>Modalità di esecuzione = P - Attivazione catena di processi  
  
#### <a name="rfc-destination-options"></a>Opzioni della destinazione RFC  
 Non è necessario conoscere e immettere questi valori in anticipo. Usare il pulsante **Ricerca** per individuare e selezionare la destinazione RFC appropriata. Dopo aver selezionato una destinazione RFC, il componente inserisce i valori appropriati per queste opzioni.  
  
 **Host gateway**  
 Immettere il nome server o l'indirizzo IP dell'host gateway. In genere, il nome o l'indirizzo IP è uguale a quello del server applicazioni SAP.  
  
 **Servizio gateway**  
 Immettere il nome del servizio del gateway, nel formato **sapgwNN**, dove **NN** è il numero del sistema.  
  
 **ID programma**  
 Immettere l'ID programma associato alla destinazione RFC.  
  
 **Cerca**  
 Individuare la destinazione RFC usando la finestra di dialogo **Cerca destinazione RFC** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca destinazione RFC](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
#### <a name="process-chain-options"></a>Opzioni della catena di processi  
 Non è necessario conoscere e immettere questi valori in anticipo. Usare il pulsante **Ricerca** per individuare e selezionare la catena di processi appropriata. Dopo aver selezionato una catena di processi, il componente inserisce il valore appropriato per l'opzione.  
  
 **Catena di processi**  
 Immettere il nome della catena di processi che verrà attivata da parte dell'origine.  
  
 **Cerca**  
 Individuare la catena di processi usando la finestra di dialogo **Cerca ProcessChain** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca ProcessChain](../../integration-services/data-flow/look-up-process-chain.md).  
  
### <a name="execution-mode--w---wait-for-notify"></a>Modalità di esecuzione = W - Attesa notifica  
  
#### <a name="rfc-destination-options"></a>Opzioni della destinazione RFC  
 Non è necessario conoscere e immettere questi valori in anticipo. Usare il pulsante **Ricerca** per individuare e selezionare la destinazione RFC appropriata. Dopo aver selezionato una destinazione RFC, il componente inserisce i valori appropriati per le opzioni.  
  
 **Host gateway**  
 Immettere il nome server o l'indirizzo IP dell'host gateway. In genere, il nome o l'indirizzo IP è uguale a quello del server applicazioni SAP.  
  
 **Servizio gateway**  
 Immettere il nome del servizio del gateway, nel formato **sapgwNN**, dove **NN** è il numero del sistema.  
  
 **ID programma**  
 Immettere l'ID programma associato alla destinazione RFC.  
  
 **Cerca**  
 Individuare la destinazione RFC usando la finestra di dialogo **Cerca destinazione RFC** . Per altre informazioni su questa finestra di dialogo, vedere [Cerca destinazione RFC](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
### <a name="execution-mode--e---extract-only"></a>Modalità di esecuzione = E - Solo estrazione  
 **ID richiesta**  
 Immettere l'ID richiesta associato all'estrazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Colonne&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Editor origine SAP BW &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Editor origine SAP BW &#40;pagina Avanzate&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
