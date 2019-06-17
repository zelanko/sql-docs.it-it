---
title: Using the SOAP API in a Windows Application (Uso dell'API SOAP in un'applicazione Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- rendered reports [Reporting Services]
- Windows applications [Reporting Services]
- Windows Forms [Reporting Services]
- SOAP [Reporting Services], Windows applications
ms.assetid: e4804792-20cd-4df2-9257-fb958ff447b4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bb34dc31d65c9b0814a348232d0e2405d7676fda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63218339"
---
# <a name="using-the-soap-api-in-a-windows-application"></a>Utilizzo dell'API SOAP in un'applicazione Windows
  È possibile accedere alle funzionalità complete del server di report tramite l'API SOAP di Reporting Services. L'API SOAP è un servizio Web e, in quanto tale, è possibile accedervi in modo semplice per fornire caratteristiche di creazione di report aziendali alle applicazioni aziendali personalizzate. È possibile accedere al servizio Web in un'applicazione Windows semplicemente scrivendo codice che consenta di effettuare chiamate al servizio. Usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], è possibile generare una classe proxy che espone le proprietà e i metodi del servizio Web e consente di usare un'infrastruttura familiare e gli strumenti per compilare applicazioni aziendali basate sulla tecnologia [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="integrating-report-management-functionality-using-windows-forms"></a>Integrazione delle funzionalità di Gestione report tramite Windows Form  
 A differenza dell'accesso con URL, l'API SOAP espone il set completo di funzioni di gestione disponibili tramite il server di report. Questo significa che tutte le funzionalità amministrative di Gestione report sono disponibili per gli sviluppatori tramite SOAP. È pertanto possibile sviluppare uno strumento completo di gestione e amministrazione tramite Windows Form. Nell'applicazione Windows è ad esempio possibile consentire agli utenti di recuperare il contenuto dello spazio dei nomi del server di report. A tale scopo, è possibile utilizzare il metodo <xref:ReportService2010.ReportingService2010.ListChildren%2A> del servizio Web per elencare tutti gli elementi del database del server di report, quindi utilizzare un controllo Listview, Treeview o Combobox per consentire agli utenti di visualizzare tali elementi. Il codice del servizio Web seguente potrebbe essere utilizzato per recuperare l'elenco corrente di report disponibili nella cartella My Reports di un utente quando un utente fa clic su un pulsante in un modulo:  
  
```vb  
' Button click event that retrieves a list of reports from  
' the My Reports folder and displays them in a combo box  
Private Sub listReportsButton_Click(sender As Object, e As System.EventArgs)  
   ' Create a new Web service object and set credentials  
   ' to Windows Authentication  
   Dim rs As New ReportingService2010()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return the list of items in My Reports  
   Dim items As CatalogItem() = rs.ListChildren("/Adventureworks 2008 Sample Reports", False)  
  
   Dim ci As CatalogItem  
   For Each ci In  items  
      ' If the item is a report, add it to   
      ' a combo box  
      If ci.TypeName = "Report" Then  
         catalogComboBox.Items.Add(ci.Name)  
      End If  
   Next ci  
End Sub 'listReportsButton_Click  
```  
  
```csharp  
// Button click event that retrieves a list of reports from  
// the My Reports folder and displays them in a combo box  
private void listReportsButton_Click(object sender, System.EventArgs e)  
{  
   // Create a new Web service object and set credentials  
   // to Windows Authentication  
   ReportingService2010 rs = new ReportingService2010();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return the list of items in My Reports  
   CatalogItem[] items = rs.ListChildren("/Adventureworks 2008 Sample Reports", false);  
  
   foreach (CatalogItem ci in items)  
   {  
      // If the item is a report, add it to   
      // a combo box  
      if (ci.TypeName == "Report")  
         catalogComboBox.Items.Add(ci.Name);  
   }  
}  
```  
  
 È quindi possibile consentire agli utenti di selezionare il report dalla casella combinata e di visualizzare in anteprima il report nel form utilizzando un controllo browser o immagine.  
  
## <a name="enabling-report-viewing-and-navigation-using-windows-forms"></a>Abilitazione della visualizzazione e della navigazione dei report tramite Windows Form  
 Per integrare i report nelle applicazioni Windows Form, sono disponibili due metodi.  
  
 È possibile utilizzare l'API SOAP per eseguire il rendering dei report in qualsiasi formato di rendering supportato utilizzando il metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A>. L'abilitazione della visualizzazione e della navigazione dei report tramite SOAP presenta alcuni piccoli svantaggi:  
  
-   Non è possibile utilizzare le funzionalità predefinite della barra degli strumenti dei report disponibili nel Visualizzatore HTML tramite accesso con URL.  
  
-   Se si esegue il rendering in formato HTML, è necessario eseguire separatamente il rendering di qualsiasi immagine o risorsa come flusso aggiuntivo utilizzando il metodo <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A>.  
  
-   Il rendering di report tramite l'accesso con URL offre prestazioni leggermente migliori rispetto all'utilizzo dell'API SOAP.  
  
 È tuttavia possibile utilizzare il metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A> dell'API SOAP per eseguire il rendering dei report e salvarli in diversi formati di output a livello di programmazione. Questo è un vantaggio rispetto all'accesso con URL, che richiede l'interazione dell'utente. Quando si esegue il rendering di un report utilizzando il metodo <xref:ReportExecution2005.ReportExecutionService.Render%2A> dell'API SOAP, è possibile scegliere qualsiasi formato di output supportato.  
  
 È anche possibile usare gratuitamente i controlli ReportViewer distribuibili inclusi in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)]. I controlli ReportViewer consentono di incorporare in modo semplice le funzionalità di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nelle applicazioni personalizzate. Tali controlli sono destinati agli sviluppatori che desiderano fornire report predefiniti e completi come parte del set di caratteristiche di un'applicazione. Un'applicazione di gestione di un sito Web può ad esempio includere report relativi a un'analisi clickstream nei siti Web aziendali. L'incorporamento dei controlli in un'applicazione costituisce un'alternativa efficace all'inclusione dei componenti server di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella distribuzione dell'applicazione. I controlli forniscono funzionalità per i report, ma senza il supporto aggiuntivo per la creazione, la pubblicazione o la distribuzione e il recapito di report, disponibile in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Sono disponibili due versioni dei controlli ReportViewer: una versione per le applicazioni rich client Windows e una per le applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. I controlli supportano sia la modalità di elaborazione locale che quella remota. In modalità di elaborazione locale l'applicazione fornisce la definizione e i set di dati del report e avvia l'elaborazione del report. In modalità di elaborazione remota il recupero dei dati e l'elaborazione del report vengono eseguiti nel server di report e il controllo viene utilizzato per visualizzare e navigare il report. Questo modello consente di compilare applicazioni complete adatte per ambienti di qualsiasi dimensione, dal desktop all'azienda.  
  
 I controlli ReportViewer sono descritti nella Guida online di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Per ulteriori informazioni, vedere la documentazione di [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integrazione di Reporting Services nelle applicazioni](../application-integration/integrating-reporting-services-into-applications.md)   
 [Uso dell'API SOAP in un'applicazione Web](integrating-reporting-services-using-soap-web-application.md)  
  
  
