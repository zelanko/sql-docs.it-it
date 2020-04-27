---
title: Utilità rsconfig (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b78691b0300b6098dfa88c35b4b61c7aa63fed4a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099814"
---
# <a name="rsconfig-utility-ssrs"></a>utilità rsconfig (SSRS)
  L'utilità **rsconfig** consente di crittografare e archiviare i valori relativi alle connessioni e agli account nel file RSReportServer.config. I valori crittografati includono le informazioni sulla connessione al database del server di report e i valori relativi agli account utilizzati per l'elaborazione automatica dei report.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      rsconfig {-?}  
{-cconnection}  
{-eunattendedaccount}  
{-mcomputername}  
{-iinstancename}  
{-sservername}  
{-ddatabasename}  
{-aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Facoltativo/obbligatorio|Definizione|  
|----------|------------------------|----------------|  
|**-?**|Facoltativa.|Visualizza la sintassi degli argomenti di Rsconfig.exe.|  
|`-c`|Obbligatorio se non si specifica l'argomento `-e`.|Specifica la stringa di connessione, le credenziali e i valori relativi all'origine dei dati utilizzati per connettere un server di report al database corrispondente.<br /><br /> Questo argomento non accetta un valore. È tuttavia necessario specificare ulteriori argomenti per definire tutti i valori di connessione richiesti.<br /><br /> Gli argomenti che è possibile specificare `-c` con `-m`includono, **-s** `-i`,`-d`,`-a`,`-u`,`-p`, e`-t`.|  
|`-e`|Obbligatorio se non si specifica l'argomento `-c`.|Specifica un account di esecuzione automatica dei report.<br /><br /> Questo argomento non accetta un valore. Per specificare i valori crittografati nel file di configurazione, tuttavia, è necessario includere ulteriori argomenti nella riga di comando.<br /><br /> In combinazione con `-e` è possibile specificare gli argomenti `-u` e `-p`. È inoltre possibile specificare `-t`.|  
|`-m`  *ComputerName*|Obbligatorio se si sta configurando un'istanza remota del server di report.|Specifica il nome del computer che ospita il server di report. Se questo argomento viene omesso, l'impostazione predefinita è `localhost`.|  
|**-s**  *servername*|Obbligatorio.|Specifica l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database del server di report.|  
|`-i`  *InstanceName*|Obbligatorio in caso di utilizzo di istanze denominate.|Se per ospitare il database del server di report è stata usata un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , questo valore specifica l'istanza denominata.|  
|`-d`  *DatabaseName*|Obbligatorio.|Specifica il nome del database del server di report.|  
|`-a`  *metododiautenticazione*|Obbligatorio.|Specifica il metodo di autenticazione utilizzato dal server di report per la connessione al relativo database. I valori validi sono `Windows` o `SQL`. Questo argomento non supporta la distinzione tra maiuscole e minuscole.<br /><br /> `Windows` specifica che il server di report utilizza l'autenticazione di Windows.<br /><br /> `SQL` specifica che il server di report utilizza l'autenticazione di SQL Server.|  
|`-u`  *[dominio\\] nome utente*|Obbligatorio in combinazione con `-e`, facoltativo in combinazione con `-c`.|Consente di specificare un account utente per la connessione al database del server di report o per l'account automatico.<br /><br /> Per **rsconfig -e**, questo argomento è obbligatorio. Deve essere un account utente di dominio.<br /><br /> Per **rsconfig-c** e `-a SQL`, questo argomento deve specificare un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account di accesso.<br /><br /> Per **rsconfig-c** e `-a Windows`, questo argomento può specificare un utente di dominio, un account predefinito o le credenziali dell'account del servizio. Se si specifica un account di dominio, specificare *dominio* e *nome utente* nel formato *dominio\nomeutente*. Se si utilizza un account predefinito, questo argomento è facoltativo. Se si desidera utilizzare le credenziali dell'account di servizio, omettere questo argomento.|  
|`-p`  *password*|Obbligatorio se si specifica `-u`.|Specifica la password da usare con l'argomento *nomeutente* . Se per l'account non è necessaria una password, è possibile non specificare alcun valore per questo argomento. Per gli account di dominio questo valore supporta la distinzione tra maiuscole e minuscole.|  
|`-t`|Facoltativo.|Crea l'output dei messaggi di errore nel log di traccia. Questo argomento non accetta un valore. Per altre informazioni, vedere [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
  
## <a name="permissions"></a>Autorizzazioni  
 È necessario essere un amministratore locale nel computer che ospita il server di report che si sta configurando.  
  
## <a name="file-location"></a>Percorso file  
 L'utilità rsconfig si trova in **\Programmi\Microsoft SQL Server\110\Tools\Binn**. È possibile eseguire l'utilità da qualsiasi cartella del file system.  
  
## <a name="remarks"></a>Osservazioni  
 Rsconfig.exe consente di:  
  
-   Modificare le informazioni di connessione utilizzate da un server di report per connettersi al relativo database.  
  
-   Configurare un account speciale che il server di report utilizza per accedere a un server di database remoto quando non sono disponibili altre credenziali.  
  
 È possibile eseguire l'utilità**rsconfig** in un'istanza locale o remota di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Non è possibile usare l'utilità **rsconfig** per decrittografare e visualizzare i valori già impostati.  
  
 Prima di eseguire questa utilità, nel computer in fase di configurazione deve essere installato Windows Management Instrumentation (WMI).  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti illustrano alcuni modi per usare **rsconfig**.  
  
#### <a name="specifying-a-domain-user-account"></a>Impostazione di un account utente di dominio  
 Nell'esempio seguente viene illustrata la configurazione di un server di report in modo che utilizzi un account utente di dominio durante la connessione al relativo database locale.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>Impostazione di un account utente del database di SQL Server  
 Nell'esempio seguente viene illustrato come configurare un server di report per utilizzare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la connessione a un database del server di report remoto.  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>Impostazione di un account predefinito  
 Nell'esempio seguente viene illustrata la configurazione di un server di report in modo che utilizzi un account predefinito durante la connessione al relativo database locale. Si noti che `-u` non viene utilizzato. Esempi di valori di account predefiniti supportati includono NT AUTHORITY\SYSTEM per il sistema locale e NT AUTHORITY\NetworkService per il servizio di[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] rete (solo).  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>Impostazione di un account di servizio  
 Nell'esempio seguente viene illustrata la configurazione di un server di report in modo che utilizzi all'account del servizio Windows ReportServer e l'account del servizio Web per la connessione al relativo database locale. Si noti che `-u` non viene utilizzato e che non viene specificata alcuna informazione sull'account. Quando i valori relativi all'account vengono eliminati dal comando, l'utilità **rsconfig** usa la sicurezza integrata e l'account del servizio con i quali viene eseguito ogni servizio.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>Impostazione di un account per l'esecuzione automatica su un server locale  
 Nell'esempio seguente viene illustrata la configurazione dell'account utilizzato per l'esecuzione automatica dei report che non trasmettono le credenziali all'origine dei dati esterna. L'account deve essere un account di dominio di Windows. Non è possibile specificare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il nome utente e la password. L'account viene configurato nell'istanza locale del server di report. I messaggi di errore vengono acquisiti nei log di traccia nella cartella ReportingServices\LogFiles.  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>Impostazione di un account per l'esecuzione automatica su un server remoto  
 Nell'esempio seguente viene illustrato come configurare l'account in un'istanza remota del server di report della stessa versione di Rsconfig.exe, ad esempio se la versione del server di report e quella di Rsconfig.exe sono entrambe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2. Le informazioni sui messaggi di errore vengono acquisite nei log di traccia nel server remoto.  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare una connessione al database del server di report &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Configurare l'account di esecuzione automatica &#40;Configuration Manager SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS &#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [File di configurazione di Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Utilità del prompt dei comandi del server di report &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [File di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
