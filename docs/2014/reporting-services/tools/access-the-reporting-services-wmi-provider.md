---
title: Accedere al provider WMI per Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services]
- programming [Reporting Services]
ms.assetid: 22cfbeb8-4ea3-4182-8f54-3341c771e87b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efbe03a4aab65f792b352eeb5b6c5130c4c32335
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783210"
---
# <a name="access-the-reporting-services-wmi-provider"></a>Accedere al provider WMI per Reporting Services
  Nel provider WMI per Reporting Services sono esposte due classi WMI per l'amministrazione di istanze del server di report in modalità nativa tramite scripting:  
  
> [!IMPORTANT]  
>  A partire dalla versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , il provider WMI è supportato solo per server di report in modalità nativa. I server di report in modalità SharePoint possono essere gestiti con pagine di Amministrazione centrale SharePoint e script di PowerShell.  
  
|Classe|Spazio dei nomi|Descrizione|  
|-----------|---------------|-----------------|  
|MSReportServer_Instance|root\Microsoft\SqlServer\ReportServer\ RS_*\<nomeistanzacodificato>* \v11|Fornisce le informazioni di base necessarie affinché un client si connetta a un server di report installato.|  
|MSReportServer_ConfigurationSetting|root\Microsoft\SqlServer\ReportServer\ RS_*\<nomeistanzacodificato>* \v11\Admin|Rappresenta i parametri di installazione e di runtime di un'istanza del server di report. Tali parametri sono archiviati nel file di configurazione per il server di report.<br /><br /> **\*\* Importante \*\*** Questa classe è accessibile solo con privilegi amministrativi.|  
  
 Per ogni istanza del server di report viene creata un'istanza di ognuna delle classi sopra indicate. È possibile utilizzare qualsiasi strumento Microsoft o di terze parti per accedere agli oggetti WMI esposti dal server di report, incluse le interfacce di programmazione WMI esposte da .NET Framework stesso. Questo argomento descrive come accedere e usare le istanze della classe WMI con il comando PowerShell [Get-WmiObject](https://technet.microsoft.com/library/dd315295.aspx).  
  
## <a name="determine-the-instance-name-in-the-namespace-string"></a>Determinare il nome dell'istanza nella stringa dello spazio dei nomi  
 Il nome dell'istanza nel percorso dello spazio dei nomi per le classi WMI per Reporting Services è una codifica dei nomi di istanze che vengono specificati durante l'installazione delle istanze denominate di Reporting Services; ovvero, vengono codificati i caratteri speciali nei nomi delle istanze. Ad esempio, un carattere di sottolineatura (_) è codificato come "_5f", pertanto un nome di istanza "My_Instance" è codificato come "My_5fInstance" nel percorso dello spazio dei nomi WMI.  
  
 Per elencare i nomi codificati delle istanze del server di report nel percorso dello spazio dei nomi WMI, utilizzare il comando PowerShell seguente:  
  
```powershell
Get-WmiObject -Namespace root\Microsoft\SqlServer\ReportServer -Class __Namespace -ComputerName hostname | Select Name  
```  
  
## <a name="access-the-wmi-classes-using-powershell"></a>Accedere alle classi WMI utilizzando PowerShell  
 Per accedere alle classi WMI, eseguire il comando riportato di seguito:  
  
```powershell
Get-WmiObject -Namespace <namespacename> -Class <classname> -ComputerName <hostname>  
```  
  
 Ad esempio, per accedere alla classe MSReportServer_ConfigurationSetting nell'istanza del server di report predefinita dell'host myrshost, eseguire il comando riportato di seguito. L'istanza del server di report predefinita deve essere installata in myrshost affinché questo comando possa essere eseguito.  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERER\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost  
```  
  
 Tutti i valori e nomi di proprietà delle classi vengono restituiti dalla sintassi di questo comando. Si noti che vengono restituite tutte le istanze della classe MSReportServer_ConfigurationSetting, anche se si accede alla classe nello spazio dei nomi dell'istanza del server di report predefinita (RS_MSSQLSERVER). Ad esempio, se myrshost è installata con l'istanza del server di report predefinita e con un'istanza del server di report denominata SharePoint, tramite questo comando verranno restituiti due oggetti WMI, i nomi di proprietà e i valori di entrambe le istanze del server di report.  
  
 Per restituire un'istanza specifica della classe quando vengono restituite più istanze, usare il parametro -Filter per filtrare i risultati in base alle proprietà con valori univoci quale InstanceName. Ad esempio, per restituire solo l'oggetto WMI per l'istanza del server di report predefinita, utilizzare il comando riportato di seguito:  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost -Filter "InstanceName='MSSQLSERVER'"  
```  
  
## <a name="query-the-available-methods-and-properties"></a>Eseguire una query sui metodi e sulle proprietà disponibili  
 Per visualizzare i metodi e le proprietà disponibili in una delle classi WMI per Reporting Services, inviare i risultati da Get-WmiObject al comando Get-Member. Ad esempio:  
  
```powershell
Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost | Get-Member  
```  
  
 Per la documentazione sulle proprietà e sui metodi delle classi WMI Reporting Services, vedere....  
  
## <a name="use-a-wmi-method-or-property"></a>Utilizzare un metodo o una proprietà WMI  
 Una volta che si dispone degli oggetti WMI nelle classi di Reporting Services e che si conoscono i metodi e le proprietà disponibili, è possibile utilizzare questi ultimi. Ad esempio, se si dispone di un'istanza del server di report denominata in modalità integrata SharePoint chiamata SHAREPOINT, utilizzare la sequenza dei comandi riportata di seguito per recuperare l'URL per il sito Amministrazione centrale SharePoint:  
  
```powershell
$rsconfig = Get-WmiObject -Namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLServer\v11\Admin" -Class MSReportServer_ConfigurationSetting -ComputerName myrshost -Filter "InstanceName='SHAREPOINT'"  
$rsconfig.GetAdminSiteUrl()  
```  
  
## <a name="see-also"></a>Vedere anche
 [Riferimento della libreria del provider WMI Reporting Services &#40;SSRS&#41;](../wmi-provider-library-reference/reporting-services-wmi-provider-library-reference-ssrs.md)   
 [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md)  
