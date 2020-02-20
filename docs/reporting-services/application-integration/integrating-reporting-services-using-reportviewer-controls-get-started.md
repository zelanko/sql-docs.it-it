---
title: Guida introduttiva ai controlli Visualizzatore report
description: I controlli Visualizzatore report possono essere usati per integrare i report RDL di Reporting Services nelle app Web Form e Windows Form.
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: conceptual
ms.assetid: 01a821c4-2920-400c-be03-93d26c749bb1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d7e1e64bddcdcc7efed701770aea0e97c8e84ec5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75241832"
---
# <a name="integrating-reporting-services-using-the-report-viewer-controls---get-started"></a>Integrazione di Reporting Services tramite i controlli Visualizzatore report - Guida introduttiva

I controlli Visualizzatore report possono essere usati per integrare i report RDL di Reporting Services nelle app Web Form e Windows Form. Per informazioni dettagliate sugli aggiornamenti recenti, vedere il [registro delle modifiche](changelog.md).

## <a name="adding-the-report-viewer-control-to-a-new-web-project"></a>Aggiunta del controllo Visualizzatore report a un nuovo progetto Web

1. Creare un nuovo **sito Web ASP.NET vuoto** o aprire un progetto ASP.NET esistente.

    ![ssRS-Create-New-ASPNET-Project](../../reporting-services/application-integration/media/ssrs-create-new-aspnet-project.png)

2. Installare il pacchetto NuGet del controllo Visualizzatore report tramite la **console di Gestione pacchetti NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WebForms
    ```
3. Aggiungere una nuova pagina ASPX al progetto e registrare l'assembly del controllo Visualizzatore report per l'uso all'interno della pagina.

    ```
    <%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>
    ```
    
4. Aggiungere uno **ScriptManagerControl** alla pagina.

5. Aggiungere il controllo Visualizzatore report alla pagina. Il frammento seguente può essere aggiornato per fare riferimento a un report ospitato in un server di report remoto.

    ```
    <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
      <ServerReport ReportPath="" ReportServerUrl="" />
    </rsweb:ReportViewer>
    ```
    
La pagina finale sarà simile alla seguente.

```html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="Sample" %>

<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <meta http-equiv="X-UA-Compatible" content="IE=edge" /> 
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
    <asp:ScriptManager runat="server"></asp:ScriptManager>        
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote">
            <ServerReport ReportServerUrl="https://AContosoDepartment/ReportServer" ReportPath="/LatestSales" />
        </rsweb:ReportViewer>
    </form>
</body>
</html>
```

## <a name="updating-an-existing-project-to-use-the-report-viewer-control"></a>Aggiornamento di un progetto esistente per usare il controllo Visualizzatore report

Assicurarsi di aggiornare tutti i riferimenti degli assembly alla versione *15.0.0.0*, incluse le pagine web.config e tutte le pagine con estensione aspx che fanno riferimento al controllo visualizzatore.

### <a name="sample-webconfig-changes"></a>Modifiche del file web.config di esempio

```xml
<?xml version="1.0"?>
<!--
  For more information on how to configure your ASP.NET application, please visit
  https://go.microsoft.com/fwlink/?LinkId=169433
  -->
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.5.2">
      <assemblies>
        <!-- All assemblies updated to version 15.0.0.0. -->
        <add assembly="Microsoft.ReportViewer.Common, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.DataVisualization, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.Design, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.ProcessingObjectModel, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebDesign, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
        <add assembly="Microsoft.ReportViewer.WinForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </assemblies>
      <buildProviders>
        <!-- Version updated to 15.0.0.0. -->
        <add extension=".rdlc"
          type="Microsoft.Reporting.RdlBuildProvider, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
      </buildProviders>
    </compilation>
    <httpRuntime targetFramework="4.5.2"/>
    <httpHandlers>
      <!-- Version updated to 15.0.0.0 -->
      <add path="Reserved.ReportViewerWebControl.axd" verb="*"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"
        validate="false"/>
    </httpHandlers>
  </system.web>
  <system.webServer>
    <validation validateIntegratedModeConfiguration="false"/>
    <modules runAllManagedModulesForAllRequests="true"/>
    <handlers>
      <!-- Version updated to 15.0.0.0 -->
      <add name="ReportViewerWebControlHandler" verb="*" path="Reserved.ReportViewerWebControl.axd" preCondition="integratedMode"
        type="Microsoft.Reporting.WebForms.HttpHandler, Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845DCD8080CC91"/>
    </handlers>
  </system.webServer>
</configuration>
```

### <a name="sample-aspx"></a>Pagina ASPX di esempio

```
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SampleAspx" %>

<!-- Update version to 15.0.0.0 -->
<%@ Register assembly="Microsoft.ReportViewer.WebForms, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" namespace="Microsoft.Reporting.WebForms" tagprefix="rsweb" %>

