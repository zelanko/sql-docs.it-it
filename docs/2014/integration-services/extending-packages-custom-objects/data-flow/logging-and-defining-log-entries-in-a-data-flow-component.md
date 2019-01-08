---
title: Registrazione e definizione di voci di log in un componente flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 99eff9181699ed08c7293e2dddf98d5aca2777c6
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358264"
---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>Registrazione e definizione di voci di log in un componente del flusso di dati
  I componenti personalizzati del flusso di dati possono inserire messaggi in una voce di log esistente tramite il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> dell'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. Possono inoltre presentare informazioni all'utente tramite il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> o metodi simili dell'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. Tuttavia, questo approccio genera l'overhead della generazione e gestione di eventi aggiuntivi e forza l'utente a esaminare numerosi messaggi informativi dettagliati alla ricerca di quelli che potrebbero interessarlo. È possibile utilizzare una voce di log personalizzata, come descritto di seguito, per fornire informazioni di log personalizzate con etichette distinte agli utenti del componente.  
  
## <a name="registering-and-using-a-custom-log-entry"></a>Registrazione e utilizzo di una voce di log personalizzata  
  
### <a name="registering-a-custom-log-entry"></a>Registrazione di una voce di log personalizzata  
 Per registrare una voce di log personalizzata per il componente, eseguire l'override del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> della classe di base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Nell'esempio seguente viene registrata una voce di log personalizzata e vengono forniti un nome e una descrizione.  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 L'enumerazione <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> fornisce un hint al runtime sulla frequenza con cui verrà registrato l'evento:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>: Evento viene registrato solo in alcuni casi, non durante ogni esecuzione.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>: Evento viene registrato un numero costante di volte in cui durante ogni esecuzione.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>: Evento viene registrato un numero di volte proporzionale alla quantità di lavoro completato.  
  
 Negli esempi precedenti viene utilizzato <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT> perché il componente si aspetta di registrare una voce una volta ogni esecuzione.  
  
 Dopo la registrazione della voce di log personalizzata e l'aggiunta di un'istanza del componente personalizzato nell'area di progettazione del flusso di dati, nella finestra di dialogo **Registrazione** della finestra di progettazione viene visualizzata una nuova voce di log denominata "My Custom Component Log Entry" nell'elenco di voci di log disponibili.  
  
### <a name="logging-to-a-custom-log-entry"></a>Registrazione in una voce di log personalizzata  
 Dopo la registrazione della voce di log personalizzata, il componente può registrare messaggi personalizzati. Nell'esempio seguente viene scritta una voce di log personalizzata durante il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> che contiene il testo di un'istruzione SQL utilizzata dal componente.  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 A questo punto, quando l'utente esegue il pacchetto, dopo la selezione di "My Custom Component Log Entry" nella finestra di dialogo **Registrazione**, il log conterrà una voce chiaramente identificata come "User::My Custom Component Log Entry". Questa nuova voce di log contiene il testo dell'istruzione SQL, il timestamp ed eventuali altri dati registrati dallo sviluppatore.  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](../../performance/integration-services-ssis-logging.md)  
  
  
