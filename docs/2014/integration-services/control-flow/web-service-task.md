---
title: Attività Servizio Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ee28bbfa3cea482f934b3491f51e0caf601f5465
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363163"
---
# <a name="web-service-task"></a>Attività Servizio Web
  L'attività Servizio Web esegue un metodo di servizio Web. È possibile utilizzare l'attività Servizio Web per gli scopi seguenti:  
  
-   Scrivere in una variabile i valori restituiti da un metodo di servizio Web. È ad esempio possibile ottenere la temperatura massima del giorno da un metodo di servizio Web e quindi utilizzare tale valore per aggiornare una variabile utilizzata in un'espressione che imposta il valore di una colonna.  
  
-   Scrivere in un file i valori restituiti da un metodo di servizio Web. È ad esempio possibile scrivere in un file un elenco di potenziali clienti e utilizzare tale file come origine dei dati in un pacchetto che pulisce i dati prima che vengano scritti in un database.  
  
## <a name="wsdl-file"></a>File WSDL  
 Per connettersi al servizio Web l'attività Servizio Web utilizza una gestione connessione HTTP, configurata separatamente, a cui viene fatto riferimento dall'attività Servizio Web. La gestione connessione HTTP specifica le impostazioni proxy del server, quali l'URL del server, le credenziali per l'accesso al server dei servizi Web e la durata del timeout. Per altre informazioni, vedere [Gestione connessione HTTP](../connection-manager/http-connection-manager.md).  
  
> [!IMPORTANT]  
>  La gestione connessione HTTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 La gestione connessione HTTP può puntare a un sito Web o a un file WSDL (Web Service Description Language). L'URL di una gestione connessione HTTP che punta a un file WSDL include il parametro `?WSDL` , ad esempio `http://MyServer/MyWebService/MyPage.asmx?WSDL`.  
  
 Affinché sia possibile configurare l'attività Servizio Web tramite la finestra di dialogo **Editor attività Servizio Web** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , il file WSDL deve essere disponibile localmente.  
  
-   Se la gestione connessione HTTP punta a un sito Web, il file WSDL dovrà essere copiato manualmente in un computer locale.  
  
-   Se la gestione connessione HTTP punta a un file WSDL, l'attività Servizio Web potrà scaricare il file dal sito Web a un file locale.  
  
 Nel file WSDL sono elencati i metodi offerti dal servizio Web, i parametri di input richiesti dai metodi, le risposte restituite dai metodi e la modalità con cui comunicare con il servizio Web.  
  
 Se il metodo utilizza parametri di input, l'attività Servizio Web richiederà i valori dei parametri. Un metodo che determina la lunghezza consigliata degli sci da acquistare in base alla statura del cliente, ad esempio, richiede l'immissione della statura in un parametro di input. I valori dei parametri possono essere specificati mediante stringhe definite all'interno dell'attività oppure tramite variabili definite nell'ambito dell'attività o di un contenitore padre. Il vantaggio dell'utilizzo di variabili consiste nella possibilità di aggiornare dinamicamente i valori dei parametri mediante script o configurazioni di pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Configurazioni di pacchetto](../package-configurations.md).  
  
 Molti metodi di servizi Web non utilizzano parametri di input. Un metodo di servizio Web che ottiene i nomi dei presidenti nati nel mese corrente, ad esempio, non richiede parametri di input, perché è in grado di determinare il mese corrente localmente.  
  
 I risultati del metodo di servizio Web possono essere scritti in una variabile o in un file. Per specificare il file o il nome della variabile in cui scrivere i risultati, è necessario utilizzare una gestione connessione file. Per altre informazioni, vedere [Gestione connessione File](../connection-manager/file-connection-manager.md) e [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Messaggi di registrazione personalizzati disponibili nell'attività Servizio Web  
 Nella tabella seguente sono elencate le voci di log personalizzate che è possibile attivare per l'attività Servizio Web. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`WSTaskBegin`|Indica che l'attività ha iniziato ad accedere a un servizio Web.|  
|`WSTaskEnd`|Indica che l'attività ha completato un metodo per il servizio Web.|  
|`WSTaskInfo`|Offre informazioni descrittive sull'attività.|  
  
## <a name="configuration-of-the-web-service-task"></a>Configurazione dell'attività Servizio Web  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Servizio Web &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Servizio Web &#40;pagina Input&#41;](../web-service-task-editor-input-page.md)  
  
-   [Editor attività Servizio Web &#40;pagina Output&#41;](../web-service-task-editor-output-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostare le proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>Configurazione dell'attività Servizio Web a livello di codice  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>Contenuto correlato  
 Video, [come: Chiamare un servizio Web usando l'attività servizio Web (Video di SQL Server)](https://go.microsoft.com/fwlink/?LinkId=259642), sul sito Web technet.microsoft.com.  
  
 Risposta curata relativa all' [uso dei servizi Web in SSIS tramite script](https://go.microsoft.com/fwlink/?LinkId=321996)su curatedviews.cloudapp.net.  
  
  
