---
title: Classe SqlErrorLogEvent
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
ms.openlocfilehash: f77b7a36e51d08aa3ae82b5d42e28b0173d750cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73659024"
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
 La classe SQLErrorLogEvent definisce le proprietà seguenti.  
  
|||  
|-|-|  
|FileName|Tipo di dati: **String**<br /><br /> Tipo di accesso: sola lettura<br /><br /> <br /><br /> Nome del file di log degli errori.|  
|InstanceName|Tipo di dati: **String**<br /><br /> Tipo di accesso: sola lettura<br /><br /> Qualificatori: chiave<br /><br /> Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si trova il file di log.|  
|LogDate|Tipo di dati: **DateTime**<br /><br /> Tipo di accesso: sola lettura<br /><br /> Qualificatori: chiave<br /><br /> <br /><br /> Data e ora della registrazione dell'evento nel file di log.|  
|Message|Tipo di dati: **String**<br /><br /> Tipo di accesso: sola lettura<br /><br /> <br /><br /> Il messaggio evento.|  
|ProcessInfo|Tipo di dati: **String**<br /><br /> Tipo di accesso: sola lettura<br /><br /> <br /><br /> Informazioni sull'ID del processo server di origine (SPID) per l'evento.|  
  
## <a name="remarks"></a>Osservazioni  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Spazio dei nomi|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come recuperare valori per tutti gli eventi registrati in un file di log specificato. Per eseguire l'esempio, sostituire \< *Instance_Name*> con il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio "instance1", e sostituire "file_name" con il nome del file di log degli errori, ad esempio "log degli errori. 1".  
  
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
 Quando *NomeIstanza* o *filename* non vengono specificati nell'istruzione WQL, la query restituirà informazioni per l'istanza predefinita e il file di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] log corrente. L'istruzione WQL seguente restituisce, ad esempio, tutti gli eventi di log per il file di log corrente (ERRORLOG) nell'istanza predefinita (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Security  
 Per connettersi a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di log tramite WMI, è necessario disporre delle autorizzazioni seguenti per i computer locali e remoti:  
  
-   Accesso in lettura allo spazio dei nomi WMI **allo root\Microsoft\SqlServer\ComputerManagement10** . Per impostazione predefinita, chiunque dispone di accesso in lettura tramite l'autorizzazione Abilita account.  
  
-   Autorizzazione di lettura per la cartella che contiene i log degli errori. Per impostazione predefinita, i log degli errori si trovano nel percorso seguente, dove \< *unità>* rappresenta l'unità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cui \<è stato installato e *NomeIstanza*> è il nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dell'istanza di:  
  
     **Unità>: \Programmi\Microsoft SQL Server\MSSQL13. \<** **\< Nomeistanza> \MSSQL\Log**  
  
 Se si sta eseguendo la connessione attraverso un firewall, assicurarsi che sia impostata un'eccezione nel firewall per WMI nei computer di destinazione remoti. Per ulteriori informazioni, vedere [connessione a WMI in modalità remota a partire da Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Vedere anche  
 [Classe SqlErrorLogFile](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [Visualizzare file di log offline](../../relational-databases/logs/view-offline-log-files.md)  
  
  
