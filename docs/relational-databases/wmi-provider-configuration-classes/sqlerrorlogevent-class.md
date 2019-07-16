---
title: Classe SqlErrorLogEvent | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e36d05c39fb3bc4fc19d2ea0c28def7cd626fbf1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052520"
---
# <a name="sqlerrorlogevent-class"></a>Classe SqlErrorLogEvent
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Fornisce proprietà per la visualizzazione di eventi in un file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>Proprietà  
 Classe SQLErrorLogEvent definisce le proprietà seguenti.  
  
|||  
|-|-|  
|FileName|Tipo di dati: **stringa**<br /><br /> Tipo di accesso: Sola lettura<br /><br /> <br /><br /> Nome del file di log degli errori.|  
|InstanceName|Tipo di dati: **stringa**<br /><br /> Tipo di accesso: Sola lettura<br /><br /> Qualificatori: Chiave<br /><br /> Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si trova il file di log.|  
|LogDate|Tipo di dati: **datetime**<br /><br /> Tipo di accesso: Sola lettura<br /><br /> Qualificatori: Chiave<br /><br /> <br /><br /> Data e ora della registrazione dell'evento nel file di log.|  
|`Message`|Tipo di dati: **stringa**<br /><br /> Tipo di accesso: Sola lettura<br /><br /> <br /><br /> Messaggio di evento.|  
|Classe ProcessInfo|Tipo di dati: **stringa**<br /><br /> Tipo di accesso: Sola lettura<br /><br /> <br /><br /> Informazioni sull'ID del processo server di origine (SPID) per l'evento.|  
  
## <a name="remarks"></a>Note  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Spazio dei nomi|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come recuperare valori per tutti gli eventi registrati in un file di log specificato. Per eseguire l'esempio, sostituire \< *nome_istanza*> con il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio "Istanza1" e sostituire "File_Name" con il nome del file di log degli errori, ad esempio "ERRORLOG.1".  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>Commenti  
 Quando *InstanceName* oppure *FileName* non disponibili nell'istruzione WQL, la query restituirà le informazioni per l'istanza predefinita e corrente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di log. Ad esempio, l'istruzione WQL seguente restituisce tutti gli eventi di log del file di log corrente (ERRORLOG) nell'istanza predefinita (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Sicurezza  
 Per connettersi a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di log tramite WMI, è necessario disporre delle autorizzazioni seguenti in entrambi i computer locali e remoti:  
  
-   Accesso in lettura per il **Root\Microsoft\SqlServer\ComputerManagement10** dello spazio dei nomi WMI. Per impostazione predefinita, chiunque dispone di accesso in lettura tramite l'autorizzazione Abilita account.  
  
-   Autorizzazione di lettura per la cartella che contiene i log degli errori. Per impostazione predefinita l'errore log si trovano nel percorso seguente (dove \< *unità >* rappresenta l'unità in cui è installato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e \< *NomeIstanza*> è il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Unità >: \Programmi\Microsoft SQL Server\MSSQL13** **.\< NomeIstanza > \mssql\log.**  
  
 Se si sta eseguendo la connessione attraverso un firewall, assicurarsi che sia impostata un'eccezione nel firewall per WMI nei computer di destinazione remoti. Per altre informazioni, vedere [la connessione a WMI in modalità remota a partire da Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Vedere anche  
 [Classe SqlErrorLogFile](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
