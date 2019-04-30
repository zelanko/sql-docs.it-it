---
title: "Procedura: Distribuire un'estensione di elaborazione dei dati in Progettazione Report | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 947ad59b8ac20862a8ef6da8ea527e2befb1be57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63164323"
---
# <a name="how-to-deploy-a-data-processing-extension-to-report-designer"></a>Procedura: Distribuire un'estensione per l'elaborazione dati in Progettazione report
  In Progettazione report vengono utilizzate le estensioni per l'elaborazione dati per il recupero e l'elaborazione dei dati durante la progettazione dei report. È necessario distribuire l'assembly di estensioni per l'elaborazione dati in Progettazione report come assembly privato. È inoltre necessario immettere una voce nel file di configurazione di Progettazione report, RSReportDesigner.config.  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>Per distribuire un assembly dell'estensione per l'elaborazione dati  
  
1.  Copiare l'assembly dal percorso di gestione temporanea nella directory di Progettazione report. Il percorso predefinito della directory di Progettazione report è C:\Programmi\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
2.  Dopo aver copiato il file di assembly, aprire il file RSReportDesigner.config. Anche questo file si trova nella directory di Progettazione report. È necessario immettere una voce nel file di configurazione per il file di assembly dell'estensione per l'elaborazione dati. È possibile aprire il file di configurazione con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o con un semplice editor di testo, ad esempio Blocco note.  
  
3.  Individuare l'elemento **Data** nel file RSReportDesigner.config. È necessario immettere una voce per l'estensione per l'elaborazione dati appena creata nel percorso seguente:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Aggiungere una voce per l'estensione per l'elaborazione dati che include un' **estensione** elemento con i valori per il `Name`, `Type`, e `Visible` attributi. La voce può essere simile alla seguente:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     Il valore per `Name` è il nome univoco dell'estensione per l'elaborazione dati. Il valore per `Type` è un elenco delimitato da virgole che include una voce per lo spazio dei nomi completo della classe che implementa le interfacce <xref:Microsoft.ReportingServices.Interfaces.IExtension> e <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>, seguito dal nome dell'assembly, senza l'estensione dll. Per impostazione predefinita, le estensioni per l'elaborazione dati sono visibili. Per nascondere un'estensione dalle interfacce utente, ad esempio Progettazione Report, aggiungere un `Visible` dell'attributo per il **estensione** elemento e impostarlo su `false`.  
  
5.  Aggiungere infine un gruppo di codice per l'assembly personalizzato che conceda l'autorizzazione **FullTrust** per l'estensione. A tale scopo, aggiungere il gruppo di codice al file rspreviewpolicy.config che, per impostazione predefinita, si trova in C:\Programmi\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies. Il gruppo di codice può essere simile a quanto riportato di seguito:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 L'appartenenza URL è solo una delle diverse condizioni di appartenenza selezionabili per l'estensione per l'elaborazione dati. Per altre informazioni sulla sicurezza dall'accesso di codice in [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)], vedere [Sviluppo sicuro &#40;Reporting Services&#41;](../secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>Progettazione query standard  
 In Progettazione report è disponibile una finestra Progettazione query standard che è possibile utilizzare con le estensioni per l'elaborazione dati personalizzate. Questa finestra di progettazione è costituita da due riquadri, uno per le query e uno per i risultati. È possibile utilizzare la finestra Progettazione query standard per scrivere query non supportate dall'interfaccia grafica. Diversamente dalla finestra Progettazione query con interfaccia grafica, l'interfaccia standard di Progettazione query non controlla la sintassi della query né ristruttura la query.  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>Per abilitare la finestra Progettazione query standard per un'estensione personalizzata  
  
-   Aggiungere la voce seguente al file RSReportDesigner. config sotto il **Designer** elemento, sostituendo il `Name` attributo con il nome specificato nelle voci precedenti.  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>Verifica della distribuzione  
 Per poter verificare la distribuzione, è necessario chiudere tutte le istanze di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] nel computer locale. Dopo aver chiuso tutte le sessioni correnti, è possibile verificare se l'estensione per l'elaborazione dati è stata distribuita correttamente in Progettazione report creando un nuovo progetto report in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Quando si crea un nuovo set di dati per il report, l'estensione dovrebbe essere inclusa nell'elenco dei tipi di origini dati disponibili.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuzione di un'estensione per l'elaborazione dati](deploying-a-data-processing-extension.md)   
 [Estensioni di Reporting Services](../reporting-services-extensions.md)   
 [Implementazione di un'estensione per l'elaborazione dati](implementing-a-data-processing-extension.md)   
 [Libreria di estensioni di Reporting Services](../reporting-services-extension-library.md)  
  
  
