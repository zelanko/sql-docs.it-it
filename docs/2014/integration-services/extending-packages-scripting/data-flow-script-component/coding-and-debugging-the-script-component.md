---
title: Codifica e debug del componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fd4153aaaf0fdffe32ce48db872a43cb5dbb84c8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894795"
---
# <a name="coding-and-debugging-the-script-component"></a>Codifica e debug del componente script
  In Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] sono disponibili due modalità per il componente script: progettazione metadati e progettazione codice. Quando si apre l'**Editor trasformazione Script**, per il componente viene attivata la modalità di progettazione metadati, che consente di configurare i metadati e impostare le proprietà del componente. Dopo l'impostazione delle proprietà del componente script e la configurazione di input e output nella modalità di progettazione metadati, è possibile passare alla modalità di progettazione codice per scrivere lo script personalizzato. Per altre informazioni sulla modalità di progettazione metadati e sulla modalità di progettazione codice, vedere [Configurazione del componente script nell'editor corrispondente](configuring-the-script-component-in-the-script-component-editor.md).  
  
## <a name="writing-the-script-in-code-design-mode"></a>Scrittura dello script in modalità di progettazione codice  
  
### <a name="script-component-development-environment"></a>Ambiente di sviluppo del componente script  
 Per scrivere lo script, fare clic su **Modifica script** nella pagina **Script** dell'**Editor trasformazione Script** per aprire l'ambiente IDE di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA). L'IDE di VSTA include tutte le funzionalità standard dell'ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET, come l'editor di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con codifica a colori, la tecnologia IntelliSense e il Visualizzatore oggetti.  
  
 Il codice di script viene scritto in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. Il linguaggio di scripting viene specificato mediante l'impostazione della proprietà **ScriptLanguage** nell'**Editor trasformazione Script**. Per utilizzare un altro linguaggio di programmazione, è possibile sviluppare un assembly personalizzato nel linguaggio desiderato e chiamarne la funzionalità dal codice nel componente script.  
  
 Lo script creato nel componente script viene archiviato nella definizione del pacchetto. Non viene creato un file script separato. Pertanto, l'utilizzo del componente script non ha effetto sulla distribuzione del pacchetto.  
  
> [!NOTE]  
>  Durante la progettazione del pacchetto, il codice di script viene scritto temporaneamente in un file di progetto. Poiché l'archiviazione di informazioni riservate in un file costituisce un potenziale rischio per la sicurezza, è consigliabile non inserire nel codice di script informazioni riservate, ad esempio le password.  
  
 Per impostazione predefinita, `Option Strict` è disabilitato nell'IDE.  
  
### <a name="script-component-project-structure"></a>Struttura di progetto del componente script  
 L'efficacia del componente script consiste nella possibilità di generare codice di infrastruttura in grado di ridurre la quantità di codice da scrivere. Questa funzionalità si basa sul fatto che input e output, con le relative colonne e proprietà, sono fissi e noti in anticipo. Pertanto, qualsiasi modifica successiva apportata ai metadati del componente può invalidare il codice scritto. Questa condizione è causa di errori di compilazione durante l'esecuzione del pacchetto.  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>Elementi e classi del progetto del componente script  
 Quando si passa alla modalità di progettazione codice, nell'IDE di VSTA viene aperto e visualizzato l'elemento del progetto `ScriptMain`. L'elemento del progetto `ScriptMain` contiene la classe `ScriptMain` modificabile che funge da punto di ingresso per lo script e nella quale viene scritto il codice. Gli elementi di codice nella classe variano a seconda del linguaggio di programmazione selezionato per l'attività Script.  
  
 Il progetto di script contiene due elementi del progetto aggiuntivi di sola lettura generati automaticamente:  
  
-   L'elemento del progetto `ComponentWrapper` contiene tre classi:  
  
    -   Classe `UserComponent` che eredita da <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> e contiene i metodi e le proprietà da utilizzare per elaborare i dati e interagire con il pacchetto. La classe `ScriptMain` eredita dalla classe `UserComponent`.  
  
    -   Classe della raccolta `Connections` che contiene riferimenti alle connessioni selezionate nella pagina Gestione connessione dell'Editor trasformazione Script.  
  
    -   Classe `Variables` di raccolta che contiene riferimenti alle variabili immesse nelle proprietà `ReadOnlyVariable` e `ReadWriteVariables` nella pagina **script** di **Editor trasformazione script**.  
  
