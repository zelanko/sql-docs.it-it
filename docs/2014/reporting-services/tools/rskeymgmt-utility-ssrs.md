---
title: Utilità rskeymgmt (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c9b5ca361cbfb5de42341fad8625f10d7ce3c2fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099806"
---
# <a name="rskeymgmt-utility-ssrs"></a>Utilità rskeymgmt (SSRS)
  Questa utilità consente di estrarre, ripristinare, creare ed eliminare la chiave simmetrica utilizzata per proteggere i dati riservati del server di report dall'accesso non autorizzato. Questa utilità viene inoltre utilizzata per unire in join istanze del server di report in un'implementazione basata sulla scalabilità orizzontale. La *distribuzione con scalabilità orizzontale di un server di report* fa riferimento a più istanze del server di report che condividono lo stesso database del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
      rskeymgmt {-?}  
{-eextract}  
{-aapply}  
{-ddeleteall}  
{-srecreatekey}  
{-rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>Argomenti  
 **-?**  
 Visualizza la sintassi degli argomenti **rskeymgmt** .  
  
 **-e**  
 Consente di estrarre la chiave simmetrica utilizzata per crittografare e decrittografare i dati per l'istanza del server di report in modo da renderne possibile la copia in un file.  
  
 Questo argomento non accetta un valore. Per completare l'estrazione, tuttavia, è necessario includere ulteriori argomenti. Gli argomenti che è necessario specificare includono `-f` e `-p`.  
  
 **-a**  
 Sostituisce una chiave simmetrica esistente con una copia specificata in un file di backup protetto da password. Tutte le istanze della chiave simmetrica vengono aggiornate.  
  
 Questo argomento non accetta un valore. Per selezionare il file contenente la chiave da applicare, è tuttavia necessario includere ulteriori argomenti. Gli argomenti che è possibile specificare includono `-f` e `-p`.  
  
 **-d**  
 Elimina tutte le istanze della chiave simmetrica e tutti i dati crittografati in un database del server di report. Questo argomento non accetta un valore.  
  
 `-s`  
 Genera una nuova chiave simmetrica e crittografa di nuovo tutto il contenuto crittografato in base alla nuova chiave. Tutte le istanze della chiave simmetrica verranno rigenerate.  
  
 `-j`  
 Configura un'istanza remota del server di report in modo che condivida il database del server di report utilizzato dall'istanza locale del server di report.  
  
 **-r**  *installationID*  
 Consente di rimuovere le informazioni relative alla chiave simmetrica per un'istanza specifica del server di report, quindi di rimuovere il server di report da un'implementazione basata sulla scalabilità orizzontale. *installationID* è un valore GUID disponibile nel file RSReportserver.config.  
  
 `-f`  *file*  
 Consente di specificare il percorso completo del file in cui è archiviata una copia di backup delle chiavi simmetriche.  
  
 Per l'argomento **rskeymgmt -e**, la chiave simmetrica viene scritta nel file specificato.  
  
 Per l'argomento **rskeymgmt -a**, il valore di chiave simmetrica archiviato nel file viene applicato all'istanza del server di report.  
  
 `-p`  *password*  
 (Obbligatorio per `-f`) Consente di specificare la password utilizzata per eseguire il backup o applicare una chiave simmetrica. Questo valore non può essere omesso.  
  
 `-i`  
 Specifica un'istanza locale del server di report. Questo argomento è facoltativo se il server di report è stato installato nell'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (il valore predefinito per `-i` è MSSQLSERVER). Se si installa il server di report come istanza denominata, l'argomento `-i` è obbligatorio.  
  
 `-m`  
 Specifica il nome del computer remoto in cui risiede l'istanza del server di report che si sta unendo in join all'implementazione del server di report basata sulla scalabilità orizzontale. Utilizzare il nome del computer che lo identifica all'interno della rete.  
  
 `-n`  
 Specifica il nome dell'istanza del server di report in un computer remoto. Questo argomento è facoltativo se il server di report è stato installato nell'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (il valore predefinito per `-n` è MSSQLSERVER). Se si installa il server di report come istanza denominata, l'argomento `-n` è obbligatorio.  
  
 `-u`  *AccountUtente*  
 Consente di specificare l'account amministratore nel computer remoto che si sta unendo in join alla distribuzione con scalabilità orizzontale Se non si specifica un account, vengono utilizzate le credenziali dell'utente corrente.  
  
 `-v`  *password*  
 (Obbligatorio per `-u`) Consente di specificare la password di un account amministratore nel computer remoto che si desidera unire in join alla distribuzione con scalabilità orizzontale.  
  
 **-t**  *trace*  
 Crea l'output dei messaggi di errore nel log di traccia. Questo argomento non accetta un valore. Per altre informazioni, vedere [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire lo strumento è necessario essere un amministratore locale ed eseguirlo a livello locale nel computer in cui risiede il server di report. L'utilità rskeymgmt interagisce con l'istanza locale del servizio Windows ReportServer. L'utilità non è infatti in grado di connettersi alle istanze remote del servizio Windows ReportServer e pertanto non può essere utilizzata per gestire le chiavi di crittografia di un'istanza remota del server di report.  
  
> [!NOTE]  
>  Se si utilizzano gli argomenti `-u` e `-v`, verificare di aver specificato un account che dispone delle autorizzazioni di amministratore nel computer remoto.  
  
## <a name="examples"></a>Esempi  
 Gli esempi seguenti illustrano alcuni modi per usare **rskeymgmt**. Negli esempi seguenti viene illustrato come estrarre, ripristinare ed eliminare le chiavi di crittografia, nonché come configurare una distribuzione con scalabilità orizzontale di un server di report.  
  
#### <a name="extracting-encryption-keys"></a>Estrazione delle chiavi di crittografia  
 Nell'esempio seguente viene illustrato come creare una copia di backup della chiave di crittografia e come salvarla in un file protetto da password in un disco floppy. Se il server di report è stato installato come istanza denominata, aggiungere l'argomento `-i`.  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>Ripristino delle chiavi di crittografia  
 Nell'esempio seguente viene illustrato come sostituire la chiave di crittografia. È necessario specificare la posizione della copia di backup della chiave e la password che sblocca il file.  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>Eliminazione delle chiavi di crittografia e del contenuto crittografato  
 Nell'esempio seguente viene illustrato come eliminare tutte le chiavi di crittografia archiviate in un server di report. Se l'installazione corrente è un'implementazione del server di report basata sulla scalabilità orizzontale, verranno eliminate le chiavi di crittografia per tutte le istanze del server di report incluse nell'implementazione. L'eliminazione di una chiave di crittografia comporta l'eliminazione anche dei valori crittografati esistenti nel database del server di report. Per altre informazioni sul contenuto crittografato, vedere [Archiviare i dati crittografati del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md).  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>Unione in join di un'istanza remota denominata del server di report a un'implementazione basata sulla scalabilità orizzontale  
 Nell'esempio seguente viene illustrato come aggiungere un'istanza del server di report installata in un computer remoto a un'implementazione del server di report basata sulla scalabilità orizzontale. È necessario eseguire il comando in uno dei computer già configurati per l'utilizzo del database condiviso. Gli argomenti del comando specificano l'istanza remota del server di report che si desidera unire in join all'implementazione basata sulla scalabilità orizzontale.  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  Un'implementazione del server di report basata sulla scalabilità orizzontale fa riferimento a un modello di implementazione dove più istanze del server di report condividono lo stesso database. Un database del server di report può essere utilizzato da qualsiasi istanza del server di report che archivia le relative chiavi simmetriche nel database. Se, ad esempio, un database del server di report contiene le informazioni sulle chiavi per tre istanze del server di report, queste tre istanze verranno considerate membri della stessa implementazione basata sulla scalabilità orizzontale.  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>Unione in join di istanze del server di report nello stesso computer  
 È possibile creare una distribuzione con scalabilità orizzontale da più istanze del server di report installate nello stesso computer. Se si esegue l'unione in join di istanze del server di report installate localmente, non impostare gli argomenti `-u` e `-v`. Gli argomenti `-u` e `-v` vengono infatti utilizzati solo per l'unione in join di un'istanza di un computer remoto. Se si specificano tali argomenti, viene visualizzato il messaggio di errore seguente: "Impossibile usare le credenziali dell'utente per le connessioni locali".  
  
 Nell'esempio seguente viene illustrata la sintassi per la creazione di una distribuzione con scalabilità orizzontale utilizzando più istanze locali. In questo esempio <`initializedinstance`> è il nome di un'istanza già inizializzata per utilizzare il database del server di report e <`newinstance`> è il nome dell'istanza che si desidera aggiungere alla distribuzione:  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>Rimozione delle chiavi di crittografia per un singolo server di report in un'implementazione basata sulla scalabilità orizzontale  
 Nell'esempio seguente viene illustrato come rimuovere le chiavi di crittografia per un singolo server di report in un'implementazione del server di report basata sulla scalabilità orizzontale. Le chiavi vengono rimosse dal database del server di report. Dopo l'eliminazione delle chiavi relative all'istanza specifica del server di report, tale istanza non potrà più accedere ai dati crittografati nel database e pertanto verrà rimossa in modo definitivo dall'implementazione basata sulla scalabilità orizzontale.  
  
 Per rimuovere un'istanza del server di report da una distribuzione con scalabilità orizzontale, è necessario specificare un ID di installazione. L'ID di installazione è un GUID archiviato nel file RSReportserver.config dell'istanza del server di report per la quale si desidera rimuovere le chiavi di crittografia. È necessario eseguire il comando seguente nel computer che si desidera rimuovere dall'implementazione basata sulla scalabilità orizzontale. Se il server di report è stato installato come istanza denominata, utilizzare l'argomento `-i` per specificare l'istanza. Per altre informazioni, vedere [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md).  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>Percorso file  
 Rskeymgmt. exe si trova in ** \< *unità*>: \Programmi\Microsoft SQL Server\110\Tools\Binn** o at ** \< *Drive*>: \Program Files (x86) \Microsoft SQL Server\110\Tools\Binn**. È possibile eseguire l'utilità da qualsiasi cartella del file system.  
  
## <a name="remarks"></a>Osservazioni  
 Il server di report crittografa le informazioni di connessione e le credenziali archiviate. Per la crittografia dei dati vengono utilizzate una chiave pubblica e una chiave simmetrica. Il server di report viene eseguito solo se un database del server di report dispone di chiavi valide. È possibile usare **rskeymgmt** per eseguire il backup, eliminare o ripristinare le chiavi. Se non è possibile ripristinare le chiavi, questo strumento consente di eliminare il contenuto crittografato non più utilizzabile.  
  
 L'utilità **rskeymgmt** consente di gestire il set di chiavi definito durante l'installazione o l'inizializzazione. L'utilità si connette al servizio Windows ReportServer locale tramite un endpoint RPC (Remote Procedure Call, chiamata di procedura remota). Per garantire il corretto funzionamento di questa utilità, è necessario che il servizio Windows ReportServer sia in esecuzione.  
  
 Per altre informazioni sulle chiavi di crittografia, vedere [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md) e [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Configuration Manager SSRS&#41;](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Utilità del prompt dei comandi del server di report &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [Configurare e gestire chiavi di crittografia &#40;Gestione configurazione SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
