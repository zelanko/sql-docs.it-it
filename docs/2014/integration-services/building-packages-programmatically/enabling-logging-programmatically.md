---
title: Abilitazione della registrazione a livello di programmazione | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8b83f5842ebb2bb97ebd58142ef69d3a3d153f51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62836493"
---
# <a name="enabling-logging-programmatically"></a>Abilitazione della registrazione a livello di programmazione
  Il motore di runtime include una raccolta di oggetti <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> che consentono l'acquisizione di informazioni specifiche degli eventi durante la convalida e l'esecuzione di pacchetti. Gli oggetti <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> sono disponibili per gli oggetti <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer>, compresi gli oggetti <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, <xref:Microsoft.SqlServer.Dts.Runtime.Package>, <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> e <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>. La registrazione viene abilitata su singoli contenitori o sull'intero pacchetto.  
  
 Sono disponibili diversi tipi di provider di log che un contenitore può utilizzare. In questo modo è possibile creare e archiviare le informazioni del log in modo flessibile in molti formati. Per integrare un oggetto contenitore nella registrazione, sono necessari due passaggi: viene innanzitutto abilitata la registrazione, quindi viene selezionato un provider di log. Le proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> del contenitore vengono utilizzate per specificare gli eventi registrati e per selezionare il provider di log.  
  
## <a name="enabling-logging"></a>Abilitazione della registrazione  
 La proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A>, disponibile in ogni contenitore in grado di eseguire la registrazione, determina se le informazioni degli eventi del contenitore vengono o meno registrate nel log eventi. Questa proprietà, a cui viene assegnato un valore della struttura <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode>, è ereditata dall'elemento padre del contenitore per impostazione predefinita. Se il contenitore è un pacchetto, pertanto non dispone di elemento padre, la proprietà utilizza l'oggetto <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>, che per impostazione predefinita è `Disabled`.  
  
### <a name="selecting-a-log-provider"></a>Selezione di un provider di log  
 Dopo l'impostazione della proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> su `Enabled`, viene aggiunto un provider di log alla raccolta <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> del contenitore per completare il processo. La raccolta <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> è disponibile sull'oggetto <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> e contiene i provider di log selezionati per il contenitore. Il metodo <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> viene chiamato per creare un provider e per aggiungerlo alla raccolta. Il metodo restituisce quindi il provider di log aggiunto alla raccolta. Ogni provider include impostazioni di configurazione specifiche e queste proprietà vengono impostate tramite la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>.  
  
 Nella tabella seguente sono elencati i provider di log disponibili, la relativa descrizione e le informazioni su <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>.  
  
|Provider|Descrizione|Proprietà ConfigString|  
|--------------|-----------------|---------------------------|  
|SQL Server Profiler|Genera tracce SQL che possono essere acquisite e visualizzate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. L'estensione predefinita dei file per questo provider è trc.|Non è richiesta alcuna configurazione.|  
|SQL Server|Scrive le voci del log eventi nella tabella **sysssislog** in qualsiasi database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede che siano specificati la connessione al database e anche il nome del database di destinazione.|  
|File di testo|Scrive le voci del log eventi in file di testo ASCII in formato delimitato da virgole (CSV). L'estensione predefinita dei file per questo provider è log.|Nome di una gestione connessione file.|  
|Registro eventi di Windows|Registra nel registro eventi standard di Windows nel registro applicazioni del computer locale.|Non è richiesta alcuna configurazione.|  
|File XML|Scrive le voci del log eventi in un file in formato XML. L'estensione predefinita dei file per questo provider è xml.|Nome di una gestione connessione file.|  
  
 Gli eventi vengono inclusi o esclusi dal log eventi impostando le proprietà `EventFilterKind` e `EventFilter` del contenitore. La struttura `EventFilterKind` contiene due valori, `ExclusionFilter` e `InclusionFilter`, che indicano se gli eventi aggiunti a `EventFilter` sono inclusi nel log eventi. Alla proprietà `EventFilter` viene quindi assegnata una matrice di stringhe che contiene i nomi degli eventi soggetti all'applicazione di filtri.  
  
 Nel codice seguente viene abilitata la registrazione su un pacchetto, viene aggiunto il provider di log per i file di testo nella raccolta <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> e viene specificato un elenco di eventi da includere nell'output della registrazione.  
  
## <a name="sample"></a>Esempio  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      ConnectionManager loggingConnection = p.Connections.Add("FILE");  
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";  
  
      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");  
      provider.ConfigString = loggingConnection.Name;  
      p.LoggingOptions.SelectedLogProviders.Add(provider);  
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;  
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute",   
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };  
      p.LoggingMode = DTSLoggingMode.Enabled;  
  
      // Add tasks and other objects to the package.  
  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
  
    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")  
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"  
  
    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")  
    provider.ConfigString = loggingConnection.Name  
    p.LoggingOptions.SelectedLogProviders.Add(provider)  
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion  
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _  
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}  
    p.LoggingMode = DTSLoggingMode.Enabled  
  
    ' Add tasks and other objects to the package.  
  
  End Sub  
  
End Module  
```  
  
![Icona di Integration Services (piccola)](../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md)  
  
  