-   L' `BufferWrapper` elemento del progetto contiene una classe che eredita <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> da per ogni input e output configurato nella pagina **input e** output di **Editor trasformazione script**. Ognuna di queste classi contiene proprietà della funzione di accesso tipizzate corrispondenti alle colonne di input e output configurate e i buffer del flusso di dati contenenti le colonne.  
  
 Per informazioni su come usare questi oggetti, metodi e proprietà, vedere [Informazioni sul modello a oggetti del componente script](understanding-the-script-component-object-model.md). Per informazioni su come usare i metodi e le proprietà di queste classi in un tipo di componente script specifico, vedere la sezione [Ulteriori esempi di componente script](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md). Negli argomenti di esempio vengono inoltre presentati esempi di codice completi.  
  
 Quando si configura il componente di script come trasformazione, nell'elemento del progetto `ScriptMain` è incluso il seguente codice generato automaticamente. Nel modello del codice sono inoltre disponibili una panoramica del componente di script, nonché informazioni aggiuntive su come recuperare e modificare oggetti SSIS, quali variabili, eventi e connessioni.  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>Altri elementi del progetto del componente script  
 Il progetto del componente script può includere elementi diversi dall'elemento `ScriptMain` predefinito. È possibile aggiungere al progetto classi, moduli, file di codice e cartelle ed è possibile utilizzare le cartelle per organizzare gruppi di elementi.  
  
 Tutti gli elementi aggiunti vengono salvati in modo permanente nel pacchetto.  
  
#### <a name="references-in-the-script-component-project"></a>Riferimenti nel progetto del componente script  
 Per aggiungere riferimenti agli assembly gestiti, fare clic con il pulsante destro del mouse sul progetto di attività script in **Esplora progetti** e quindi scegliere **Aggiungi riferimento**. Per altre informazioni, vedere [Riferimenti ad altri assembly nelle soluzioni di scripting](../referencing-other-assemblies-in-scripting-solutions.md).  
  
> [!NOTE]  
>  È possibile visualizzare i riferimenti al progetto nell'ambiente IDE di VSTA in **Visualizzazione classi** o in **Esplora progetti**. Queste finestre possono essere aperte dal menu **Visualizza**. È possibile aggiungere un nuovo riferimento dal menu **Progetto**, da **Esplora progetti** o da **Visualizzazione classi**.  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>Interazione con il pacchetto nel componente script  
 Tramite lo script personalizzato scritto nel componente script è possibile accedere e utilizzare variabili e gestioni connessioni del pacchetto contenitore attraverso funzioni di accesso fortemente tipizzate nelle classi di base generate automaticamente. Tuttavia, è necessario configurare sia le variabili sia le gestioni connessioni prima di passare alla modalità di progettazione codice per renderle disponibili allo script. È inoltre possibile generare eventi ed eseguire registrazioni dal codice del componente script.  
  
 Gli elementi del progetto generati automaticamente nel progetto del componente script forniscono i seguenti oggetti, metodi e proprietà per l'interazione con il pacchetto.  
  
|Funzionalità del pacchetto|Metodo di accesso|  
|---------------------|-------------------|  
|variables|Utilizzare le proprietà delle funzioni di accesso denominate e tipizzate nella classe della raccolta `Variables` nell'elemento del progetto `ComponentWrapper`, esposto tramite la proprietà `Variables` della classe `ScriptMain`.<br /><br /> Il metodo `PreExecute` può accedere unicamente a variabili di sola lettura. Il metodo `PostExecute` può accedere sia a variabili di sola lettura sia a variabili di lettura/scrittura.|  
|Connessioni|Utilizzare le proprietà delle funzioni di accesso denominate e tipizzate nella classe della raccolta `Connections` nell'elemento del progetto `ComponentWrapper`, esposto tramite la proprietà `Connections` della classe `ScriptMain`.|  
|Eventi|Generare <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> eventi tramite la proprietà della `ScriptMain` classe e i metodi **Fire\<X>** dell' <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> interfaccia.|  
|Registrazione|Eseguire la registrazione utilizzando il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> della classe `ScriptMain`.|  
  
