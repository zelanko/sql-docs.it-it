---
title: Cerca destinazione RFC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4badd9c961f5a0d7ca2d3e32185a7ab742628d97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901785"
---
# <a name="look-up-rfc-destination"></a>Cerca destinazione RFC
  Usare la finestra di dialogo **Cerca destinazione RFC** per cercare una destinazione RFC definita nel sistema SAP Netweaver BW. Quando viene visualizzato l'elenco delle destinazioni RFC disponibili, selezionare la destinazione desiderata e le opzioni associate verranno compilate con i valori richiesti dal componente.  
  
 Sia l'origine che la destinazione SAP BW usano la finestra di dialogo **Cerca destinazione RFC** . Per altre informazioni su questi componenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](sap-bw-source.md) e [Destinazione SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Cerca destinazione RFC**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine e la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine o sulla destinazione SAP BW.  
  
3.  Nell' **Editor origine SAP BW** o nell' **Editor destinazione SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella pagina **Gestione connessione** , nella casella di gruppo **Destinazione RFC** fare clic su **Ricerca** per visualizzare la finestra di dialogo **Cerca destinazione RFC** .  
  
     Nell' **Editor origine SAP BW**, la casella di gruppo **Destinazione RFC** viene visualizzata solo se il valore di **Modalità di esecuzione** è **P - Attivazione catena processi** o **W - Attesa notifica**.  
  
## <a name="options"></a>Opzioni  
 **Destinazione**  
 Visualizzare il nome della destinazione RFC definito nel sistema SAP Netweaver BW.  
  
 **Host gateway**  
 Visualizzare il nome del server o l'indirizzo IP dell'host gateway. In genere, il nome o l'indirizzo IP è uguale a quello del server applicazioni SAP.  
  
 **Servizio gateway**  
 Visualizzare il nome del servizio gateway, nel formato `sapgwNN`, dove `NN` è il numero del sistema.  
  
 **ID programma**  
 Visualizzare l'ID programma associato alla destinazione RFC.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor destinazione SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
