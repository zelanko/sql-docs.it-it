---
title: 'Lezione 1: Creare il progetto di Visual Studio Schema RDL | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f420509c-51aa-4170-8c25-64c2954f4bb9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c34062acefc2dfd847790a39cea35b03727f49ff
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018912"
---
# <a name="lesson-1-create-the-rdl-schema-visual-studio-project"></a>Lezione 1: Creare il progetto di Visual Studio Schema RDL
  Per questa esercitazione verrà creata una semplice applicazione console. Questa esercitazione si presuppone cui si sta sviluppando [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)].  
  
> [!NOTE]  
>  Quando si accede al servizio Web ReportServer in esecuzione su [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services, è necessario aggiungere "_SQLExpress" al percorso "ReportServer". Ad esempio:  
>   
>  `http://myserver/reportserver_sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-create-the-web-service-proxy"></a>Per creare il proxy del servizio Web  
  
1.  Dal **avviare** dal menu **tutti i programmi**, quindi Microsoft Visual Studio, quindi **strumenti di Visual Studio**e quindi **Prompt dei comandi di Visual Studio 2010** .  
  
2.  Nella finestra del prompt dei comandi, eseguire il comando seguente se si utilizza C#:  
  
    ```  
    wsdl /language:CS /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Se si utilizza Visual Basic, eseguire il comando seguente:  
  
    ```  
    wsdl /language:VB /n:"ReportService2010" http://<Server Name>/reportserver/reportservice2010.asmx?wsdl  
    ```  
  
     Questo comando genera un file con estensione cs o vb. Questo file verrà aggiunto all'applicazione.  
  
### <a name="to-create-a-console-application"></a>Per creare un'applicazione console  
  
1.  Nel **File** dal menu **New**e quindi fare clic su **progetto** per aprire la **nuovo progetto** nella finestra di dialogo.  
  
2.  Nel riquadro sinistro, sotto **modelli installati**, fare clic su **Visual Basic** o nella **Visual c#** nodo e selezionare una categoria di progetto tipi dall'elenco espanso.  
  
3.  Scegliere il **applicazione Console** tipo di progetto.  
  
4.  Nel **nome** immettere un nome per il progetto. Digitare il nome `SampleRDLSchema`.  
  
5.  Nel **ubicazione** , digitare il percorso in cui si desidera salvare il progetto oppure fare clic su **Sfoglia** per passare alla cartella.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] Verrà visualizzata una vista compressa del progetto in Esplora soluzioni.  
  
7.  Nel menu **Progetto** fare clic su **Aggiungi elemento esistente**.  
  
8.  Passare al percorso per l'estensione cs o vb file generato, quindi selezionare il file e quindi fare clic su **Add**.  
  
     È inoltre necessario aggiungere un riferimento allo spazio dei nomi <xref:System.Web.Services> per il riferimento Web da utilizzare.  
  
9. Nel menu progetto, fare clic su **Aggiungi riferimento**.  
  
     Nel **Aggiungi riferimento** nella finestra di dialogo il **.NET** scheda, seleziona **System**, quindi fare clic su **OK**.  
  
     Per altre informazioni su come connettersi al servizio Web ReportServer, vedere [compilazione di applicazioni tramite il servizio Web e .NET Framework](../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md).  
  
10. Espandere il nodo del progetto in Esplora soluzioni. Al progetto è stato aggiunto un file di codice con il nome predefinito Program.cs (Module1.vb per [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]).  
  
11. Aprire il file Program.cs (Module1.vb per [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) e sostituire il codice con quanto segue:  
  
     Il codice seguente fornisce gli stub del metodo da utilizzare per l'implementazione della funzionalità di caricamento, aggiornamento e salvataggio.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using System.Xml.Serialization;  
    using ReportService2010;  
  
    namespace SampleRDLSchema  
    {  
        class ReportUpdater  
        {  
            ReportingService2010 _reportService;  
  
            static void Main(string[] args)  
            {  
                ReportUpdater reportUpdater = new ReportUpdater();  
                reportUpdater.UpdateReport();  
            }  
  
            private void UpdateReport()  
            {  
                try  
                {  
                    // Set up the Report Service connection  
                    _reportService = new ReportingService2010();  
                    _reportService.Credentials =  
                        System.Net.CredentialCache.DefaultCredentials;  
                    _reportService.Url =  
                       "http://<Server Name>/reportserver/" +  
                                       "reportservice2010.asmx";  
  
                    // Call the methods to update a report definition  
                    LoadReportDefinition();  
                    UpdateReportDefinition();  
                    PublishReportDefinition();  
                }  
                catch (Exception ex)  
                {  
                    System.Console.WriteLine(ex.Message);  
                }  
            }  
  
            private void LoadReportDefinition()  
            {  
                //Lesson 3: Load a report definition from the report   
                //          catalog  
            }  
  
            private void UpdateReportDefinition()  
            {  
                //Lesson 4: Update the report definition using the    
                //          classes generated from the RDL Schema  
            }  
  
            private void PublishReportDefinition()  
            {  
                //Lesson 5: Publish the updated report definition back   
                //          to the report catalog  
            }  
        }  
    }  
    ```  
  
    ```vb  
    Imports System  
    Imports System.Collections.Generic  
    Imports System.IO  
    Imports System.Text  
    Imports System.Xml  
    Imports System.Xml.Serialization  
    Imports ReportService2010  
  
    Namespace SampleRDLSchema  
  
        Module ReportUpdater  
  
            Private m_reportService As ReportingService2010  
  
            Public Sub Main(ByVal args As String())  
  
                Try  
                    'Set up the Report Service connection  
                    m_reportService = New ReportingService2010  
                    m_reportService.Credentials = _  
                        System.Net.CredentialCache.DefaultCredentials  
                    m_reportService.Url = _  
                        "http:// <Server Name>/reportserver/" & _  
                               "reportservice2010.asmx"  
  
                    'Call the methods to update a report definition  
                    LoadReportDefinition()  
                    UpdateReportDefinition()  
                    PublishReportDefinition()  
                Catch ex As Exception  
                    System.Console.WriteLine(ex.Message)  
                End Try  
  
            End Sub  
  
            Private Sub LoadReportDefinition()  
                'Lesson 3: Load a report definition from the report   
                '          catalog  
            End Sub  
  
            Private Sub UpdateReportDefinition()  
                'Lesson 4: Update the report definition using the   
                '          classes generated from the RDL Schema  
            End Sub  
  
            Private Sub PublishReportDefinition()  
                'Lesson 5: Publish the updated report definition back   
                '          to the report catalog  
            End Sub  
  
        End Module  
  
    End Namespace   
    ```  
  
## <a name="next-lesson"></a>Lezione successiva  
 Nella lezione successiva verrà utilizzato lo strumento per la definizione di XML Schema (Xsd.exe) per generare classi dallo schema RDL e includerle nel progetto. Vedere [lezione 2: Generare classi dallo Schema RDL mediante lo strumento xsd](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei report mediante le classi generate dallo Schema RDL &#40;esercitazione su SSRS&#41;](../../2014/tutorials/updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial.md)   
 [Report Definition Language &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
