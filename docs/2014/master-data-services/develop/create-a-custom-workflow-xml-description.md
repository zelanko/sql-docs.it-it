---
title: Descrizione XML del flusso di lavoro personalizzato (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: e267e5f4-38bb-466d-82e8-871eabeec07e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a71ee85fc4dce4abd7d8ef91a8f22529ce8d5a0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483010"
---
# <a name="custom-workflow-xml-description-master-data-services"></a>Descrizione XML del flusso di lavoro personalizzato (Master Data Services)
  In [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] il metodo <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> viene chiamato da SQL Server MDS Workflow Integration Service all'avvio di un flusso di lavoro. Questo metodo riceve i metadati e i dati sull'elemento che ha attivato la regola business del flusso di lavoro come blocco di XML. Per un esempio di codice che implementa un gestore del flusso di lavoro, vedere [Creare un flusso di lavoro personalizzato - Esempio &#40;Master Data Services&#41;](create-a-custom-workflow-example.md).  
  
 Nell'esempio seguente viene illustrato il possibile aspetto del codice XML inviato al gestore del flusso di lavoro:  
  
```scr  
<ExternalAction>  
  <Type>TEST</Type>  
  <SendData>1</SendData>  
  <Server_URL>This is my test!</Server_URL>  
  <Action_ID>Test Workflow</Action_ID>  
  <Model_ID>5</Model_ID>  
  <Model_Name>Customer</Model_Name>  
  <Entity_ID>34</Entity_ID>  
  <Entity_Name>Customer</Entity_Name>  
  <Version_ID>8</Version_ID>  
  <MemberType_ID>1</MemberType_ID>  
  <Member_ID>12</Member_ID>  
  <MemberData>  
    <ID>12</ID>  
    <Version_ID>8</Version_ID>  
    <ValidationStatus_ID>3</ValidationStatus_ID>  
    <ChangeTrackingMask>0</ChangeTrackingMask>  
    <EnterDTM>2011-02-25T20:16:36.650</EnterDTM>  
    <EnterUserID>2</EnterUserID>  
    <EnterUserName>MyUserName</EnterUserName>  
    <EnterUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</EnterUserMuid>  
    <EnterVersionId>8</EnterVersionId>  
    <EnterVersionName>VERSION_1</EnterVersionName>  
    <EnterVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</EnterVersionMuid>  
    <LastChgDTM>2011-02-25T20:16:36.650</LastChgDTM>  
    <LastChgUserID>2</LastChgUserID>  
    <LastChgUserName>MyUserName</LastChgUserName>  
    <LastChgUserMuid>EEF91D48-B673-4D83-B95F-5A363C11DE91</LastChgUserMuid>  
    <LastChgVersionId>8</LastChgVersionId>  
    <LastChgVersionName>VERSION_1</LastChgVersionName>  
    <LastChgVersionMuid>52B788C2-2750-4651-9DB0-2CB05A88AA5A</LastChgVersionMuid>  
    <Name>Test Customer</Name>  
    <Code>TC</Code>  
  </MemberData>  
</ExternalAction>  
```  
  
 Nella tabella seguente vengono descritti alcuni dei tag contenuti nel codice XML:  
  
|Tag|Descrizione|  
|---------|-----------------|  
|\<Digitare>|Testo immesso nella casella di testo **Tipo di flusso di lavoro** in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] per identificare l'assembly del flusso di lavoro personalizzato da caricare.|  
|
  \<SendData >|Valore booleano gestito dalla casella di controllo **Includi dati membro nel messaggio** in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]. Il valore 1 indica che la sezione \<MemberData> viene inviata; se il valore non è 1 la sezione \<MemberData> non viene inviata.|  
|<Server_URL>|Testo immesso nella casella di testo **Sito flusso di lavoro** in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|<Action_ID>|Testo immesso nella casella di testo **Nome flusso di lavoro** in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].|  
|
  \<MemberData>|Contiene i dati del membro che ha attivato l'azione del flusso di lavoro. È incluso solo se il valore di \<SendData> è 1.|  
|\<Immettere*xxx*>|Questo set di tag contiene i metadati sulla creazione del membro, ad esempio il momento e l'autore della creazione.|  
|\<LastChg*xxx*>|Questo set di tag contiene i metadati sull'ultima modifica apportata al membro, ad esempio il momento e l'autore dell'esecuzione della modifica.|  
|\<Nome>|Primo attributo del membro modificato. Questo membro di esempio contiene solo gli attributi Name e Code.|  
|\<> di codice|Attributo successivo del membro modificato. Se il membro di esempio contiene più attributi, essi vengono specificati dopo questo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creare un &#40;del flusso di lavoro personalizzato Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)   
 [Esempio di flusso di lavoro personalizzato &#40;Master Data Services&#41;](create-a-custom-workflow-example.md)  
  
  
