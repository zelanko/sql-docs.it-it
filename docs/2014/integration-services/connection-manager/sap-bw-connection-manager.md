---
title: Gestione connessione SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b3ee629cd7701d8b06351e8932daac57637b195e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833674"
---
# <a name="sap-bw-connection-manager"></a>Gestione connessione SAP BW
  La gestione connessione SAP BW è il componente per la gestione delle connessioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. La gestione connessione SAP BW offre la connettività a un sistema SAP Netweaver BW versione 7 di cui hanno bisogno i componenti di origine e destinazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. L'origine e la destinazione SAP BW che fanno parte del pacchetto di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW sono gli unici componenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che usano la gestione connessione SAP BW.  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 Quando si aggiunge una gestione connessione SAP BW a un pacchetto, la proprietà `ConnectionManagerType` della gestione connessione è impostata su `SAPBI`.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>Configurazione della gestione connessione SAP BW  
 Per configurare la gestione connessione SAP BW, procedere nel modo seguente:  
  
-   Specificare client, nome utente, password e lingua della connessione.  
  
-   Scegliere se stabilire la connessione a un server applicazioni singolo o a un gruppo di server con carico bilanciato.  
  
-   Specificare il numero di sistema e host per un server applicazioni oppure specificare server messaggi, gruppo e SID per un gruppo di server con carico bilanciato.  
  
-   Abilitare la registrazione personalizzata delle chiamate di funzione RFC per i componenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Tale registrazione è separata dalla registrazione facoltativa che è possibile abilitare nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per abilitare la registrazione delle chiamate di funzione RFC, specificare una directory in cui archiviare i file di log creati prima e dopo ogni chiamata di funzione RFC. Questa funzionalità di registrazione crea molti file di log in formato XML. Poiché questi file di log contengono anche tutte le righe di dati trasferiti, è possibile che occupino una grande quantità di spazio su disco. Se non si seleziona una directory di log, la registrazione non è abilitata.  
  
    > [!IMPORTANT]  
    >  Se i dati trasferiti contengono informazioni riservate, anche i file di log conterranno tali informazioni riservate.  
  
-   Utilizzare i valori immessi per verificare la connessione.  
  
 Se non si conoscono tutti i valori richiesti per configurare la gestione connessione, può essere necessario consultare l'amministratore SAP.  
  
 Per una procedura dettagliata che illustra come configurare e utilizzare la gestione connessione, l'origine e la destinazione SAP BW, vedere il white paper [Utilizzo dei servizi di integrazione SQL Server 2008 con SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). Nel white paper viene anche indicato come configurare gli oggetti necessari in SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Utilizzo di Progettazione SSIS per configurare l'origine  
 Per ulteriori informazioni sulle proprietà della gestione connessione SAP BW che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Editor gestione connessione SAP BW](../sap-bw-connection-manager-editor.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Componenti di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-components.md)  
  
  
