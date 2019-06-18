---
title: Distribuzione di un'estensione per il recapito | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- delivery extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: 4436ce48-397d-42c7-9b5d-2a267e2a1b2c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 06cffe614eaa55713fed862dc03f7c81da7bc287
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193769"
---
# <a name="deploying-a-delivery-extension"></a>Distribuzione di un'estensione per il recapito
  Le estensioni per il recapito forniscono le informazioni di configurazione in un file di configurazione XML. Il file XML è conforme all'elemento XML Schema definito per le estensioni per il recapito. Le estensioni per il recapito forniscono l'infrastruttura per l'impostazione e la modifica del file di configurazione.  
  
 Se un'estensione per il recapito viene sostituita o aggiornata, tutte le sottoscrizioni che fanno riferimento all'estensione per il recapito rimangono valide.  
  
 Dopo avere scritto e compilato l'estensione per il recapito [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] in una libreria [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], è necessario copiarla nella directory appropriata e aggiungere una voce al file di configurazione [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] appropriato, in modo che il server di report possa individuarla.  
  
## <a name="configuration-file-extension-element"></a>Elemento Extension del file di configurazione  
 Le estensioni per il recapito distribuite nel server di report devono essere immesse come elementi **Extension** nel file di configurazione. Il file di configurazione per il server di report è RSReportServer.config.  
  
 Nella tabella riportata di seguito vengono descritti gli attributi dell'elemento **Extension** per le estensioni per il recapito.  
  
|attribute|Descrizione|  
|---------------|-----------------|  
|**Nome**|Nome univoco per l'estensione, ad esempio "Posta elettronica server di report" per l'estensione per il recapito tramite posta elettronica o "Condivisione file server di report" per l'estensione per il recapito tramite condivisione. La lunghezza massima consentita per l'attributo **Name** è 255 caratteri. Il nome deve essere univoco tra tutte le voci dell'elemento **Extension** di un file di configurazione. Se è presente un nome duplicato, il server di report restituirà un errore.|  
|**Tipo**|Elenco delimitato da virgole che include lo spazio dei nomi completo insieme al nome dell'assembly.|  
|**Visible**|Il valore **false** indica che l'estensione per il recapito non deve essere visibile nelle interfacce utente. Se l'attributo non è incluso, il valore predefinito è **true**.|  
  
 Per altre informazioni sul file RSReportServer.config, vedere [File di configurazione di Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="deploying-the-extension-to-the-report-server"></a>Distribuzione dell'estensione nel server di report  
 Il server di report utilizza estensioni per il recapito per l'elaborazione e il recapito di notifiche o report. È necessario distribuire l'assembly di estensioni per il recapito in un server di report come assembly privato. È inoltre necessario creare una voce nel file di configurazione del server di report, ovvero RSReportServer.config.  
  
#### <a name="to-deploy-a-deliver-extension-assembly-to-a-report-server"></a>Per distribuire un assembly di estensioni per il recapito in un server di report  
  
1.  Copiare l'assembly dal percorso di gestione temporanea nella directory bin del server di report in cui si desidera utilizzare l'estensione per il recapito. Il percorso predefinito della directory bin del server di report è %Programmi%\Microsoft SQL Server\MSRS13.\<NomeIstanza>\Reporting Services\ReportServer\bin.  
  
    > [!IMPORTANT]  
    >  Se si tenta di sovrascrivere un assembly di estensioni per il recapito esistente, è necessario arrestare il servizio del server di report prima di copiare l'assembly aggiornato. Riavviare il servizio dopo il completamento della copia dell'assembly.  
  
2.  Dopo aver copiato il file di assembly, aprire il file RSReportServer.config Il file RSReportServer.config si trova nella directory %Programmi%\Microsoft SQL Server\MSRS13.\<NomeIstanza>\Reporting Services\ReportServer. È necessario immettere una voce nel file di configurazione per il file di assembly di estensioni per il recapito. È possibile aprire il file di configurazione con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o con un semplice editor di testo, ad esempio Blocco note.  
  
3.  Individuare l'elemento **Delivery** nel file RSReportServer.config. È necessario immettere una voce per l'estensione per il recapito appena creata nel percorso seguente:  
  
    ```  
    <Extensions>  
       <Delivery>  
          <Your extension configuration information goes here>  
       </Delivery>  
    </Extensions>  
    ```  
  
4.  Aggiungere una voce per l'estensione per il recapito. La voce deve includere un elemento **Extension** con i valori per **Name** e **Type** e può essere simile a quanto riportato di seguito:  
  
    ```  
    <Extension Name="My Delivery Extension Name" Type="CompanyName.ExtensionName.MyDeliveryExtensionClass, AssemblyName" />  
    ```  
  
     Il valore per **Name** è il nome univoco dell'estensione per il recapito. Il valore per **Type** è un elenco delimitato da virgole che include una voce per lo spazio dei nomi completo della classe che implementa l'interfaccia <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>, seguita dal nome dell'assembly, senza l'estensione dll. Per impostazione predefinita, le estensioni per il recapito sono visibili. Per nascondere un'estensione dalle interfacce utente, ad esempio il portale Web, aggiungere un attributo **Visible** all'elemento **Extension** e impostarlo su **false**.  
  
5.  Aggiungere infine un gruppo di codice per l'assembly personalizzato che conceda l'autorizzazione **FullTrust** per l'estensione per il recapito. A questo scopo, aggiungere il gruppo di codice al file rssrvpolicy.config che per impostazione predefinita si trova in %Programmi%\Microsoft SQL Server\MSRS13.\<NomeIstanza>\Reporting Services\ReportServer. Il gruppo di codice può essere simile a quanto riportato di seguito:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my delivery extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft SQL Server\MSRS13.<InstanceName>\Reporting Services\ReportServer\bin\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
     L'appartenenza URL è solo una delle numerose condizioni di appartenenza che è possibile scegliere per l'estensione per il recapito. Per altre informazioni sulla sicurezza dall'accesso di codice in [!INCLUDE[ssRS](../../../includes/ssrs.md)], vedere [Sviluppo sicuro &#40;Reporting Services&#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
   
## <a name="verifying-the-deployment"></a>Verifica della distribuzione  
 È possibile verificare se l'estensione per il recapito è stata distribuita correttamente nel server di report tramite il metodo <xref:ReportService2010.ReportingService2010.ListExtensions%2A> del servizio Web. È inoltre possibile aprire il portale Web e verificare che l'estensione sia inclusa nell'elenco delle estensioni per il recapito disponibili per una sottoscrizione. Per altre informazioni sul portale Web e sulle sottoscrizioni, vedere [Sottoscrizioni e recapito &#40;Reporting Services&#41;](../../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Implementazione di un'estensione per il recapito](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Libreria di estensioni di Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
