---
title: Esecuzione di preparazione aggiornamento (prompt dei comandi) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], running
- command prompt [Upgrade Advisor]
- UpgradeAdvisorWizardCmd utility
- XML formats [Upgrade Advisor]
ms.assetid: 7c83049b-9227-4723-9b7f-66288bc6bd1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 997d637d109c04dbecb3105538f51fa6ece0518f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092434"
---
# <a name="running-upgrade-advisor-command-prompt"></a>Esecuzione di Preparazione aggiornamento (prompt dei comandi)
  Usare la **UpgradeAdvisorWizardCmd** eseguire Preparazione aggiornamento dal prompt dei comandi dell'utilità. È possibile scegliere di ricevere i risultati in formato XML o in un file con valori delimitati da virgole.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      UpgradeAdvisorWizardCmd [ -? ]  |   
    [ -ConfigFilefilename | <server_info> ]  
    [ -SqlUserlogin_id-SqlPasswordpassword ]  
    [ -CSV ]  
  
where <server_info> is any combination of the following:  
        -Serverserver_name-Instanceinstance_name-ASInstanceAS_instance_name-RSInstanceRS_instance_name  
```  
  
## <a name="arguments"></a>Argomenti  
 **-?**  
 Visualizza la sintassi del comando.  
  
 **-ConfigFile** _filename_  
 È il nome del percorso e nome del file di un file XML contenente le impostazioni da usare quando si esegue la **UpgradeAdvisorWizardCmd** utilità.  
  
 *<server_info>*  
 Specifica il computer e l'istanza da analizzare. Utilizzare queste opzioni se non si utilizza un file di configurazione.  
  
 *< server_info >* può essere qualsiasi combinazione dei quattro argomenti seguenti:  
  
 **-Server** _nome_server_  
 Specifica il nome del computer da analizzare, che può essere il computer locale, ovvero il valore predefinito, oppure un computer remoto.  
  
 **-Istanza** _nome_istanza_  
 Specifica il nome dell'istanza da analizzare. Nessun valore predefinito. Se non si specifica questo parametro il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non viene analizzato. Il valore per un'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è MSSQLSERVER. Per un'istanza denominata, utilizzare il nome dell'istanza.  
  
 **-ASInstance**  _AS_instance_name_  
 Specifica il nome dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da analizzare. Nessun valore predefinito. Se non si specifica questo valore, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non viene analizzato. Il valore per un'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è MSSQLServerOLAPService. Per un'istanza denominata, utilizzare il nome dell'istanza.  
  
 **-RSInstance**  _RS_instance_name_  
 Specifica il nome dell'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da analizzare. Nessun valore predefinito. Se non si specifica questo valore, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non viene analizzato. Il valore per un'istanza predefinita di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è ReportServer. Per un'istanza denominata, utilizzare il nome dell'istanza.  
  
 **-SqlUser** _login_id_  
 Se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questo valore corrisponde all'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che verrà utilizzato da Preparazione aggiornamento per stabilire la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se non si specifica un account di accesso, per la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà utilizzata l'autenticazione di Windows.  
  
 **-SqlPassword** _password_  
 Se si usa la **- SqlUser** argomento, usare questo argomento per specificare la password per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.  
  
 **-CSV**  
 Specifica la restituzione dei risultati come valori delimitati da virgole in un file con estensione csv in aggiunta ai risultati XML standard. I risultati vengono scritti i documenti\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cartella Advisor\110\Reports esegue l'aggiornamento.  
  
## <a name="return-values"></a>Valori restituiti  
 Nella tabella seguente mostra i valori **UpgradeAdvisorWizardCmd** restituisce.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|0|Analisi riuscita, nessun problema di aggiornamento rilevato.|  
|numero intero positivo|Analisi riuscita, problemi di aggiornamento rilevati.|  
|numero intero negativo|Analisi non riuscita.|  
  
## <a name="remarks"></a>Note  
 Tutte le informazioni richieste per eseguire l'analisi, ad eccezione dei nomi utente e delle password dell'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], possono essere fornite in un file di configurazione XML. Il file di configurazione XML è documentato nel modello. Se non si utilizza un file di configurazione, è possibile analizzare tutti i componenti installati in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con le impostazioni predefinite specificando i nomi di computer e i nomi di istanza. Per una descrizione delle impostazioni predefinite del file di configurazione, vedere la tabella "Descrizione degli elementi" più avanti in questo argomento.  
  
## <a name="configuration-file-template"></a>Modello di file di configurazione  
 Utilizzare il seguente file XML come modello per la creazione dei file di configurazione. È possibile modificare il modello in base alle esigenze specifiche dell'organizzazione.  
  
```xml  
<Configuration>  
    <Server> </Server>  
    <Instance></Instance>  
    <Components>  
        <SQLServer>  
            <Databases>  
                <Database></Database>  
            </Databases>  
            <TraceFiles>  
                <TraceFile></TraceFile>  
            </TraceFiles>  
            <BatchFiles>  
                <BatchFile></BatchFile>  
            </BatchFiles>  
            <BatchSeparator></BatchSeparator>  
        </SQLServer>  
        <AnalysisServices>  
            <ASInstance></ASInstance>  
            <Databases>  
                <Database></Database>  
            </Databases>  
        </AnalysisServices>  
        <ReportingServices>  
            <RSInstance></RSInstance>  
        </ReportingServices>  
        <IntegrationServices>  
            <PackagePath></PackagePath>  
        </IntegrationServices>  
    </Components>  
