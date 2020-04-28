---
title: Ruolo di SOAP in Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4e0b418e44436912b5ed1368ad7a316951872266
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62519202"
---
# <a name="the-role-of-soap-in-reporting-services"></a>Ruolo di SOAP in Reporting Services
  Il servizio Web ReportServer utilizza la messaggistica SOAP (Simple Object Access Protocol) per inviare comandi basati su testo in una rete. Questi comandi sono in formato di testo XML e vengono inviati nel World Wide Web utilizzando HTTP. Grazie all'utilizzo di SOAP come protocollo di comunicazione, il servizio Web ReportServer consente alle applicazioni e ai componenti di scambiare dati con il server di report utilizzando un'infrastruttura aperta molto diffusa. Lo standard SOAP è definito nel sito www.w3.org/TR/SOAP (informazioni in lingua inglese).  
  
 Qualsiasi applicazione client può essere utilizzata come client SOAP a condizione che supporti SOAP e che sia in grado di inviare richieste SOAP. Gestione report è un client SOAP. Questo client fornisce un'interfaccia per il database del server di report in cui vengono archiviati tutti i report e il contenuto correlato ai report. Gli utenti finali possono utilizzare l'applicazione per esplorare e gestire report e cartelle nello spazio dei nomi del server di report. Gestione report è basato sull'infrastruttura del servizio Web ReportServer.  
  
 Un server di report funge da server SOAP, un servizio che supporta SOAP in grado di accettare le richieste dai client SOAP e di creare risposte appropriate. Il server gestisce le richieste e restituisce al client risposte codificate.  
  
 I messaggi SOAP in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono avere formati diversi, a seconda del tipo di richiesta effettuata dal client. Nell'esempio seguente viene rappresentata una semplice richiesta client SOAP per la rimozione di un elemento dal database del server di report.  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="https://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 SOAP  richiede che i messaggi siano inseriti in un elemento `Envelope` e che il blocco del messaggio sia inserito in un elemento `Body`. In questo esempio il corpo contiene una chiamata al metodo <xref:ReportService2010.ReportingService2010.DeleteItem%2A> che accetta un parametro stringa che rappresenta il percorso dell'elemento da eliminare. È possibile creare una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] classe proxy client che incapsula tutte le operazioni SOAP nei metodi. Il metodo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] seguente rappresenta l'esempio SOAP fornito in precedenza.  
  
```  
public void DeleteItem(string item);  
```  
  
 La risposta dal server può essere simile alla seguente:  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="https://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 Il metodo <xref:ReportService2010.ReportingService2010.DeleteItem%2A> non restituisce alcun valore, pertanto viene restituita una risposta vuota.  
  
## <a name="see-also"></a>Vedi anche  
 [Accesso all'API SOAP](accessing-the-soap-api.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services server di report](../reporting-services-report-server.md)   
 [Servizio Web ReportServer](report-server-web-service.md)  
  
  
