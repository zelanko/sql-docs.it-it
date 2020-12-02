---
description: Destinazione SAP BW
title: Destinazione SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a612ed91-b89b-4173-a0b1-0bce381e1e28
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d46d3598bb309029319c1b74b467983e681b96ac
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "92197055"
---
# <a name="sap-bw-destination"></a>Destinazione SAP BW

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La destinazione SAP BW è il componente di destinazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Pertanto, la destinazione SAP BW carica i dati dal flusso di dati in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in un sistema SAP Netweaver BW versione 7.  
  
 Questa destinazione include un input e un output degli errori.  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
 Per utilizzare la destinazione SAP BW, effettuare le operazioni seguenti:  
  
-   [Preparare gli oggetti SAP Netweaver BW](#bkmk_Prepare_Objects)  
  
-   [Connettersi al sistema SAP Netweaver BW](#bkmk_Connect_Database)  
  
-   [Configurare la destinazione SAP BW](#bkmk_Configure_Destination)  
  
##  <a name="preparing-the-sap-netweaver-bw-objects-that-the-destination-requires"></a><a name="bkmk_Prepare_Objects"></a> Preparazione degli oggetti SAP Netweaver BW richiesti dalla destinazione  
 La destinazione SAP BW richiede la presenza di determinati oggetti nel sistema SAP Netweaver BW per funzionare. Se questi oggetti non esistono ancora, è necessario eseguire questi passaggi per crearli e configurarli nel sistema SAP Netweaver BW.  
  
> [!NOTE]  
>  Per ulteriori dettagli sugli oggetti e sui passaggi di configurazione, vedere la documentazione di SAP Netweaver BW.  
  
1.  Creare un nuovo sistema di origine:  
  
    1.  Selezionare il tipo **"Third Party/Staging BAPIs"**(BAPI gestione temporanea/terze parti).  
  
    2.  In **Communication Type with Target System**(Tipo di comunicazione con sistema di destinazione) selezionare **Non-Unicode (Inactive MDMP Settings)**(Non Unicode (Impostazioni MDMP inattive)).  
  
    3.  Assegnare un ID programma appropriato.  
  
2.  Assegnare il sistema di origine a un'InfoSource.  
  
3.  Creare un InfoPackage.  
  
     L'InfoPackage è l'oggetto più importante richiesto dalla destinazione SAP BW.  
  
 È inoltre possibile creare altri InfoObject, Infocube, InfoSource e InfoPackage necessari per supportare il caricamento di dati nel sistema SAP Netweaver BW.  
  
##  <a name="connecting-to-the-sap-netweaver-bw-system"></a><a name="bkmk_Connect_Database"></a> Connessione al sistema SAP Netweaver BW  
 Per connettersi al sistema SAP Netweaver BW versione 7, la destinazione SAP BW utilizza la gestione connessione SAP BW che fa parte di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. La gestione connessione SAP BW è l'unica gestione connessione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che può essere utilizzata dalla destinazione SAP BW.  
  
 Per ulteriori informazioni sulla gestione connessione SAP BW, vedere [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="configuring-the-sap-bw-destination"></a><a name="bkmk_Configure_Destination"></a> Configurazione della destinazione SAP BW  
 È possibile configurare la destinazione SAP BW nei modi seguenti:  
  
-   Cercare e selezionare l'InfoPackage da utilizzare per caricare i dati.  
  
-   Eseguire il mapping di ogni colonna nel flusso di dati all'InfoObject appropriato nell'InfoPackage.  
  
-   Specificare il numero di righe di dati che verranno trasferite contemporaneamente mediante la configurazione della proprietà **PackageSize** .  
  
-   Scegliere di attendere il completamento del caricamento dei dati da parte del sistema SAP Netweaver BW.  
  
-   Scegliere di non attivare l'InfoPackage, ma di attendere la notifica dell'avvio del caricamento dei dati da parte del sistema SAP Netweaver BW.  
  
-   Facoltativamente, attivare un'altra catena di processi al completamento del caricamento dei dati.  
  
-   Facoltativamente, creare gli oggetti SAP Netweaver BW richiesti dalla destinazione. Ciò include la creazione di InfoObject, InfoCube, InfoSource e InfoPackage.  
  
-   Verificare il caricamento dei dati con le opzioni selezionate.  
  
 È inoltre possibile abilitare la registrazione delle chiamate di funzioni RFC da parte della destinazione. Tale registrazione è separata dalla registrazione facoltativa che è possibile abilitare nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Abilitare la registrazione delle chiamate di funzioni RFC quando si configura la gestione connessione SAP BW che verrà utilizzata dalla destinazione. Per ulteriori informazioni sulla configurazione della gestione connessione SAP BW, vedere [SAP BW Connection Manager](../../integration-services/connection-manager/sap-bw-connection-manager.md).  
  
 Se non si conoscono tutti i valori richiesti per configurare la destinazione, può essere necessario consultare l'amministratore SAP.  
  
 Per una procedura dettagliata che illustra come configurare e utilizzare la gestione connessione, l'origine e la destinazione SAP BW, vedere il white paper [Utilizzo dei servizi di integrazione SQL Server 2008 con SAP BI 7.0](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100)). Nel white paper viene anche indicato come configurare gli oggetti necessari in SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-destination"></a>Utilizzo di Progettazione SSIS per configurare la destinazione  
 Per ulteriori informazioni sulle proprietà della destinazione SAP BW che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor destinazione SAP BW &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)  
  
-   [Editor destinazione SAP BW &#40;pagina Mapping&#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)  
  
-   [Editor destinazione SAP BW &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/sap-bw-destination-editor-error-output-page.md)  
  
-   [Editor destinazione SAP BW &#40;pagina Avanzate&#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)  
  
 Quando si configura la destinazione SAP BW, è inoltre possibile utilizzare varie finestre di dialogo per cercare o creare gli oggetti SAP Netweaver BW. Per ulteriori informazioni su queste finestre di dialogo, fare clic su uno degli argomenti seguenti:  
  
-   [Cerca InfoPackage](../../integration-services/data-flow/look-up-infopackage.md)  
  
-   [Crea nuovo InfoObject](../../integration-services/data-flow/create-new-infoobject.md)  
  
-   [Crea InfoCube per dati transazione](../../integration-services/data-flow/create-infocube-for-transaction-data.md)  
  
-   [Cerca InfoObject](../../integration-services/data-flow/look-up-infoobject.md)  
  
-   [Crea InfoSource](../../integration-services/data-flow/create-infosource.md)  
  
-   [Crea InfoSource per dati transazione](../../integration-services/data-flow/create-infosource-for-transaction-data.md)  
  
-   [Crea InfoSource per dati master](../../integration-services/data-flow/create-infosource-for-master-data.md)  
  
-   [Crea InfoPackage](../../integration-services/data-flow/create-infopackage.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Componenti di Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
