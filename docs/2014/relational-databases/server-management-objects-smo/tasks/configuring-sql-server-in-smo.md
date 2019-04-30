---
title: Configurazione di SQL Server in SMO | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7fc07b0b38a9612159ea8f88c00724340f7b494
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273772"
---
# <a name="configuring-sql-server-in-smo"></a>Configurazione di SQL Server in SMO
  In SMO la <xref:Microsoft.SqlServer.Management.Smo.Information> oggetto, il <xref:Microsoft.SqlServer.Management.Smo.Settings> oggetto, il <xref:Microsoft.SqlServer.Management.Smo.UserOptions> oggetto e il <xref:Microsoft.SqlServer.Management.Smo.Configuration> contenute impostazioni e informazioni per l'istanza di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sono disponibili varie proprietà tramite cui viene descritto il comportamento dell'istanza installata. Le proprietà consentono di descrivere opzioni di avvio, impostazioni predefinite del server, file e directory, informazioni sul sistema e sul processore, prodotto e versioni, informazioni di connessione, opzioni per la memoria, selezioni relative a lingua e regole di confronto e modalità di autenticazione.  
  
## <a name="sql-server-configuration"></a>Configurazione di SQL Server  
 Le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Information> contengono informazioni sull'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ad esempio processore e piattaforma.  
  
 Le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Settings> contengono informazioni sull'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Oltre al profilo di posta e all'account del server, è possibile modificare il file e la directory di database predefiniti. Queste proprietà rimangono valide per la durata della connessione.  
  
 Le proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> contengono informazioni sul comportamento delle connessioni correnti in relazione ad aritmetica, standard ANSI e transazioni.  
  
 È inoltre disponibile un set di opzioni di configurazione rappresentato dall'oggetto <xref:Microsoft.SqlServer.Management.Smo.Configuration>. Contiene un set di proprietà che rappresentano le opzioni che possono essere modificate dalla stored procedure `sp_configure`. Impostazione di opzioni, ad esempio **Priority Boost**, **Recovery Interval** e **Network Packet Size**controllare le prestazioni dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Molte di queste opzioni possono essere modificate dinamicamente, ma in alcuni casi il valore viene prima configurato, quindi modificato al riavvio dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 È presente una proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Configuration> per ogni opzione di configurazione. È possibile modificare l'impostazione di configurazione globale utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>. Molte proprietà hanno valori massimi e minimi, anch'essi archiviati come proprietà <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty>. Queste proprietà richiedono il <xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> metodo per eseguire il commit della modifica all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Tutte le opzioni di configurazione nell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Configuration> devono essere modificate dall'amministratore del sistema.  
  
## <a name="examples"></a>Esempi  
 Per gli esempi di codice seguenti, è necessario selezionare l'ambiente, il modello e il linguaggio di programmazione per la creazione dell'applicazione. Per altre informazioni, vedere [creare un progetto Visual Basic SMO in Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [creare un Visual C#&#35; progetto SMO in Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>Modifica delle opzioni di configurazione di SQL Server in Visual Basic  
 Nell'esempio di codice viene illustrato come aggiornare un'opzione di configurazione in Visual Basic .NET. Vengono inoltre recuperate e visualizzate informazioni relative ai valori massimi e minimi per l'opzione di configurazione specificata. Infine, viene segnalato all'utente se la modifica è stata apportata dinamicamente o se è stata archiviata fino al riavvio dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure2](SMO How to#SMO_VBConfigure2)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>Modifica delle impostazioni di SQL Server in Visual Basic  
 L'esempio di codice vengono visualizzate informazioni relative all'istanza del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nelle <xref:Microsoft.SqlServer.Management.Smo.Information> e <xref:Microsoft.SqlServer.Management.Smo.Settings>che modifica le impostazioni in <xref:Microsoft.SqlServer.Management.Smo.Settings> e <xref:Microsoft.SqlServer.Management.Smo.UserOptions>le proprietà dell'oggetto.  
  
 Nell'esempio l'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> e l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Settings> hanno entrambi un metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. È possibile eseguire i metodi <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> per questi oggetti singolarmente.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBConfigure1](SMO How to#SMO_VBConfigure1)]  -->  
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>Modifica delle impostazioni di SQL Server in Visual C#  
 L'esempio di codice vengono visualizzate informazioni relative all'istanza del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nelle <xref:Microsoft.SqlServer.Management.Smo.Information> e <xref:Microsoft.SqlServer.Management.Smo.Settings>che modifica le impostazioni in <xref:Microsoft.SqlServer.Management.Smo.Settings> e <xref:Microsoft.SqlServer.Management.Smo.UserOptions>le proprietà dell'oggetto.  
  
 Nell'esempio l'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> e l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Settings> hanno entrambi un metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. È possibile eseguire i metodi <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> per questi oggetti singolarmente.  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```  
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>Modifica delle impostazioni di SQL Server in PowerShell  
 L'esempio di codice vengono visualizzate informazioni relative all'istanza del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nelle <xref:Microsoft.SqlServer.Management.Smo.Information> e <xref:Microsoft.SqlServer.Management.Smo.Settings>che modifica le impostazioni in <xref:Microsoft.SqlServer.Management.Smo.Settings> e <xref:Microsoft.SqlServer.Management.Smo.UserOptions>le proprietà dell'oggetto.  
  
 Nell'esempio l'oggetto <xref:Microsoft.SqlServer.Management.Smo.UserOptions> e l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Settings> hanno entrambi un metodo <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A>. È possibile eseguire i metodi <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> per questi oggetti singolarmente.  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>Modifica delle opzioni di configurazione di SQL Server in PowerShell  
 Nell'esempio di codice viene illustrato come aggiornare un'opzione di configurazione in Visual Basic .NET. Vengono inoltre recuperate e visualizzate informazioni relative ai valori massimi e minimi per l'opzione di configurazione specificata. Infine, viene segnalato all'utente se la modifica è stata apportata dinamicamente o se è stata archiviata fino al riavvio dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
```  
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = get-item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {    
   "Configuration option has been updated."  
 }  
Else  
{  
    "Configuration option will be updated when SQL Server is restarted."  
}  
```  
  
  
