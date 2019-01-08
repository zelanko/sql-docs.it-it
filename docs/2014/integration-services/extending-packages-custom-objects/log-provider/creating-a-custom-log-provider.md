---
title: Creazione di un provider di log personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom log providers [Integration Services], creating
ms.assetid: fc20af96-9eb8-4195-8d3f-8a4d7c753f24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d4a61a20dacbe24551459253f3721f9af9c96a2
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356704"
---
# <a name="creating-a-custom-log-provider"></a>Creazione di un provider di log personalizzato
  L'ambiente di runtime di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] include funzionalità estese di registrazione. Un log consente di acquisire gli eventi che si verificano durante l'esecuzione di pacchetti. In [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] è inclusa una varietà di provider di log che consentono di creare e archiviare log in più formati quali XML, testo, database o nel registro eventi di Windows. Se uno di questi provider o formati di output non soddisfano specifiche esigenze, è possibile creare un provider di log personalizzato.  
  
 I passaggi per la creazione di un provider di log personalizzato sono simili a quelli richiesti per la creazione di qualsiasi altro oggetto personalizzato per [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]:  
  
-   Creare una nuova classe che eredita dalla classe di base. Per un provider di log, la classe di base è <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>.  
  
-   Applicare alla classe l'attributo che identifica il tipo di oggetto. Per un provider di log, l'attributo è <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>.  
  
-   Eseguire l'override dell'implementazione dei metodi e delle proprietà della classe di base. Per un provider di log, questi includono la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> e i metodi <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> e <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>.  
  
-   Le interfacce utente personalizzate per i provider di log personalizzati non sono implementate in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="getting-started-with-a-custom-log-provider"></a>Introduzione ai provider di log personalizzati  
  
### <a name="creating-projects-and-classes"></a>Creazione di progetti e classi  
 Poiché tutti i provider di log gestiti derivano dalla classe di base <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>, il primo passaggio da completare quando si crea un provider di log personalizzato consiste nel creare un progetto di libreria di classi nel linguaggio di programmazione gestito preferito e creare una classe che eredita dalla classe di base. In questa classe derivata si eseguirà l'override dei metodi e delle proprietà della classe di base per implementare la funzionalità personalizzata.  
  
 Configurare il progetto per firmare l'assembly che verrà generato utilizzando un file di chiave con nome sicuro.  
  
> [!NOTE]  
>  Molti provider di log di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] hanno un'interfaccia utente personalizzata che implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e sostituisce la casella di testo **Configurazione** nella finestra di dialogo **Configura log SSIS** con un elenco a discesa filtrato di gestioni connessioni disponibili. Tuttavia, le interfacce utente personalizzate per i provider di log personalizzati non sono implementate in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
### <a name="applying-the-dtslogprovider-attribute"></a>Applicazione dell'attributo DtsLogProvider  
 Applicare l'attributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> alla classe creata per identificarla come provider di log. Questo attributo fornisce informazioni in fase di progettazione, ad esempio il nome e la descrizione del provider di log. Il `DisplayName` e `Description` proprietà dell'attributo corrispondono al **nome** e `Description` le colonne visualizzate nel **Configura log SSIS** editor, che viene visualizzato quando configurazione della registrazione per un pacchetto in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
> [!IMPORTANT]  
>  La proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.LogProviderType%2A> dell'attributo non viene utilizzata. È tuttavia necessario immettere un valore per tale proprietà, altrimenti il provider di log personalizzato non verrà visualizzato nell'elenco di provider di log disponibili.  
  
> [!NOTE]  
>  Poiché le interfacce utente personalizzate per i provider di log personalizzati non vengono implementate in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], l'impostazione di un valore per la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> di <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> non ha alcun effetto.  
  
```vb  
<DtsLogProvider(DisplayName:="MyLogProvider", Description:="A simple log provider.", LogProviderType:="Custom")> _  
Public Class MyLogProvider  
     Inherits LogProviderBase  
    ' TODO: Override the base class methods.  
End Class  
```  
  
```csharp  
[DtsLogProvider(DisplayName="MyLogProvider", Description="A simple log provider.", LogProviderType="Custom")]  
public class MyLogProvider : LogProviderBase  
{  
    // TODO: Override the base class methods.  
}  
```  
  
## <a name="building-deploying-and-debugging-a-custom-log-provider"></a>Compilazione, distribuzione e debug di un provider di log personalizzato  
 I passaggi per la compilazione, la distribuzione e il debug di un provider di log personalizzato in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sono molto simili a quelli richiesti per altri tipi di oggetti personalizzati. Per altre informazioni, vedere [Compilazione, distribuzione e debug di oggetti personalizzati](../building-deploying-and-debugging-custom-objects.md).  
  
![Icona di Integration Services (piccola)](../../media/dts-16.gif "icona di Integration Services (piccola)")**rimangono fino a Date con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina di Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Scrittura del codice di un provider di log personalizzato](coding-a-custom-log-provider.md)   
 [Sviluppo di un'interfaccia utente per un provider di log personalizzato](developing-a-user-interface-for-a-custom-log-provider.md)  
  
  
