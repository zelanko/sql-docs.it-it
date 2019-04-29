---
title: Origine SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 749afb64-3567-4dc9-8431-783d650c25db
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 169c35d89075646aa3f4964d0e9d6eda92bc13a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901069"
---
# <a name="sap-bw-source"></a>Origine SAP BW
  L'origine SAP BW è il componente di origine di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. Pertanto, l'origine SAP BW estrae i dati da un sistema SAP Netweaver BW versione 7 e li rende disponibili al flusso di dati in un pacchetto di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Questa origine include un output e un output degli errori.  
  
> [!IMPORTANT]  
>  La documentazione per Microsoft Connector 1.1 for SAP BW presuppone la conoscenza dell'ambiente SAP Netweaver BW. Per ulteriori informazioni su SAP Netweaver BW o per informazioni su come configurare oggetti e processi di SAP Netweaver BW, vedere la documentazione SAP.  
  
> [!IMPORTANT]  
>  L'estrazione di dati da SAP Netweaver BW richiede licenze SAP aggiuntive. Contattare SAP per verificare questi requisiti.  
  
 Per utilizzare l'origine SAP BW, effettuare le operazioni seguenti:  
  
-   [Preparare gli oggetti SAP Netweaver BW](#bkmk_Prepare_Objects)  
  
-   [Connettersi al sistema SAP Netweaver BW](#bkmk_Connect_Database)  
  
-   [Configurare l'origine SAP BW](#bkmk_Configure_Source)  
  
##  <a name="bkmk_Prepare_Objects"></a> Preparazione degli oggetti SAP Netweaver BW richiesti dall'origine  
 L'origine SAP BW richiede la presenza di determinati oggetti nel sistema SAP Netweaver BW per funzionare. Se questi oggetti non esistono ancora, è necessario eseguire questi passaggi per crearli e configurarli nel sistema SAP Netweaver BW.  
  
> [!NOTE]  
>  Per ulteriori dettagli sugli oggetti e sui passaggi di configurazione, vedere la documentazione di SAP Netweaver BW.  
  
1.  Accedere al sistema SAP Netweaver BW tramite la GUI SAP, immettere il codice di transazione SM59 e creare una destinazione RFC:  
  
    1.  In **Tipo di connessione**selezionare **TCP/IP**.  
  
    2.  In **Tipo di attivazione**selezionare **Programma server registrato**.  
  
    3.  In **Communication Type with Target System**(Tipo di comunicazione con sistema di destinazione) selezionare **Non-Unicode (Inactive MDMP Settings)**(Non Unicode (Impostazioni MDMP inattive)).  
  
    4.  Assegnare un ID programma appropriato.  
  
2.  Creare una destinazione di hub aperto:  
  
    1.  Passare alla workbench dell'amministratore (codice di transazione RSA1) e, nel riquadro sinistro, selezionare **Open Hub Destination**(Destinazione hub aperto).  
  
    2.  Nel riquadro centrale fare clic con il pulsante destro del mouse su un'InfoArea, quindi selezionare **"Create Open Hub Destination"**(Crea destinazione di hub aperto).  
  
    3.  Per **Tipo destinazione**selezionare **"Strumento di terze parti"**, quindi immettere la destinazione RFC creata in precedenza.  
  
    4.  Salvare e attivare la nuova destinazione di hub aperto.  
  
3.  Creare un processo di trasferimento dati (DTP):  
  
    1.  Nel riquadro centrale dell'InfoArea, fare clic con il pulsante destro del mouse sulla destinazione creata in precedenza, quindi selezionare **"Create data transfer process"**(Crea processo di trasferimento dati).  
  
    2.  Configurare, salvare e attivare il DTP.  
  
    3.  Nel menu fare clic su **Vai a**, quindi fare clic su **Impostazioni per gestioni batch**.  
  
    4.  Aggiornare **Numero di processi** su 1 per l'elaborazione seriale.  
  
4.  Creare una catena di processi:  
  
    1.  Quando si configura la catena di processi, selezionare **Avvia utilizzando catena di metadati o API** per **Opzioni di pianificazione** di **Processo di avvio**, quindi aggiungere il DTP creato in precedenza come nodo successivo.  
  
    2.  Salvare e attivare la catena di processi.  
  
     L'origine SAP BW può chiamare la catena di processi per attivare il processo di trasferimento dati.  
  
##  <a name="bkmk_Connect_Database"></a> Connessione al sistema SAP Netweaver BW  
 Per connettersi al sistema SAP Netweaver BW versione 7, l'origine SAP BW utilizza la gestione connessione SAP BW che fa parte di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW. La gestione connessione SAP BW è l'unica gestione connessione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che può essere utilizzata dall'origine SAP BW.  
  
 Per ulteriori informazioni sulla gestione connessione SAP BW, vedere [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md).  
  
##  <a name="bkmk_Configure_Source"></a> Configurazione dell'origine SAP BW  
 Per configurare l'origine SAP BW, procedere nei modi seguenti:  
  
-   Cercare e selezionare la destinazione OHS (Open Hub Service) da utilizzare per estrarre i dati.  
  
-   Selezionare uno dei metodi seguenti per estrarre i dati:  
  
    -   Attivare una catena di processi. In questo caso, il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] avvia il processo di estrazione.  
  
    -   Attendere la notifica dal sistema SAP Netweaver BW per iniziare un'estrazione. In questo caso, il sistema SAP Netweaver BW avvia il processo di estrazione.  
  
    -   Recuperare i dati associati a un ID richiesta specifico. In questo caso, il sistema SAP Netweaver BW ha già estratto i dati in una tabella interna e il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] legge solo i dati.  
  
-   A seconda del metodo selezionato per estrarre dati, fornire le informazioni aggiuntive seguenti:  
  
    -   Per l'opzione **P - Attivazione catena processi** , fornire il nome host del gateway, il nome del servizio gateway, l'ID programma per la destinazione RFC e il nome della catena di processi.  
  
    -   Per l'opzione **W - Attesa notifica** , fornire il nome host del gateway, il nome del server gateway e l'ID programma per la destinazione RFC. È inoltre possibile specificare il timeout (in secondi). Il timeout è il periodo di tempo massimo di attesa della notifica da parte dell'origine.  
  
    -   Per l'opzione **E - Solo estrazione** , fornire l'ID richiesta.  
  
-   Specificare le regole per la conversione di stringhe. Convertire, ad esempio, tutte le stringhe a seconda che il sistema SAP Netweaver BW sia Unicode oppure no; in alternativa, convertire tutte le stringhe in `varchar` o `nvarchar`.  
  
-   Utilizzare le opzioni selezionate per visualizzare in anteprima i dati da estrarre.  
  
 È inoltre possibile abilitare la registrazione delle chiamate di funzioni RFC da parte dell'origine. Tale registrazione è separata dalla registrazione facoltativa che è possibile abilitare nei pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Abilitare la registrazione delle chiamate di funzioni RFC quando si configura la gestione connessione SAP BW che verrà utilizzata dall'origine. Per ulteriori informazioni sulla configurazione della gestione connessione SAP BW, vedere [SAP BW Connection Manager](../connection-manager/sap-bw-connection-manager.md).  
  
 Se non si conoscono tutti i valori richiesti per configurare l'origine, può essere necessario consultare l'amministratore SAP.  
  
 Per una procedura dettagliata che illustra come configurare e utilizzare la gestione connessione, l'origine e la destinazione SAP BW, vedere il white paper [Utilizzo dei servizi di integrazione SQL Server 2008 con SAP BI 7.0](https://go.microsoft.com/fwlink/?LinkID=137090). Nel white paper viene anche indicato come configurare gli oggetti necessari in SAP BW.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>Utilizzo di Progettazione SSIS per configurare l'origine  
 Per ulteriori informazioni sulle proprietà dell'origine SAP BW che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor origine SAP BW &#40;pagina Gestione connessione&#41;](sap-bw-source-editor-connection-manager-page.md)  
  
-   [Editor origine SAP BW &#40;pagina Colonne&#41;](sap-bw-source-editor-columns-page.md)  
  
-   [Editor origine SAP BW &#40;pagina Output degli errori&#41;](sap-bw-source-editor-error-output-page.md)  
  
-   [Editor origine SAP BW &#40;pagina Avanzate&#41;](sap-bw-source-editor-advanced-page.md)  
  
 Quando si configura l'origine SAP BW, è inoltre possibile utilizzare varie finestre di dialogo per cercare gli oggetti SAP Netweaver BW o visualizzare in anteprima i dati di origine. Per ulteriori informazioni su queste finestre di dialogo, fare clic su uno degli argomenti seguenti:  
  
-   [Cerca destinazione RFC](look-up-rfc-destination.md)  
  
-   [Cerca ProcessChain](look-up-process-chain.md)  
  
-   [Log richieste](request-log.md)  
  
-   [Anteprima](preview.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Componenti di Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-components.md)  
  
  
