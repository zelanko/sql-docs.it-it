---
description: Cerca ProcessChain
title: Cerca ProcessChain | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 28d354fce02498905c61df6b61a35a774d804eec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495828"
---
# <a name="look-up-process-chain"></a>Cerca ProcessChain

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare la finestra di dialogo **Cerca ProcessChain** per cercare una catena di processi definita nel sistema SAP Netweaver BW. Quando viene visualizzato l'elenco delle catene di processi disponibili, selezionare la catena desiderata e le opzioni associate verranno compilate con i valori richiesti dall'origine.  
  
 L'origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW utilizza la finestra di dialogo **Cerca ProcessChain** . Per ulteriori informazioni sull'origine SAP BW, vedere [SAP BW Source](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 **Per aprire la finestra di dialogo Cerca ProcessChain**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Nella casella di gruppo **Catena di processi** fare clic su **Ricerca** per visualizzare la finestra di dialogo **Cerca ProcessChain** .  
  
     La casella di gruppo **Catena di processi** viene visualizzata solo se il valore di **Modalità di esecuzione** è **P - Attivazione catena di processi**.  
  
## <a name="lookup-options"></a>Opzioni di ricerca  
 Nei campi di ricerca è possibile filtrare i risultati tramite il carattere jolly asterisco (*) oppure utilizzando una stringa parziale in combinazione con il carattere jolly asterisco. Tuttavia, se si lascia un campo di ricerca vuoto, l'operazione di ricerca restituirà solo stringhe vuote in tale campo.  
  
 **Catena di processi**  
 Immettere il nome della catena di processi da cercare oppure un nome parziale con il carattere jolly asterisco (*). In alternativa, utilizzare il carattere jolly asterisco da solo per includere tutte le catene di processi.  
  
 **Cerca**  
 Cercare le catene di processi corrispondenti definiti nel sistema SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Risultati di ricerca  
 Dopo avere fatto clic sul pulsante Ricerca, viene visualizzato un elenco delle catene di processi nel sistema SAP Netweaver BW in una tabella con le intestazioni di colonna seguenti:  
  
 **Catena di processi**  
 Visualizza il nome della catena di processi definita nel sistema SAP Netweaver BW.  
  
 **Descrizione**  
 Visualizza la descrizione della catena di processi.  
  
 Quando viene visualizzato l'elenco delle catene di processi disponibili, selezionare la catena desiderata e le opzioni associate verranno compilate con i valori richiesti dall'origine.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Guida sensibile al contesto di Microsoft Connector per SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