</Configuration>  
```  
  
## <a name="element-descriptions"></a>Descrizione degli elementi  
  
|Tag|Definizione|Occorrenza|  
|---------|----------------|----------------|  
|`Configuration`|Elemento padre per il file di configurazione di Preparazione aggiornamento.|Obbligatorio una volta per ogni file di configurazione.|  
|`Server`|Nome del server da analizzare.|Facoltativo una volta per ogni file di configurazione. Il valore predefinito è il computer locale.|  
|`Instance`|Nome dell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] da analizzare.|Facoltativo una volta per ogni file di configurazione. Il valore predefinito è l'istanza predefinita.<br /><br /> Obbligatorio una volta per ogni file di configurazione, se nel server è presente un elemento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un elemento `IntegrationServices`.|  
|`Components`|Contiene elementi che specificano quali componenti analizzare.|Obbligatorio una volta per ogni file di configurazione.|  
|`SQLServer`|Contiene le impostazioni dell'analisi per un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].|Facoltativo una volta per ogni file di configurazione. Se non viene specificato, i database [!INCLUDE[ssDE](../../includes/ssde-md.md)] non verranno analizzati.|  
|Elemento `Databases` per `SQLServer`|Contiene un elenco di database da analizzare.|Facoltativo una volta per ogni elemento di `SQLServer`. Se questo elemento non è presente, verranno analizzati tutti i database dell'istanza.|  
|Elemento `Database` per `SQLServer`|Specifica il nome di un database da analizzare.|Obbligatorio una o più volte se l'elemento `Databases` è presente. Se un elemento `Database` contiene il valore "*", verranno analizzati tutti i database dell'istanza. Nessun valore predefinito.|  
|`TraceFiles`|Contiene un elenco di file di traccia da analizzare.|Facoltativo una volta per ogni elemento di `SQLServer`.|  
|`TraceFile`|Specifica il percorso e il nome di un file di traccia da analizzare.|Obbligatorio una o più volte se l'elemento `TraceFiles` è presente. Nessun valore predefinito.|  
|`BatchFiles`|Contiene un elenco di file batch da analizzare.|Facoltativo una volta per ogni elemento di `SQLServer`.|  
|`BatchFile`|Specifica un file batch da analizzare. Possono essere più di uno.|Obbligatorio una o più volte se l'elemento `BatchFiles` è presente. Nessun valore predefinito.|  
|`BatchSeparator`|Specifica il separatore batch utilizzato nei file batch di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Facoltativo una volta per ogni elemento di `SQLServer`. Il valore predefinito è GO.|  
|`AnalysisServices`|Contiene le impostazioni dell'analisi per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|Facoltativo una volta per ogni file di configurazione. Se non viene specificato, i database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non verranno analizzati.|  
|`ASInstance`|Specifica il nome dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|Obbligatorio una volta per ogni elemento di `AnalysisServices`. Nessun valore predefinito.|  
|Elemento `Databases` per `Analysis Services`|Contiene un elenco di database da analizzare.|Facoltativo una volta per ogni elemento di `AnalysisServices`. Se questo elemento non è presente, verranno analizzati tutti i database dell'istanza.|  
|Elemento `Database` per `AnalysisServices`|Specifica il nome di un database da analizzare.|Obbligatorio una o più volte se l'elemento `Databases` è presente. Se un elemento `Database` contiene il valore "*", verranno analizzati tutti i database dell'istanza. Nessun valore predefinito.|  
|`ReportingServices`|Specifica di eseguire l'analisi su [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Facoltativo una volta per ogni file di configurazione. Se non viene specificato, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non viene analizzato.|  
|`RSInstance`|Specifica il nome dell'istanza di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Obbligatorio una volta per ogni elemento di `ReportingServices`. Nessun valore predefinito.|  
|`IntegrationServices`|Contiene le impostazioni di analisi per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|Facoltativo una volta per ogni file di configurazione. Se non viene specificato, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non viene analizzato.|  
|`PackagePath`|Specifica il percorso di un set di pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|Facoltativo una volta per ogni elemento di `IntegrationServices`. Se questo elemento non è presente, l'analisi verrà effettuata sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mentre i pacchetti archiviati esternamente non verranno analizzati. Nessun valore predefinito.|  
  
## <a name="examples"></a>Esempi  
  
### <a name="a-run-upgrade-advisor-using-a-configuration-file"></a>A. Eseguire Preparazione aggiornamento utilizzando un file di configurazione  
 Nell'esempio seguente viene illustrato come eseguire Preparazione aggiornamento dal prompt dei comandi utilizzando un file di configurazione in cui vengono specificati i componenti da analizzare. In questo esempio viene utilizzata l'autenticazione di Windows per la connessione a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"  
```  
  
### <a name="b-run-upgrade-advisor-using-default-configuration-settings"></a>B. Eseguire Preparazione aggiornamento utilizzando le impostazioni di configurazione predefinite  
 Nell'esempio seguente viene illustrato come eseguire Preparazione aggiornamento dal prompt dei comandi utilizzando le impostazioni di configurazione predefinite e l'autenticazione di Windows.  
  
```  
UpgradeAdvisorWizardCmd -Server MyServer -Instance MyInst   
```  
  
### <a name="c-run-upgrade-advisor-using-includessnoversionincludesssnoversion-mdmd-authentication"></a>C. Eseguire Preparazione aggiornamento utilizzando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nell'esempio seguente viene illustrato come eseguire Preparazione aggiornamento dal prompt dei comandi utilizzando un file di configurazione. Vengono specificati un nome utente e una password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per eseguire la connessione all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"   
    -SqlUser "MyUserName" -SqlPassword "QweRTy-55"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Risoluzione dei problemi di aggiornamento](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Utilizzo di preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Esecuzione di preparazione aggiornamento a &#40;interfaccia utente&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)  
  
  
