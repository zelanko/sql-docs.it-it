---
title: adattatore del cloud per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cloud adapter
- Deploy to Azure
ms.assetid: 82ed0d0f-952d-4d49-aa36-3855a3ca9877
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bf57adb31330f5b0c0f18fbcccd4d71f47d3c933
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176014"
---
# <a name="cloud-adapter-for-sql-server"></a>Adattatore cloud per SQL Server
  Il servizio adattatore del cloud viene creato come parte del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] provisioning in una macchina virtuale di Azure. Il servizio Adattatore del cloud genera un certificato SSL autofirmato quando viene eseguito per la prima volta, quindi viene eseguito come account di **sistema locale** . Genera un file di configurazione utilizzato per autoconfigurarsi. L'adattatore cloud crea inoltre una regola di Windows Firewall per autorizzare le connessioni TCP in ingresso alla porta predefinita 11435.  
  
 L'adattatore cloud è un servizio senza stato e sincrono tramite cui si ricevono i messaggi da un'istanza locale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando il servizio adattatore cloud viene arrestato, l'adattatore cloud con accesso remoto viene arrestato, l'associazione del certificato SSL viene annullata e la regola di Windows Firewall viene disabilitata.  
  
## <a name="cloud-adapter-requirements"></a>Requisiti dell'adattatore cloud  
 Per installare, abilitare ed eseguire l'adattatore cloud per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è necessario tenere in considerazione i requisiti seguenti:  
  
-   L'adattatore cloud è supportato con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 e versioni successive. In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012, per l'adattatore cloud per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è necessario SMO (SQL Management Objects) per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012.  
  
-   Il servizio Web Adattatore del cloud viene eseguito come account di **sistema locale** e verifica le credenziali del client prima dell'esecuzione di qualsiasi attività. Le credenziali fornite dal client devono appartenere all'account use membro del gruppo **Administrators** locale nel computer remoto.  
  
-   L'adattatore cloud supporta solo l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   L'adattatore cloud utilizza l'account amministratore locale della macchina virtuale per eseguire i comandi nel computer locale e non un account amministratore di sistema.  
  
-   L'adattatore cloud è in attesa su TCP/IP. Il numero di porta predefinito è 11435.  
  
-   L'adattatore cloud deve disporre delle autorizzazioni per creare e modificare le regole di Windows Firewall.  
  
## <a name="cloud-adapter-configuration-settings"></a>Impostazioni di configurazione dell'adattatore cloud  
 Per modificare le impostazioni di un adattatore cloud, utilizzare le informazioni sulla configurazione dell'adattatore cloud riportate di seguito.  
  
-   **Percorso predefinito del file di configurazione** : C:\Programmi\Microsoft SQL Server\120\Tools\CloudAdapter\  
  
-   **Parametri del file di configurazione** -  
  
    -   \<configuration>  
  
        -   \<appSettings>  
  
            -   \<add key="WebServicePort" value="" />  
  
            -   \<add key="WebServiceCertificate" value="GUID" />  
  
            -   \<add key="ExposeExceptionDetails" value="true" />  
  
        -   \</appSettings>  
  
    -   \<>/configurazione  
  
-   **Dettagli del certificato** : il certificato presenta i valori seguenti:  
  
    -   Subject-"CN = CloudAdapter\<VMName >, DC = SQL Server, DC = Microsoft"  
  
    -   Il certificato deve disporre di un solo utilizzo chiavi avanzato (EKU) nell'attributo Autenticazione server.  
  
    -   La lunghezza della chiave del certificato è 2048.  
  
 **Valori del file di configurazione**:  
  
|Impostazione|Valori|Predefinito|Commenti|  
|-------------|------------|-------------|--------------|  
|WebServicePort|1-65535|11435|Se omesso, viene utilizzato 11435.|  
|WebServiceCertificate|Thumbprint|Empty|Se vuoto, viene generato un nuovo certificato autofirmato.|  
|ExposeExceptionDetails|True/False|False||  
  
## <a name="cloud-adapter-troubleshooting"></a>Risoluzione dei problemi dell'adattatore cloud  
 Per risolvere i problemi relativi all'adattatore cloud per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], fare riferimento alle informazioni seguenti:  
  
-   **Gestione degli errori e registrazione** : gli errori e i messaggi di stato vengono scritti nel registro eventi dell'applicazione.  
  
-   **Traccia, eventi** : tutti gli eventi vengono scritti nel registro eventi dell'applicazione.  
  
-   **Controllo, configurazione** : usare il file di configurazione che si trova in:  C:\Programmi\Microsoft SQL Server\120\Tools\CloudAdapter\\.  
  
|Errore|ID errore|Causa|Risoluzione|  
|-----------|--------------|-----------|----------------|  
|Si è verificata un'eccezione durante l'aggiunta del certificato all'archivio certificati. {Testo dell'eccezione}.|45560|Autorizzazioni per l'archiviazione dei certificati del computer|Verificare che il servizio adattatore cloud disponga delle autorizzazioni per aggiungere i certificati all'archivio certificati del computer.|  
|Si è verificata un'eccezione durante il tentativo di configurare l'associazione SSL per la porta {numero di porta} e il certificato {Identificazione digitale}. {Eccezione}.|45561|Un'altra applicazione ha già utilizzato la porta o vi ha già associato un certificato.|Rimuovere le associazioni esistenti o modificare la porta dell'adattatore cloud nel file di configurazione.|  
|Impossibile trovare il certificato SSL [{Identificazione digitale}] nell'archivio certificati.|45564|L'identificazione digitale del certificato è nel file di configurazione, ma l'archivio certificati personale per il servizio non contiene il certificato.<br /><br /> Autorizzazioni insufficienti.|Verificare che il certificato sia nell'archivio certificati personale per il servizio.<br /><br /> Verificare che il servizio disponga delle autorizzazioni corrette per l'archivio.|  
|Impossibile avviare il servizio Web. {Testo dell'eccezione}.|45570|Descritto nell'eccezione.|Abilitare ExposeExceptionDetails e utilizzare le informazioni estese dell'eccezione.|  
|Il certificato [{Identificazione digitale}] è scaduto.|45565|Si fa riferimento a un certificato scaduto nel file di configurazione.|Aggiungere un certificato valido e aggiornare il file di configurazione con la relativa identificazione digitale.|  
|Errore del servizio Web {0}:.|45571|Descritto nell'eccezione.|Abilitare ExposeExceptionDetails e utilizzare le informazioni estese dell'eccezione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire un database di SQL Server a una macchina virtuale di Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)  
  
  
