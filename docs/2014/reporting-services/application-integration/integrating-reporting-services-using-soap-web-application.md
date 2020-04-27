---
title: Using the SOAP API in a Web Application (Uso dell'API SOAP in un'applicazione Web) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
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
manager: kfile
ms.openlocfilehash: 5a90135c634e45f3fb4e3ff9c780347caaea24f9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63126268"
---
# <a name="using-the-soap-api-in-a-web-application"></a>Utilizzo dell'API SOAP in un'applicazione Web
  È possibile accedere alle funzionalità complete del server di report tramite l'API SOAP di Reporting Services. L'API SOAP è un servizio Web e, in quanto tale, è possibile accedervi in modo semplice per fornire caratteristiche di creazione di report aziendali alle applicazioni aziendali personalizzate. È possibile accedere al servizio Web ReportServer da un'applicazione Web nello stesso modo in cui si accede all'API SOAP da un'applicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]Utilizzando, è possibile generare una classe proxy che espone le proprietà e i metodi del servizio Web ReportServer e consente di utilizzare un'infrastruttura e strumenti familiari per compilare applicazioni aziendali sulla [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tecnologia.  
  
 È possibile accedere alla funzionalità di gestione dei report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con la stessa facilità da un'applicazione Web o da un'applicazione Windows. Da un'applicazione Web, è possibile aggiungere e rimuovere gli elementi al e dal database del server di report, impostare la sicurezza degli elementi, modificare gli elementi del database del server di report, gestire le pianificazione e il recapito e altro ancora.  
  
## <a name="enabling-impersonation"></a>Abilitazione della rappresentazione  
 Il primo passaggio per la configurazione dell'applicazione Web consiste nell'attivare la rappresentazione dal client del servizio Web. Con la rappresentazione, le applicazioni [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] possono venire eseguite con l'identità del client per il quale operano. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] si basa su [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) per autenticare l'utente e passare un token autenticato all'applicazione [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] o, nel caso in cui non sia possibile autenticare l'utente, passare un token non autenticato. In entrambi i casi, l'applicazione [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] rappresenta il token ricevuto, se la rappresentazione è abilitata. È possibile abilitare la rappresentazione nel client modificando il file Web.config dell'applicazione client come indicato di seguito:  
  
```  
<!-- Web.config file. -->  
<identity impersonate="true"/>  
```  
  
> [!NOTE]  
>  Per impostazione predefinita, la rappresentazione è disabilitata.  
  
 Per ulteriori informazioni sulla [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] rappresentazione, vedere la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentazione di SDK.  
  
## <a name="managing-the-report-server-using-soap-api"></a>Gestione del server di report tramite l'API SOAP  
 È inoltre possibile utilizzare l'applicazione Web per gestire un server di report e i relativi contenuti. Gestione report, disponibile con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è un esempio di applicazione Web compilata completamente utilizzando [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e l'API SOAP di Reporting Services. È possibile aggiungere le funzionalità di Gestione report alle applicazioni Web personalizzate. È ad esempio possibile che si desideri restituire un elenco di report disponibili nel database del server di report e visualizzarli in [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] `Listbox` un controllo per consentire agli utenti di scegliere tra loro. Nel codice seguente viene eseguita la connessione al database del server di report e viene restituito un elenco di elementi disponibili nel database del server di report. I report disponibili vengono aggiunti quindi a un controllo ListBox, in cui viene visualizzato il percorso di ogni report.  
  
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
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Integrazione di Reporting Services in applicazioni](../application-integration/integrating-reporting-services-into-applications.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Uso dell'API SOAP in un'applicazione Windows](integrating-reporting-services-using-soap-windows-application.md)  
  
  
