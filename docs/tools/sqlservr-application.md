---
title: Applicazione sqlservr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 93a4572b44cf2be6fa8f1c0912fa7e8178e6c9a7
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733353"
---
# <a name="sqlservr-application"></a>Applicazione sqlservr
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  L'applicazione **sqlservr** avvia, arresta, sospende e riprende un'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dal prompt dei comandi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
sqlservr [-sinstance_name] [-c] [-dmaster_path] [-f]   
     [-eerror_log_path] [-lmaster_log_path] [-m]  
     [-n] [-Ttrace#] [-v] [-x] [-gnumber]  
```  
  
## <a name="arguments"></a>Argomenti  
 **-s** *_istanza*  
 Specifica l'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alla quale connettersi. Se non si specifica un'istanza denominata, **sqlservr** avvia l'istanza predefinita di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Per l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], è necessario usare l'applicazione **sqlservr** nella directory appropriata per l'istanza. Nel caso dell'istanza predefinita, eseguire **sqlservr** dalla directory \MSSQL\Binn. Nel caso dell'istanza denominata, eseguire **sqlservr** dalla directory \MSSQL$\*nome_istanza*\Binn.  
  
 **-c**  
 Indica l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in modo indipendente da Gestione controllo servizi di Windows. Questa opzione viene utilizzata dal prompt dei comandi all'avvio di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per ridurre il tempo di avvio di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se si usa questa opzione, non è possibile arrestare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando Gestione servizi [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oppure il comando **net stop** e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene arrestato se si disconnette il computer.  
  
 **-d** *master_path*  
 Indica il percorso completo del file del database **master** . Non sono presenti spazi tra **-d** e *master_path*. Se non si imposta questa opzione, vengono utilizzati i parametri esistenti nel Registro di sistema.  
  
 **-f**  
 Avvia un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la configurazione minima. È utile nel caso in cui l'impostazione di un valore di configurazione, ad esempio un'allocazione eccessiva di memoria, abbia impedito l'avvio del server.  
  
 **-e** *error_log_path*  
 Indica il percorso completo del file di log degli errori. Se omesso, il percorso predefinito è *Unità>\<* :\Programmi\Microsoft SQL Server\MSSQL\Log\Errorlog per l'istanza predefinita e *Unità>\<* :\Programmi\Microsoft SQL Server\MSSQL$*nome_istanza*\Log\Errorlog per un'istanza denominata. Non sono presenti spazi tra **-e** e *error_log_path*.  
  
 **-l** *master_log_path*  
 Indica il percorso completo del file del log delle transazioni del database **master** . Non sono presenti spazi tra **-l** e *master_log_path*.  
  
 **-m**  
 Indica l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] in modalità utente singolo. Se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene avviato in modalità utente singolo, la connessione è consentita solo a un utente. Il meccanismo di CHECKPOINT, che assicura la regolare scrittura delle transazioni completate dalla cache del disco al database, non viene avviato. In genere, questa opzione viene utilizzata quando si riscontrano problemi che richiedono interventi nei database di sistema. L'impostazione abilita l'opzione **sp_configure allow updates**. Per impostazione predefinita, l'opzione **allow updates** è disabilitata.  
  
 **-n**  
 Avvia un'istanza denominata di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se non si specifica il set di parametri **-s** , viene avviata l'istanza predefinita. Al prompt dei comandi è necessario passare alla directory BINN appropriata per l'istanza prima di avviare **sqlservr.exe**. Ad esempio, se Instance1 usa \mssql$Instance1 per i relativi file binari, l'utente deve passare alla directory \mssql$Instance1\binn per avviare **sqlservr.exe -s instance1**. Se si avvia un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con l'opzione **-n** , è consigliabile usare anche l'opzione **-e** . In caso contrario, gli eventi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non vengono registrati.  
  
 **-T** *trace#*  
 Indica l'avvio di un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con uno specifico flag di traccia (*trace#* ) attivo. I flag di traccia vengono utilizzati per avviare il server con un funzionamento non standard. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
> [!IMPORTANT]  
>  Quando si specifica un flag di traccia, indicarne il numero usando **-T**. La lettera minuscola t ( **-t**) è accettata da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ma **-t** imposta altri flag di traccia interni necessari per i tecnici del supporto tecnico per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **-v**  
 Visualizza il numero di versione del server.  
  
 **-x**  
 Disabilita la registrazione delle statistiche relative al tempo di utilizzo della CPU e alla frequenza di accesso alla cache. Consente l'ottimizzazione delle prestazioni.  
  
 **-g** *memory_to_reserve*  
 Specifica un numero intero di megabyte (MB) di memoria che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] riserva per le allocazioni di memoria all'interno del processo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ma esternamente al pool di memoria di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La memoria esterna al pool di memoria è l'area in cui [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] carica elementi quali file `.dll` delle procedure estese, provider OLE DB ai quali fanno riferimento le query distribuite e oggetti di automazione ai quali fanno riferimento le istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] . Il valore predefinito è 256 MB.  
  
 L'utilizzo di questa opzione può semplificare l'ottimizzazione dell'allocazione di memoria ma soltanto se la memoria fisica supera il limite configurato specifico del sistema operativo per la memoria virtuale disponibile per le applicazioni. L'opzione può risultare appropriata in configurazioni con grandi quantità di memoria, in cui i requisiti di utilizzo della memoria di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] risultano atipici e lo spazio degli indirizzi virtuale del processo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è utilizzato completamente. L'utilizzo errato di questa opzione può impedire l'avvio dell'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o generare errori di esecuzione.  
  
 Usare il valore predefinito per il parametro **-g** a meno che nel log degli errori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non venga visualizzato uno degli avvisi seguenti:  
  
-   "Failed Virtual Allocate Bytes: FAIL_VIRTUAL_RESERVE \<size>"  
  
-   "Failed Virtual Allocate Bytes: FAIL_VIRTUAL_COMMIT \<size>"  
  
 Questi messaggi possono indicare che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sta cercando di liberare settori del pool di memoria di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per l'inserimento di oggetti quali file dll per stored procedure estese o oggetti di automazione. In questo caso, è consigliabile aumentare la quantità di memoria riservata usando l'opzione **-g** .  
  
 L'utilizzo di un valore inferiore a quello predefinito aumenta la quantità di memoria disponibile per il pool del buffer e gli stack di thread. Ciò può determinare vantaggi a livello delle prestazioni per carichi di lavoro che impegnano molta memoria in sistemi che non utilizzano un gran numero di stored procedure estese, query distribuite o oggetti di automazione.  
  
## <a name="remarks"></a>Remarks  
 Nella maggior parte dei casi il programma sqlservr.exe viene utilizzato solo per la risoluzione dei problemi o interventi di manutenzione ordinaria. Se si avvia [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dal prompt dei comandi con sqlservr.exe, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non viene avviato come servizio. Quindi, non sarà possibile arrestare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando i comandi **net** . Gli utenti possono connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], ma gli strumenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] indicano lo stato del servizio. Di conseguenza, Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] indica correttamente che il servizio è stato arrestato. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] può connettersi al server anche se indica che il servizio è stato arrestato.  
  
## <a name="compatibility-support"></a>Informazioni sulla compatibilità  
 Il parametro **-h**  non è supportato in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Questo parametro è stato utilizzato in versioni precedenti di istanze a 32 bit di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per riservare spazio di indirizzi della memoria virtuale per metadati della memoria a caldo quando AWE è abilitato. Per altre informazioni, vedere [Funzionalità di SQL Server sospese in SQL Server 2016](https://msdn.microsoft.com/library/0678bfbc-5d3f-44f4-89c0-13e8e52404da).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di avvio del servizio del motore di database](../database-engine/configure-windows/database-engine-service-startup-options.md)  
  
  
