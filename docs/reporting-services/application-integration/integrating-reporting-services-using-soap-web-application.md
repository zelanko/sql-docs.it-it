---
title: Using the SOAP API in a Web Application (Uso dell'API SOAP in un'applicazione Web) | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], Web applications
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- report servers [Reporting Services], SOAP
- Web applications [Reporting Services]
ms.assetid: e8ca4455-0dc3-4741-8872-3636114938ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 53196d1336bb7be6093b749acb93f1ad95a99852
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62741958"
---
# <a name="integrating-reporting-services-using-soap---web-application"></a>Integrazione di Reporting Services tramite SOAP - Applicazione Web
  È possibile accedere alle funzionalità complete del server di report tramite l'API SOAP di Reporting Services. L'API SOAP è un servizio Web e, in quanto tale, è possibile accedervi in modo semplice per fornire caratteristiche di creazione di report aziendali alle applicazioni aziendali personalizzate. È possibile accedere al servizio Web ReportServer da un'applicazione Web nello stesso modo in cui si accede all'API SOAP da un'applicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Usando [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], è possibile generare una classe proxy che espone le proprietà e i metodi del servizio Web ReportServer e consente di utilizzare un'infrastruttura e strumenti familiari per compilare applicazioni aziendali in tecnologia [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 È possibile accedere alla funzionalità di gestione dei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con la stessa facilità da un'applicazione Web o da un'applicazione Windows. Da un'applicazione Web, è possibile aggiungere e rimuovere gli elementi al e dal database del server di report, impostare la sicurezza degli elementi, modificare gli elementi del database del server di report, gestire le pianificazione e il recapito e altro ancora.  
  
## <a name="enabling-impersonation"></a>Abilitazione della rappresentazione  
 Il primo passaggio per la configurazione dell'applicazione Web consiste nell'attivare la rappresentazione dal client del servizio Web. Con la rappresentazione, le applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] possono venire eseguite con l'identità del client per il quale operano. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] si basa su [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) per autenticare l'utente e passare un token autenticato all'applicazione [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] o, nel caso in cui non sia possibile autenticare l'utente, passare un token non autenticato. In entrambi i casi, l'applicazione [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] rappresenta il token ricevuto, se la rappresentazione è abilitata. È possibile abilitare la rappresentazione nel client modificando il file Web.config dell'applicazione client come indicato di seguito:  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  Per impostazione predefinita, la rappresentazione è disabilitata.  
  
 Per altre informazioni sulla rappresentazione in [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)], vedere la documentazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="managing-the-report-server-using-soap-api"></a>Gestione del server di report tramite l'API SOAP  
 È inoltre possibile utilizzare l'applicazione Web per gestire un server di report e i relativi contenuti. Gestione report, disponibile con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è un esempio di applicazione Web compilata completamente utilizzando [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e l'API SOAP di Reporting Services. È possibile aggiungere le funzionalità di Gestione report alle applicazioni Web personalizzate. È ad esempio possibile fare in modo che venga restituito un elenco di report disponibili nel database del server di report e visualizzarli in un controllo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] **Listbox** per consentire agli utenti di scegliere i report dall'elenco. Nel codice seguente viene eseguita la connessione al database del server di report e viene restituito un elenco di elementi disponibili nel database del server di report. I report disponibili vengono aggiunti quindi a un controllo ListBox, in cui viene visualizzato il percorso di ogni report.  
  
```vb  
Private Sub Page_Load(sender As Object, e As System.EventArgs)  
   ' Create a Web service proxy object and set credentials  
   Dim rs As New ReportingService2005()  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
  
   ' Return a list of catalog items in the report server database  
   Dim items As CatalogItem() = rs.ListChildren("/", True)  
  
   ' For each report, display the path of the report in a Listbox  
   Dim ci As CatalogItem  
   For Each ci In  items  
      If ci.Type = ItemTypeEnum.Report Then  
         catalogListBox.Items.Add(ci.Path)  
      End If  
   Next ci  
End Sub ' Page_Load   
```  
  
```csharp  
private void Page_Load(object sender, System.EventArgs e)  
{  
   // Create a Web service proxy object and set credentials  
   ReportingService2005 rs = new ReportingService2005();  
   rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
  
   // Return a list of catalog items in the report server database  
   CatalogItem[] items = rs.ListChildren("/", true);  
  
   // For each report, display the path of the report in a Listbox  
   foreach(CatalogItem ci in items)  
   {  
      if (ci.Type == ItemTypeEnum.Report)  
         catalogListBox.Items.Add(ci.Path);  
   }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integrazione di Reporting Services nelle applicazioni](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Uso dell'API SOAP in un'applicazione Windows](../../reporting-services/application-integration/integrating-reporting-services-using-soap-windows-application.md)  
  
  