## <a name="debugging-the-script-component"></a>Debug del componente script  
 Per eseguire il debug del codice nel componente di script, impostare almeno un punto di interruzione nel codice, quindi chiudere l'IDE di VSTA per eseguire il pacchetto in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Quando l'esecuzione del pacchetto entra nel componente di script, l'IDE di VSTA viene riaperto e visualizza il codice in modalità di sola lettura. Quando l'esecuzione raggiunge il punto di interruzione, è possibile esaminare i valori delle variabili e scorrere il codice rimanente.  
  
> [!NOTE]  
>  Non è possibile eseguire il debug di un componente di script se l'attività viene eseguita nell'ambito di un pacchetto figlio eseguito da un'attività Esegui pacchetto. In tali circostanze, i punti di interruzione impostati all'interno del componente di script del pacchetto figlio verranno ignorati. È possibile eseguire il debug del pacchetto figlio normalmente eseguendolo separatamente.  
  
> [!NOTE]  
>  Quando si esegue il debug di un pacchetto che contiene più componenti di script, il debugger è in grado di elaborarne solo uno. Il sistema può eseguire il debug di un altro componente di script se il debugger termina l'elaborazione, come nel caso di un contenitore Ciclo ForEach o Ciclo For.  
  
 È anche possibile monitorare l'esecuzione del componente di script utilizzando i metodi seguenti:  
  
-   Interrompere l'esecuzione e visualizzare un messaggio modale usando il `MessageBox.Show` metodo nello spazio dei nomi **System. Windows. Forms** . Rimuovere il codice al termine del processo di debug.  
  
-   Generare eventi per messaggi informativi, avvisi ed errori. I metodi FireInformation, FireWarning e FireError visualizzano la descrizione dell'evento nella finestra **Output** di Visual Studio. I metodi FireProgress, Console.Write e Console.WriteLine, tuttavia, non visualizzano alcuna informazione nella finestra **Output**. I messaggi dell'evento FireProgress vengono visualizzati nella scheda **Stato** di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Per altre informazioni, vedere [Generazione di eventi nel componente script](../../data-flow/transformations/script-component.md).  
  
-   Registrare eventi o messaggi definiti dall'utente nei provider di log abilitati. Per altre informazioni, vedere [Registrazione nel componente script](logging-in-the-script-component.md).  
  
 Se si vuole soltanto esaminare l'output di un componente script configurato come origine o trasformazione, senza salvare i dati in una destinazione, è possibile arrestare il flusso di dati con una [trasformazione Conteggio righe](../../data-flow/transformations/row-count-transformation.md) e collegare un visualizzatore dati all'output del componente script. Per informazioni sui visualizzatori dati, vedere [Debug di un flusso di dati](../../troubleshooting/debugging-data-flow.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Per ulteriori informazioni sulla codifica del componente script, vedere gli argomenti seguenti in questa sezione.  
  
 [Informazioni sul modello a oggetti del componente script](understanding-the-script-component-object-model.md)  
 Viene illustrato come utilizzare gli oggetti, i metodi e le proprietà disponibili nel componente script.  
  
 [Riferimenti ad altri assembly nelle soluzioni di scripting](../referencing-other-assemblies-in-scripting-solutions.md)  
 Viene illustrato come fare riferimento agli oggetti della libreria di classi [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] nel componente script.  
  
 [Simulazione di un output degli errori per il componente script](../../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 Viene illustrato come simulare un output degli errori per le righe che generano errori durante l'elaborazione tramite il componente script.  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Intervento del blog, [VSTA setup and configuration troubles for SSIS 2008 and R2 installations](https://go.microsoft.com/fwlink/?LinkId=215661) (Problemi di installazione e configurazione di VSTA per le installazioni SSIS 2008 e R2), in blogs.msdn.com.  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visita la pagina Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione del componente script nell'editor corrispondente](configuring-the-script-component-in-the-script-component-editor.md)  
  
  
