---
title: Classe SqlErrorLogFile | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c5c6f1998cffc268a57318e0124f74d3411a3b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63249322"
---
# <a name="sqlerrorlogfile-class"></a>Classe SqlErrorLogFile
  Fornisce proprietà per la visualizzazione delle informazioni relative a un file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>Proprietà  
 La classe SQLErrorLogFile definisce le proprietà seguenti.  
  
|||  
|-|-|  
|ArchiveNumber|Tipo di dati: `uint32`<br /><br /> Tipo di accesso: sola lettura<br /><br /> <br /><br /> Numero dell'archivio per il file di log.|  
|InstanceName|Tipo di dati: `string`<br /><br /> Tipo di accesso: sola lettura<br /><br /> Qualificatori: chiave<br /><br /> <br /><br /> Nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si trova il file di log.|  
|LastModified|Tipo di dati: `datetime`<br /><br /> Tipo di accesso: sola lettura<br /><br /> <br /><br /> Data dell'ultima modifica apportata al file di log.|  
|LogFileSize|Tipo di dati: `uint32`<br /><br /> Tipo di accesso: sola lettura<br /><br /> <br /><br /> Dimensione del file di log, in byte.|  
|Nome|Tipo di dati: `string`<br /><br /> Tipo di accesso: sola lettura<br /><br /> Qualificatori: chiave<br /><br /> <br /><br /> Nome del file di log.|  
  
## <a name="remarks"></a>Osservazioni  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Spazio dei nomi|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come recuperare informazioni su tutti i file di log di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per eseguire l'esempio, sostituire \< *Instance_Name*> con il nome dell'istanza, ad esempio, "instance1".  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>Commenti  
 Quando *NomeIstanza* non viene fornito nell'istruzione WQL, la query restituirà informazioni per l'istanza predefinita. L'istruzione WQL seguente restituisce, ad esempio, informazioni su tutti i file di log dall'istanza predefinita (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>Security  
 Per connettersi a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] file di log tramite WMI, è necessario disporre delle autorizzazioni seguenti per i computer locali e remoti:  
  
-   Accesso in lettura allo spazio dei nomi WMI **allo root\Microsoft\SqlServer\ComputerManagement10** . Per impostazione predefinita, chiunque dispone di accesso in lettura tramite l'autorizzazione Abilita account.  
  
    > [!NOTE]  
    >  Per informazioni su come verificare le autorizzazioni WMI, vedere la sezione relativa alla sicurezza nell'argomento [visualizzare i file di log offline](../logs/view-offline-log-files.md).  
  
-   Autorizzazione di lettura per la cartella che contiene i log degli errori. Per impostazione predefinita, i log degli errori si trovano nel percorso seguente, dove \< *unità>* rappresenta l'unità in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cui \<è stato installato e *NomeIstanza*> è il nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]dell'istanza di:  
  
     **Unità>: \Programmi\Microsoft SQL Server\MSSQL11. \<** **\< Nomeistanza> \MSSQL\Log**  
  
 Se si sta eseguendo la connessione attraverso un firewall, assicurarsi che sia impostata un'eccezione nel firewall per WMI nei computer di destinazione remoti. Per ulteriori informazioni, vedere [connessione a WMI in modalità remota a partire da Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Vedere anche  
 [Classe SqlErrorLogEvent](sqlerrorlogevent-class.md)   
 [Visualizzare file di log offline](../logs/view-offline-log-files.md)  
  
  
