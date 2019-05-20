---
title: Cerca InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7c0cb7a4-cd07-44cc-85cb-eb1ad91f85fd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c78416e70f9d37dbedf338b0475bbcb4fdf7a208
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726726"
---
# <a name="look-up-infopackage"></a>Cerca InfoPackage

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilizzare la finestra di dialogo **Cerca InfoPackage** per cercare un InfoPackage definito nel sistema SAP Netweaver BW. Quando viene visualizzato l'elenco di InfoPackage, selezionare l'InfoPackage desiderato e le opzioni associate verranno compilate con i valori richiesti dalla destinazione.  
  
 La destinazione SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW utilizza la finestra di dialogo **Cerca ProcessChain** . Per ulteriori informazioni sulla destinazione SAP BW, vedere [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Cerca InfoPackage**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella pagina **Gestione connessione** , nella casella di gruppo **InfoPackage/InfoSource** fare clic su **Ricerca** per visualizzare la finestra di dialogo **Cerca InfoPackage** .  
  
## <a name="lookup-options"></a>Opzioni di ricerca  
 Nei campi di ricerca è possibile filtrare i risultati tramite il carattere jolly asterisco (*) oppure utilizzando una stringa parziale in combinazione con il carattere jolly asterisco. Tuttavia, se si lascia un campo di ricerca vuoto, l'operazione di ricerca restituirà solo stringhe vuote in tale campo.  
  
 **InfoPackage**  
 Immettere il nome dell'InfoPackage da cercare oppure un nome parziale con il carattere jolly asterisco (*). In alternativa, utilizzare il carattere jolly asterisco da solo per includere tutti gli InfoPackage.  
  
 **InfoSource**  
 Immettere il nome dell'InfoSource oppure un nome parziale con il carattere jolly asterisco (*). In alternativa, utilizzare il carattere jolly asterisco da solo per includere tutti gli InfoPackage indipendentemente dall'InfoSource.  
  
 **Sistema di origine**  
 Immettere il nome del sistema di origine o un nome parziale con il carattere jolly asterisco (*). In alternativa, utilizzare il carattere jolly asterisco da solo per includere tutti gli InfoPackage indipendentemente dai sistemi di origine.  
  
 **Cerca**  
 Cercare gli InfoPackage corrispondenti definiti nel sistema SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Risultati di ricerca  
 Dopo avere fatto clic sul pulsante Ricerca, viene visualizzato un elenco di InfoPackage nel sistema SAP Netweaver BW in una tabella con le intestazioni di colonna seguenti.  
  
 **InfoPackage**  
 Visualizza il nome dell'InfoPackage definito nel sistema SAP Netweaver BW.  
  
 **Tipo**  
 Visualizza il tipo di InfoPackage. Nella tabella seguente sono elencati i valori possibili per il tipo.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|transazioni|Dati di transazione.|  
|Attr.|Dati dell'attributo.|  
|Testi|Testi.|  
  
 **Descrizione**  
 Visualizza la descrizione dell'InfoPackage.  
  
 **InfoSource**  
 Visualizza il nome dell'InfoSource, se esistente, associato all'InfoPackage.  
  
 **Source System**  
 Visualizza il nome del sistema di origine.  
  
 Quando viene visualizzato l'elenco di InfoPackage, selezionare l'InfoPackage desiderato e le opzioni associate verranno compilate con i valori richiesti dalla destinazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Guida (F1) di Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
