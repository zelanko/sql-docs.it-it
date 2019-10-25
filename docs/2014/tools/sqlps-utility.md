---
title: Utilità sqlps | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ff96b99ee7982be89126e79687dbc8a2215f42f
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798141"
---
# <a name="sqlps-utility"></a>sqlps - utilità
  Tramite l'utilità `sqlps` viene avviata una sessione di Windows PowerShell 2.0 con il provider PowerShell per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e i cmdlet caricati e registrati. È possibile immettere comandi o script di PowerShell che utilizzano componenti di PowerShell per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per utilizzare istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e i relativi oggetti.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] Utilizzare invece il modulo di PowerShell `sqlps`. Per ulteriori informazioni sul modulo `sqlps`, vedere [importare il modulo sqlps](../database-engine/import-the-sqlps-module.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>Argomenti  
 **-NoLogo**  
 Specifica che l'utilità `sqlps` deve nascondere le informazioni sul copyright all'avvio.  
  
 **-NoExit**  
 Specifica che l'esecuzione dell'utilità `sqlps` deve proseguire una volta completati i comandi di avvio.  
  
 **-NoProfile**  
 Specifica che l'utilità `sqlps` non deve caricare un profilo utente. I profili utente registrano alias, funzioni e variabili di uso comune per l'utilizzo nelle sessioni di PowerShell.  
  
 **-OutPutFormat** { **Text** | **XML** }  
 Specifica che l'output dell'utilità di `sqlps` deve essere formattato come stringhe di testo (**testo**) o in un formato CLIXML serializzato (**XML**).  
  
 **-InPutFormat** { **Text** | **XML** }  
 Specifica che l'input per l'utilità `sqlps` è formattato come stringhe di testo (**testo**) o in un formato CLIXML serializzato (**XML**).  
  
 **-Command**  
 Specifica il comando per l'esecuzione dell'utilità `sqlps`. L'utilità `sqlps` esegue il comando e quindi viene chiusa, a meno che non venga specificato anche **-NoExit** . Non specificare altre opzioni dopo **-Command**, in quanto verranno lette come parametri del comando.  
  
 **-**  
 **-Command-** specifica che l'utilità `sqlps` legge l'input dall'input standard.  
  
 *script_block* [ **-args**_argument_array_ ]  
 Specifica un blocco di comandi di PowerShell da eseguire. Il blocco deve essere incluso tra parentesi graffe: {}. *Script_block* può essere specificato solo quando l'utilità `sqlps` viene chiamata da **PowerShell** o da un'altra `sqlps` sessione di utilità. *argument_array* è una matrice di variabili PowerShell che contiene gli argomenti per i comandi di PowerShell in *script_block*.  
  
 *string* [ *command_parameters* ]  
 Specifica una stringa che contiene i comandi di PowerShell da eseguire. Usare il formato **"& {*`command`*}"**. Le virgolette indicano una stringa e l'operatore Invoke (&) fa sì che l'utilità `sqlps` esegua il comando.  
  
 [ **-?** | **-Help** ]  
 Visualizza il riepilogo della sintassi delle opzioni dell'utilità `sqlps`.  
  
## <a name="remarks"></a>Remarks  
 L'utilità `sqlps` avvia l'ambiente PowerShell (PowerShell. exe) e carica il modulo PowerShell di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Il modulo, denominato anche `sqlps`, carica e registra questi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] snap-in PowerShell:  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     Implementa il provider PowerShell per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e i cmdlet associati, ad esempio **Encode-SqlName** e **Decode-SqlName**.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     Implementa i cmdlet **Invoke-Sqlcmd** e **Invoke-PolicyEvaluation** .  
  
 È possibile utilizzare l'utilità `sqlps` per effettuare le operazioni seguenti:  
  
-   Eseguire in modo interattivo comandi di PowerShell.  
  
-   Eseguire file script di PowerShell.  
  
-   Eseguire cmdlet di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Utilizzare i percorsi del provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per spostarsi nella gerarchia degli oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Per impostazione predefinita, l'utilità `sqlps` viene eseguita con i criteri di esecuzione degli script impostati su **Restricted**. Questa impostazione impedisce l'esecuzione di qualsiasi script di PowerShell. Per abilitare l'esecuzione di script firmati o di qualsiasi script, è possibile usare il cmdlet **Set-ExecutionPolicy** . Eseguire solo script provenienti da origini attendibili e proteggere tutti i file di input e di output utilizzando le autorizzazioni NTFS appropriate. Per ulteriori informazioni sull'abilitazione degli script di PowerShell, vedere la pagina relativa all' [esecuzione di script di Windows PowerShell](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/).  
  
 La versione dell'utilità `sqlps` in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] viene implementata come minishell di Windows PowerShell 1.0. Alle minishell si applicano alcune restrizioni, ad esempio agli utenti non è consentito caricare snap-in diversi da quelli caricati dalla minishell. Queste restrizioni non si applicano a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e versioni successive dell'utilità, modificate per utilizzare il modulo `sqlps`.  
  
## <a name="examples"></a>Esempi  

### <a name="a-run-the-sqlps-utility-in-default-interactive-mode-without-the-copyright-banner"></a>A. Eseguire l'utilità sqlps in modalità interattiva predefinita senza le informazioni sul copyright
  
```cmd
sqlps -NoLogo  
```  
  
### <a name="b-run-a-sql-server-powershell-script-from-the-command-prompt"></a>b. Esecuzione di uno script di PowerShell per SQL Server dal prompt dei comandi
  
```cmd
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
### <a name="c-run-a-sql-server-powershell-script-from-the-command-prompt-and-keep-running-after-the-script-completes"></a>C. Esecuzione di uno script di PowerShell per SQL Server dal prompt dei comandi e proseguimento dell'esecuzione al termine dell'esecuzione dello script
  
```cmd
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Abilitare o disabilitare un protocollo di rete del server](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
