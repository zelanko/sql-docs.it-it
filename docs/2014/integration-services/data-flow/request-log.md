---
title: Log richieste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 958a2990fe3bde49898451c9fefaee74b1b335f8
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52750213"
---
# <a name="request-log"></a>Log richieste
  Usare la finestra di dialogo **Log richieste** per visualizzare gli eventi registrati durante la richiesta fatta al sistema SAP Netweaver BW per i dati di esempio. Queste informazioni possono essere utili se è necessario risolvere i problemi relativi alla configurazione dell'origine SAP BW.  
  
 Per altre informazioni sul componente di origine SAP BW di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vedere [Origine SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 **Per aprire la finestra di dialogo Log richieste**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene l'origine SAP BW.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine SAP BW.  
  
3.  Nell' **Editor origine SAP BW**fare clic su **Gestione connessione** per aprire la pagina **Gestione connessione** dell'editor.  
  
4.  Dopo aver configurato l'origine SAP BW, fare clic su **Anteprima** per visualizzare gli eventi in anteprima nella finestra di dialogo **Log richieste** .  
  
    > [!NOTE]  
    >  Quando si fa clic su **Anteprima** , inoltre, viene aperta la finestra di dialogo **Anteprima** . Per altre informazioni su questa finestra di dialogo, vedere [Anteprima](preview.md).  
  
## <a name="options"></a>Opzioni  
 **Time**  
 Visualizza l'ora di registrazione dell'evento.  
  
 **Tipo**  
 Visualizza il tipo dell'evento registrato. Nella tabella seguente sono elencati i tipi di eventi possibili.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|S|Messaggio di operazione completata.|  
|E|Messaggio di errore|  
|W|Messaggio di avviso.|  
|I|Messaggio informativo.|  
|A|L'operazione è stata interrotta.|  
  
 **Message**  
 Visualizza il testo del messaggio associato all'evento registrato.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Guida (F1) di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
