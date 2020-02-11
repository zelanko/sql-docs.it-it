---
title: 'Lezione 3: accesso al servizio Web | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c3e4c198-ab35-4548-9471-1b4e6b6e5dfd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 09671f8880f9f7745359961d9c6c126a893d26a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62653784"
---
# <a name="lesson-3-accessing-the-web-service"></a>Lezione 3: Accesso al servizio Web
  Dopo avere aggiunto al progetto un riferimento al servizio Web ReportServer, il passaggio successivo consiste nel creare un'istanza della classe proxy del servizio Web. Per accedere ai metodi del servizio Web, è quindi possibile eseguire una chiamata dalla classe proxy. Quando l'applicazione chiama questi metodi, il codice della classe proxy generato da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] gestisce le comunicazioni tra l'applicazione e il servizio Web.  
  
 Verrà innanzitutto creata un'istanza della classe proxy del servizio Web, ovvero <xref:ReportService2010.ReportingService2010>, quindi verrà utilizzata la classe proxy per chiamare il metodo <xref:ReportService2010.ReportingService2010.GetProperties%2A> del servizio Web. La chiamata del metodo verrà utilizzata per recuperare il nome e la descrizione di uno dei report di esempio, ovvero Company Sales.  
  
> [!NOTE]  
>  Quando si accede a un servizio Web in esecuzione in [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] with Advanced Services, è necessario aggiungere "$SQLExpress" al percorso "ReportServer". Ad esempio:  
>   
>  `http://<Server Name>/reportserver$sqlexpress/reportservice2010.asmx"`  
  
### <a name="to-access-the-web-service"></a>Per accedere al servizio Web  
  
1.  Aggiungere innanzitutto lo spazio dei nomi al file Program.cs (Module1.vb in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) tramite l'aggiunta di una direttiva `using` (`Imports` in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) al file di codice. Quando si utilizza questa direttiva, non è necessario specificare il nome completo dei tipi nello spazio dei nomi.  
  
2.  A tale scopo, aggiungere il codice seguente all'inizio del file di codice:  
  
    ```vb  
    Imports System  
    Imports GetPropertiesSample.ReportService2010  
    ```  
  
    ```csharp  
    using System;  
    using GetPropertiesSample.ReportService2010;  
    ```  
  
3.  Dopo avere immesso la direttiva dello spazio dei nomi nel file del codice, immettere il codice seguente nel metodo Main dell'applicazione console. Assicurarsi di modificare il nome del server quando si imposta la proprietà **Url** dell'istanza del servizio Web:  
  
    ```vb  
    Sub Main()  
       Dim rs As New ReportingService2010  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx"  
  
       Dim name As New [Property]  
       name.Name = "Name"  
  
       Dim description As New [Property]  
       description.Name = "Description"  
  
       Dim properties(1) As [Property]  
       properties(0) = name  
       properties(1) = description  
  
       Try  
          Dim returnProperties As [Property]() = rs.GetProperties( _  
             "/AdventureWorks 2012 Sample Reports/Company Sales 2012", properties)  
  
          Dim p As [Property]  
          For Each p In returnProperties  
              Console.WriteLine((p.Name + ": " + p.Value))  
          Next p  
  
       Catch e As Exception  
          Console.WriteLine(e.Message)  
       End Try  
    End Sub  
    ```  
  
    ```csharp  
    static void Main(string[] args)  
    {  
       ReportingService2010 rs = new ReportingService2010();  
       rs.Credentials = System.Net.CredentialCache.DefaultCredentials;  
       rs.Url = "http://<Server Name>/reportserver/reportservice2010.asmx";  
  
       Property name = new Property();  
       name.Name = "Name";  
  
       Property description = new Property();  
       description.Name = "Description";  
  
       Property[] properties = new Property[2];  
       properties[0] = name;  
       properties[1] = description;  
  
       try  
       {  
          Property[] returnProperties = rs.GetProperties(  
          "/AdventureWorks 2012 Sample Reports/Company Sales 2012",properties);  
  
          foreach (Property p in returnProperties)  
          {  
             Console.WriteLine(p.Name + ": " + p.Value);  
          }  
       }  
  
       catch (Exception e)  
       {  
          Console.WriteLine(e.Message);  
       }  
    }  
    ```  
  
4.  Salvare la soluzione.  
  
 Nel codice di esempio dell'esercitazione viene utilizzato il metodo <xref:ReportService2010.ReportingService2010.GetProperties%2A> del servizio Web per recuperare le proprietà del report di esempio Company Sales 2012. Il <xref:ReportService2010.ReportingService2010.GetProperties%2A> metodo accetta due argomenti: il nome del report per il quale si desidera recuperare le informazioni sulle proprietà e una matrice di oggetti **Property []** contenente i nomi delle proprietà di cui si desidera recuperare i valori. Il metodo restituisce inoltre una matrice di oggetti **Property []** che contiene i nomi e i valori delle proprietà specificate nell'argomento Properties.  
  
> [!NOTE]  
>  Se si specifica una matrice di **Proprietà []** vuota per l'argomento Properties, verranno restituite tutte le proprietà disponibili.  
  
 Nel codice dell'esempio precedente viene utilizzato il metodo <xref:ReportService2010.ReportingService2010.GetProperties%2A> per restituire il nome e la descrizione del report di esempio Company Sales 2012, quindi viene utilizzato un ciclo `foreach` per scrivere le proprietà e i valori nella console.  
  
 Per ulteriori informazioni sulla creazione e l'utilizzo di una classe proxy per il servizio Web ReportServer, vedere [Creating the Web Service Proxy](../reporting-services/report-server-web-service/net-framework/creating-the-web-service-proxy.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Lezione 4: esecuzione dell'applicazione &#40;VB-VC&#35;&#41;](../../2014/tutorials/lesson-4-running-the-application-vb-vcsharp.md)   
 [Accesso al servizio Web ReportServer utilizzando Visual Basic o Visual C&#35; &#40;SSRS tutorial&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
