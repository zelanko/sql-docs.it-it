---
title: Editor destinazione SAP BW (pagina Avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5396a6a94e1d5c4bfde39153081f3c4137a2c922
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62901034"
---
# <a name="sap-bw-destination-editor-advanced-page"></a>Editor destinazione SAP BW (pagina Avanzate)
  Usare la pagina **Avanzate** dell' **Editor destinazione SAP BW** per definire le impostazioni avanzate quali dimensioni del pacchetto e informazioni sul timeout.  
  
 Per altre informazioni sulla destinazione SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Destinazione SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la pagina Avanzate**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene la destinazione SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sulla destinazione SAP BW.  
  
3.  Nell' **Editor destinazione SAP BW**fare clic su **Avanzate** per aprire la pagina **Avanzate** dell'editor.  
  
## <a name="options"></a>Opzioni  
  
> [!NOTE]  
>  Se non si conoscono tutti i valori richiesti per configurare la destinazione, può essere necessario consultare l'amministratore SAP.  
  
 **Dimensioni pacchetto**  
 Specificare il numero di righe di dati che verranno trasferite contemporaneamente. Il valore ottimale per questo parametro dipende dal sistema SAP Netweaver BW e dall'ulteriore elaborazione dei dati che potrebbe verificarsi. In genere, i valori compresi tra 2000 e 20000 offrono prestazioni ottimali.  
  
 **Attivazione catena di processi**  
 (Facoltativo) Specificare il nome di una catena di processi da attivare dopo il completamento del caricamento dei dati.  
  
 **Timeout attesa InfoPackage**  
 Specificare il numero massimo di secondi di attesa del completamento dell'InfoPackage da parte della destinazione.  
  
 **Attendi completamento trasferimento dati**  
 Specificare se la destinazione deve attendere il completamento del caricamento dei dati da parte del sistema SAP Netweaver BW.  
  
 **Non avviare InfoPackage - solo attesa**  
 Specificare che la destinazione non attiva un InfoPackage, ma attende semplicemente la notifica dell'avvio del caricamento dei dati da parte del sistema SAP Netweaver BW.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor destinazione SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Editor destinazione SAP BW &#40;pagina Mapping&#41;](sap-bw-destination-editor-mappings-page.md)   
 [Editor destinazione SAP BW &#40;pagina Output degli errori&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
