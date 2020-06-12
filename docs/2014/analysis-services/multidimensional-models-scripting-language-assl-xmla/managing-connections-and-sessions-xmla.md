---
title: Gestione di connessioni e sessioni (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- statefulness [XML for Analysis]
- statelessness [XML for Analysis]
- XML for Analysis, sessions
- states [XML for Analysis]
- XMLA, sessions
- sessions [XML for Analysis]
ms.assetid: b83bb3ff-09be-4fda-9d1d-6248e04ffb21
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7bfe876f6874193fd0885f16d91caa9f6fe8b172
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544943"
---
# <a name="managing-connections-and-sessions-xmla"></a>Gestione di connessioni e sessioni (XMLA)
  *Informazioni sullo stato* è una condizione durante la quale il server conserva l'identità e il contesto di un client tra le chiamate al metodo. L' *assenza* di stato è una condizione durante la quale il server non memorizza l'identità e il contesto di un client al termine di una chiamata al metodo.  
  
 Per fornire informazioni sullo stato, XML for Analysis (XMLA) supporta le *sessioni* che consentono di eseguire insieme una serie di istruzioni. Un esempio di tale serie di istruzioni potrebbe essere la creazione di un membro calcolato da utilizzare in query successive.  
  
 In genere le sessioni in XMLA si comportano nel modo indicato dalla specifica OLE DB 2.6 e descritto di seguito:  
  
-   Le sessioni definiscono l'ambito del contesto dei comandi e delle transazioni.  
  
-   È possibile eseguire più comandi nel contesto di una singola sessione.  
  
-   Il supporto per le transazioni nel contesto XMLA è tramite comandi specifici del provider inviati con il metodo [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
 XMLA definisce una modalità per supportare sessioni in un ambiente Web in modo analogo all'approccio utilizzato dal protocollo DAV (Distributed Authoring and Versioning) per implementare il blocco in un ambiente a regime di controllo libero. L'analogia con il protocollo DAV consiste nel fatto che è consentita la scadenza delle sessioni nel provider per diversi motivi, ad esempio se si verifica un timeout o un errore di connessione. Quando le sessioni sono supportate, i servizi Web devono essere consapevoli e pronti per gestire di set interrotti di comandi che devono essere riavviati.  
  
 La specifica SOAP (Simple Object Access Protocol ) definita dal World Wide Web Consortium (W3C) consiglia l'utilizzo di intestazioni SOAP per la compilazione di nuovi protocolli nella parte superiore dei messaggi SOAP. Nella tabella seguente vengono elencati gli elementi dell'intestazione SOAP e gli attributi che XMLA definisce per avviare, gestire e chiudere una sessione.  
  
|Intestazione SOAP|Descrizione|  
|-----------------|-----------------|  
|BeginSession|Questa intestazione richiede al provider di creare una nuova sessione. Il provider deve rispondere costruendo una nuova sessione e restituendo l'ID di sessione come parte dell'intestazione Session nella risposta SOAP.|  
|SessionId|Area del valore che contiene l'ID di sessione da utilizzare in ogni chiamata al metodo per il resto della sessione. Nella risposta SOAP il provider invia questo tag, che deve essere inviato inoltre anche dal client con ogni elemento dell'intestazione Session.|  
|Sessione|Per ogni chiamata al metodo che si verifica nella sessione, questa intestazione deve essere utilizzata e l'ID di sessione deve essere incluso nell'area del valore dell'intestazione.|  
|EndSession|Per terminare la sessione, utilizzare questa intestazione. L'ID di sessione deve essere incluso con l'area del valore.|  
  
> [!NOTE]  
>  Un ID di sessione non garantisce che una sessione rimanga valida. Se la sessione scade (ad esempio se si verifica un timeout o se la connessione si interrompe), il provider può scegliere di terminare le azioni di tale sessione e di eseguirne il rollback. Di conseguenza, tutte le chiamate al metodo successive eseguite dal client su un ID di sessione avranno esito negativo e restituiranno un errore che indica che la sessione non è valida. Un client deve gestire questa condizione e deve essere preparato per inviare nuovamente le chiamate al metodo della sessione a partire dall'inizio.  
  
## <a name="legacy-code-example"></a>Codice di esempio legacy  
 Nell'esempio seguente viene illustrato come sono supportate le sessioni.  
  
1.  Per avviare la sessione, aggiungere un'intestazione BeginSession in SOAP alla chiamata al metodo XMLA in uscita dal client. L'area del valore è inizialmente vuota perché l'ID di sessione non è ancora noto.  
  
    ```  
    <SOAP-ENV:Envelope  
       xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
       SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
       <SOAP-ENV:Header>  
          <XA:BeginSession  
             xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
             xsi:type="xsd:int"  
             mustUnderstand="1"/>  
       </SOAP-ENV:Header>  
       <SOAP-ENV:Body>  
          ...<!-- Discover or Execute call goes here.-->  
       </SOAP-ENV:Body>  
    </SOAP-ENV:Envelope>  
    ```  
  
2.  Il messaggio di risposta SOAP del provider include l'ID sessione nell'area dell'intestazione restituita, utilizzando il tag di intestazione XMLA \<SessionId> .  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
3.  Per ogni chiamata al metodo nella sessione, l'intestazione Session deve essere aggiunta e deve contenere l'ID di sessione restituito dal provider.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:Session  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
4.  Al termine della sessione, \<EndSession> viene usato il tag, che contiene il valore dell'ID di sessione correlato.  
  
    ```  
    <SOAP-ENV:Header>  
       <XA:EndSession  
          xmlns:XA="urn:schemas-microsoft-com:xml-analysis"  
          xsi:type="xsd:int"  
          mustUnderstand="1"  
          SessionId="581"/>  
    </SOAP-ENV:Header>  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
