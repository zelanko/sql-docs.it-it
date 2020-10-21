---
description: Attività Servizio Web
title: Attività Servizio Web | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9ff964cda9e4e9687a61d50db7c7d53c6e9e24ab
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196005"
---
# <a name="web-service-task"></a>Attività Servizio Web

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Servizio Web esegue un metodo di servizio Web. È possibile utilizzare l'attività Servizio Web per gli scopi seguenti:  
  
-   Scrivere in una variabile i valori restituiti da un metodo di servizio Web. È ad esempio possibile ottenere la temperatura massima del giorno da un metodo di servizio Web e quindi utilizzare tale valore per aggiornare una variabile utilizzata in un'espressione che imposta il valore di una colonna.  
  
-   Scrivere in un file i valori restituiti da un metodo di servizio Web. È ad esempio possibile scrivere in un file un elenco di potenziali clienti e utilizzare tale file come origine dei dati in un pacchetto che pulisce i dati prima che vengano scritti in un database.  
  
## <a name="wsdl-file"></a>File WSDL  
 Per connettersi al servizio Web l'attività Servizio Web utilizza una gestione connessione HTTP, configurata separatamente, a cui viene fatto riferimento dall'attività Servizio Web. La gestione connessione HTTP specifica le impostazioni proxy del server, quali l'URL del server, le credenziali per l'accesso al server dei servizi Web e la durata del timeout. Per altre informazioni, vedere [Gestione connessione HTTP](../../integration-services/connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 La gestione connessione HTTP può puntare a un sito Web o a un file WSDL (Web Service Description Language). L'URL di una gestione connessione HTTP che punta a un file WSDL include il parametro `?WSDL` , ad esempio `https://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 Affinché sia possibile configurare l'attività Servizio Web tramite la finestra di dialogo **Editor attività Servizio Web** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , il file WSDL deve essere disponibile localmente.  
  
-   Se la gestione connessione HTTP punta a un sito Web, il file WSDL dovrà essere copiato manualmente in un computer locale.  
  
-   Se la gestione connessione HTTP punta a un file WSDL, l'attività Servizio Web potrà scaricare il file dal sito Web a un file locale.  
  
 Nel file WSDL sono elencati i metodi offerti dal servizio Web, i parametri di input richiesti dai metodi, le risposte restituite dai metodi e la modalità con cui comunicare con il servizio Web.  
  
 Se il metodo utilizza parametri di input, l'attività Servizio Web richiederà i valori dei parametri. Un metodo che determina la lunghezza consigliata degli sci da acquistare in base alla statura del cliente, ad esempio, richiede l'immissione della statura in un parametro di input. I valori dei parametri possono essere specificati mediante stringhe definite all'interno dell'attività oppure tramite variabili definite nell'ambito dell'attività o di un contenitore padre. Il vantaggio dell'utilizzo di variabili consiste nella possibilità di aggiornare dinamicamente i valori dei parametri mediante script o configurazioni di pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Configurazioni di pacchetto](../packages/legacy-package-deployment-ssis.md).  
  
 Molti metodi di servizi Web non utilizzano parametri di input. Un metodo di servizio Web che ottiene i nomi dei presidenti nati nel mese corrente, ad esempio, non richiede parametri di input, perché è in grado di determinare il mese corrente localmente.  
  
 I risultati del metodo di servizio Web possono essere scritti in una variabile o in un file. Per specificare il file o il nome della variabile in cui scrivere i risultati, è necessario utilizzare una gestione connessione file. Per altre informazioni, vedere [Gestione connessione File](../../integration-services/connection-manager/file-connection-manager.md) e [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Messaggi di registrazione personalizzati disponibili nell'attività Servizio Web  
 Nella tabella seguente sono elencate le voci di log personalizzate che è possibile attivare per l'attività Servizio Web. Per altre informazioni, vedere [registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|**WSTaskBegin**|Indica che l'attività ha iniziato ad accedere a un servizio Web.|  
|**WSTaskEnd**|Indica che l'attività ha completato un metodo per il servizio Web.|  
|**WSTaskInfo**|Offre informazioni descrittive sull'attività.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configurazione dell'attività Servizio Web  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Pagina Espressioni](../../integration-services/expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configurazione dell'attività Servizio Web a livello di codice  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>Editor attività Servizio Web (pagina Generale)
  Usare la pagina **Generale** della finestra di dialogo **Editor attività Servizio Web** per specificare una gestione connessione HTTP e il percorso del file WSDL (Web Services Description Language) usato dall'attività Servizio Web, descrivere l'attività Servizio Web e scaricare il file WSDL.  
  
### <a name="options"></a>Opzioni  
 **HTTPConnection**  
 Selezionare una gestione connessione nell'elenco oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
> [!IMPORTANT]  
>  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 **Argomenti correlati:**  [Gestione connessione HTTP](../../integration-services/connection-manager/http-connection-manager.md), [Editor gestione connessione HTTP &#40;pagina Server&#41;](../connection-manager/http-connection-manager.md)  
  
 **WSDLFile**  
 Digitare il percorso completo di un file WSDL presente in locale nel computer oppure fare clic sul pulsante sfoglia **(...)** e individuare il file.  
  
 Sezionare il file WSDL presente nel computer, se è già stato scaricato manualmente. Se invece il file WSDL non è stato ancora scaricato, attenersi alla seguente procedura:  
  
-   Creare un file vuoto con l'estensione di file "wsdl".  
  
-   Selezionare questo file vuoto per l'opzione **WSDLFile** .  
  
-   Impostare il valore di **OverwriteWSDLFile** su **True** per consentire al file vuoto di essere sovrascritto con il file WSDL effettivo.  
  
-   Fare clic su **Scarica WSDL** per scaricare il file WSDL effettivo e sovrascrivere il file vuoto.  
  
    > [!NOTE]  
    >  L'opzione **Scarica WSDL** non è abilitato fino a quando non si fornisce il nome di un file locale esistente nella casella **WSDLFile** .  
  
 **OverwriteWSDLFile**  
 Consente di specificare se il file WSDL per l'attività Servizio Web può essere sovrascritto.  
  
 Se si intende scaricare il file WSDL tramite il pulsante **Scarica WSDL** , impostare questo valore su **True**.  
  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Servizio Web. Tale nome viene utilizzato come etichetta nell'icona dell'attività.  
  
> [!NOTE]  
>  I nomi delle attività devono essere univoci all'interno di un pacchetto.  
  
 **Descrizione**  
 Consente di digitare una descrizione dell'attività Servizio Web.  
  
 **Scarica WSDL**  
 Consente di scaricare il file WSDL.  
  
 Questo pulsante non è attivato fino a quando non si fornisce il nome di un file locale esistente nella casella **WSDLFile** .  
  
## <a name="web-service-task-editor-input-page"></a>Editor attività Servizio Web (pagina Input)
  Utilizzare la pagina **Input** della finestra di dialogo **Editor attività Servizio Web** per specificare il servizio Web, il metodo Web e i valori da fornire come input al metodo Web. I valori possono essere immessi digitando direttamente le stringhe nella colonna Valore o selezionando le variabili nella colonna Valore.  
  
### <a name="options"></a>Opzioni  
 **Service**  
 Consente di selezionare un servizio Web nell'elenco da utilizzare per l'esecuzione del metodo Web.  
  
 **Metodo**  
 Consente di selezionare nell'elenco il metodo Web che l'attività deve eseguire.  
  
 **WebMethodDocumentation**  
 Digitare una descrizione del metodo Web oppure fare clic sul pulsante sfoglia **(...)** e quindi digitare la descrizione nella finestra di dialogo **Documentazione metodo Web**.  
  
 **Nome**  
 Elenca i nomi degli input per il metodo Web.  
  
 **Tipo**  
 Elenca il tipo di dati degli input.  
  
> [!NOTE]  
>  L'attività Servizio Web supporta unicamente i parametri dei tipi di dati seguenti: tipi primitivi come ad esempio valori integer e stringhe, matrici e sequenze di tipi primitivi ed enumerazioni.  
  
 **Variabile**  
 Selezionare le caselle di controllo per utilizzare le variabili per l'invio degli input.  
  
 **Valore**  
 Se le caselle di controllo Variabile sono selezionate, selezionare le variabili nell'elenco per l'invio degli input. In caso contrario, digitare i valori da utilizzare negli input.  
  
## <a name="web-service-task-editor-output-page"></a>Editor attività Servizio Web (pagina Output)
  Usare la pagina **Output** della finestra di dialogo **Editor attività Servizio Web** per specificare la posizione in cui archiviare il risultato restituito dal metodo Web.  
  
### <a name="static-options"></a>Opzioni statiche  
 **OutputType**  
 Consente di selezionare il tipo di archiviazione da utilizzare per l'archiviazione dei risultati. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**File Connection**|Consente di archiviare i risultati in un file. La selezione di questo valore determina la visualizzazione dell'opzione dinamica **File**.|  
|**Variabile**|Consente di archiviare i risultati in una variabile. La selezione di questo valore determina la visualizzazione dell'opzione dinamica **Variabile**.|  
  
### <a name="outputtype-dynamic-options"></a>Opzioni dinamiche di OutputType  
  
#### <a name="outputtype--file-connection"></a>OutputType = Connessione file  
 **File**  
 Selezionare una gestione connessione file nell'elenco oppure fare clic su \<**New Connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md), [Editor gestione connessione file](../connection-manager/file-connection-manager.md)  
  
#### <a name="outputtype--variable"></a>OutputType = Variabile  
 **Variabile**  
 Selezionare una variabile nell'elenco oppure fare clic su \<**New Variable...**> per crearne una nuova.  
  
 **Argomenti correlati:**  [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Aggiungere una variabile](../integration-services-ssis-variables.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Video [Procedura: Chiamata a un servizio Web tramite l'attività Servizio Web (video di SQL Server)](/previous-versions/dn912438(v=msdn.10)) nel sito technet.microsoft.com.