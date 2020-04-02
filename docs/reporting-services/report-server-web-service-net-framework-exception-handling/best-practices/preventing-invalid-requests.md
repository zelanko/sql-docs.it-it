---
title: Metodi per evitare le richieste non valide | Microsoft Docs
description: Informazioni su come evitare richieste non valide analizzando il flusso dell'applicazione e assicurandosi che le richieste inviate al server di report siano valide.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c11cfc1213e70bf362185a63883b8e84282696ca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216367"
---
# <a name="preventing-invalid-requests"></a>Metodi per evitare le richieste non valide
  È possibile impedire la generazione di alcuni tipi di eccezioni analizzando il flusso dell'applicazione e assicurandosi che le richieste inviate al server di report siano valide. Nelle applicazioni che consentono agli utenti di aggiungere o aggiornare il nome di un report, un'origine dati o un altro elemento del server di report, è necessario convalidare il testo che un utente potrebbe immettere. È sempre necessario verificare se sono presenti caratteri riservati prima di inviare la richiesta a un server di report. Usare istruzioni **if** condizionali o altri costrutti logici nel codice per avvisare l'utente che non sono state soddisfatte le condizioni necessarie per l'invio delle richieste al server di report.  
  
 Nell'esempio C# semplificato seguente, gli utenti visualizzano ad esempio un messaggio di errore descrittivo quando tentano di creare un report con un nome che contiene una barra (/).  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 Per altre informazioni sui tipi di errore che è possibile prevenire prima dell'invio delle richieste al server di report, vedere [Tabella degli errori SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md). Per altre informazioni su come migliorare ulteriormente l'esempio precedente usando blocchi try/catch, vedere [Uso di blocchi try e catch](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla gestione delle eccezioni in Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException di Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