<!DOCTYPE html>
```

## <a name="adding-the-report-viewer-control-to-a-new-windows-forms-project"></a>Aggiunta del controllo Visualizzatore report a un nuovo progetto Windows Forms

1. Creare una nuova **applicazione Windows Forms** o aprire un progetto esistente.

    ![ssRS-Create-New-winforms-Project](../../reporting-services/application-integration/media/ssrs-create-new-winforms-project.png)

2. Installare il pacchetto NuGet del controllo Visualizzatore report tramite la **console di Gestione pacchetti NuGet**.

    ```
    Install-Package Microsoft.ReportingServices.ReportViewerControl.WinForms
    ```
3. Aggiungere un nuovo controllo dal codice o [aggiungere il controllo alla casella degli strumenti](#adding-control-to-visual-studio-toolbar).

    ```csharp
    private Microsoft.Reporting.WinForms.ReportViewer reportViewer1;
    
    private void InitializeComponent()
    {
        this.reportViewer1 = new Microsoft.Reporting.WinForms.ReportViewer();
        this.SuspendLayout();
        // 
        // reportViewer1
        // 
        this.reportViewer1.Location = new System.Drawing.Point(168, 132);
        this.reportViewer1.Name = "reportViewer1";
        this.reportViewer1.ServerReport.BearerToken = null;
        this.reportViewer1.Size = new System.Drawing.Size(396, 246);
        this.reportViewer1.TabIndex = 0;
        // 
        // Form1
        // 
        this.Controls.Add(this.reportViewer1);
    }
    ```

## <a name="how-to-set-100-height-on-the-report-viewer-control"></a>Come impostare l'altezza 100% per il controllo Visualizzatore report

Se si imposta l'altezza del controllo visualizzatore al 100%, l'elemento padre deve avere un'altezza definita o tutti i predecessori devono avere altezze espresse in percentuale.

### <a name="setting-the-height-of-all-the-ancestors-to-100"></a>Impostazione dell'altezza di tutti i predecessori al 100%

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <style>
        html,body,form,#div1 {
            height: 100%; 
        }
    </style>
   </head>
<body>
    <form id="form1" runat="server">
    <div id="div1" >
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

### <a name="setting-the-parents-height-attribute"></a>Impostazione dell'attributo altezza dell'elemento padre

Per altre informazioni sulle lunghezze percentuali di Viewport, vedere [Viewport-percentage lengths](http://www.w3.org/TR/css3-values/#viewport-relative-lengths) (Viewport-lunghezze percentuali).

```html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
</head>
<body>
    <form id="form1" runat="server">
    <div style="height:100vh;">
            <asp:ScriptManager runat="server"></asp:ScriptManager>
        <rsweb:ReportViewer ID="ReportViewer1" runat="server" ProcessingMode="Remote" Height="100%" Width="100%">
            <ServerReport ReportServerUrl="https://test/ReportServer" ReportPath="/testreport" />
        </rsweb:ReportViewer>
    </div>
    </form>
</body>
</html>
```

## <a name="adding-control-to-visual-studio-toolbar"></a>Aggiunta del controllo alla barra degli strumenti di Visual Studio

Il controllo Visualizzatore Report è ora disponibile come pacchetto NuGet e non viene più visualizzato nella casella degli strumenti di Visual Studio per impostazione predefinita. È possibile aggiungere manualmente il controllo alla casella degli strumenti.

1. Installare il pacchetto NuGet per Windows Form o Web Form, come indicato in precedenza.

2. Rimuovere il controllo Visualizzatore report elencato nella casella degli strumenti.

    ![ssRS-remove-old-rvcontrol-toolbox](../../reporting-services/application-integration/media/ssrs-remove-old-rvcontrol-toolbox.png)

3. Fare clic con il pulsante destro del mouse in un punto qualsiasi della casella degli strumenti e selezionare **Scegli elementi**.

    ![ssRS-toolbox-choose-item](../../reporting-services/application-integration/media/ssrs-toolbox-choose-item.png)
    
4. In **Componenti di .NET Framework** selezionare **Sfoglia**.

    ![ssRS-toolbox-browse](../../reporting-services/application-integration/media/ssrs-toolbox-browse.png)

5. Selezionare il file **Microsoft.ReportViewer.WinForms.dll** o **Microsoft.ReportViewer.WebForms.dll** dal pacchetto NuGet installato.

    > [!NOTE] 
    > Il pacchetto NuGet verrà installato nella directory della soluzione del progetto. Il percorso al file DLL sarà simile al seguente: `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.Winforms.{version}\lib\net40` o `{Solution Directory}\packages\Microsoft.ReportingServices.ReportViewerControl.WebForms.{version}\lib\net40`.

6. Il nuovo controllo viene visualizzato all'interno della casella degli strumenti. È quindi possibile spostarlo in un'altra scheda all'interno della casella degli strumenti se necessario.

    ![ssRS-toolbox-rvcontrol](../../reporting-services/application-integration/media/ssrs-toolbox-rvcontrol.png)

## <a name="common-issues"></a>Problemi comuni
    
Il controllo visualizzatore è progettato per i browser moderni. Il controllo potrebbe non funzionare come previsto se il browser esegue il rendering della pagina usando la modalità di compatibilità di Internet Explorer. I siti Intranet potrebbero richiedere un tag META per l'override del comportamento predefinito del browser.

    ```
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    ```
      
## <a name="feedback"></a>Commenti e suggerimenti

Segnalare eventuali problemi al team di prodotto nei [forum di Reporting Services](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlreportingservices).

## <a name="see-also"></a>Vedere anche

[Raccolta dati nel controllo Visualizzatore report](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls-data-collection.md)  
Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)

