---
title: Configurazione motore di database-Directory dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfb62ec0bbd16a2b77e2f05f64d36ef31498a100
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095895"
---
# <a name="database-engine-configuration---data-directories"></a>Configurazione Motore di database - Directory dati
  Usare questa pagina per specificare il percorso di installazione per i file di dati e di programma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. A seconda del tipo di installazione possono essere supportati i tipi di archivio seguenti: disco locale, spazio di archiviazione condiviso o file server SMB.  
  
 Per specificare una condivisione file SMB come directory, è necessario immettere manualmente il percorso UNC supportato. La selezione di una condivisione file SMB non è supportata. Il formato di un percorso UNC supportato di una condivisione file SMB è \\\NomeServer\NomeCondivisione\\...  
  
## <a name="stand-alone-instance-of-ssnoversion"></a>Istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nella tabella seguente vengono elencati i tipi di archivio supportati e le directory predefinite per un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
  
|Descrizione|Tipo di archivio supportato|Directory predefinita|Consigli|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directory radice dati|Disco locale, file server SMB, spazio di archiviazione condiviso <sup>1</sup>|\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] C:\Programmi il programma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di installazione configurerà ACL per le directory e interromperà l'ereditarietà come parte della configurazione.[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \||  
|Directory database utente|Disco locale, file server SMB, spazio di archiviazione condiviso <sup>1</sup>|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]C:\Programmi\\\MSSQL12. \<InstanceId> \MSSQL\Data|Le procedure consigliate per le directory dei dati dell'utente dipendono dai requisiti del carico di lavoro e delle prestazioni.|  
|Directory log database utente|Disco locale, file server SMB, spazio di archiviazione condiviso <sup>1</sup>|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]C:\Programmi\\\MSSQL12. \<InstanceId> \MSSQL\Data|Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
|Directory database temporaneo|Disco locale, file server SMB, spazio di archiviazione condiviso <sup>1</sup>|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]C:\Programmi\\\MSSQL12. \<InstanceId> \MSSQL\Data|Le procedure consigliate per la directory Temp dipendono dai requisiti del carico di lavoro e delle prestazioni.|  
|Directory log database temporaneo|Disco locale, file server SMB, spazio di archiviazione condiviso <sup>1</sup>|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]C:\Programmi\\\MSSQL12. \<InstanceId> \MSSQL\Data|Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
|Directory di backup|Disco locale, file server SMB, spazio di archiviazione condiviso <sup>1</sup>|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]C:\Programmi\\\MSSQL12. \<InstanceId> \MSSQL\BACKUP|Impostare le autorizzazioni appropriate in modo da impedire la perdita di dati e assicurarsi che all'account utente per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengano concesse autorizzazioni adeguate per la scrittura nella directory di backup. Non è supportato l'utilizzo di un'unità di cui è stato eseguito il mapping per le directory di backup.|  
  
 <sup>1</sup> sebbene i dischi condivisi siano supportati, non è una procedura consigliata per un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="failover-cluster-instance-of-ssnoversion"></a>Istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nella tabella seguente vengono elencati i tipi di archivio supportati e le directory predefinite per un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrizione|Tipo di archivio supportato|Directory predefinita|Consigli|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directory radice dati|Spazio di archiviazione condiviso, file server SMB|\<Unità:>\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Suggerimento: se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.|  
|Directory database utente|Spazio di archiviazione condiviso, file server SMB|\<Unità: >programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. \<InstanceId> \MSSQL\Data<br /><br /> Suggerimento: se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Le procedure consigliate per le directory dei dati dell'utente dipendono dai requisiti del carico di lavoro e delle prestazioni.|  
|Directory log database utente|Spazio di archiviazione condiviso, file server SMB|\<Unità: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. \<InstanceId> \MSSQL\Data<br /><br /> Suggerimento: se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
|Directory database temporaneo|Disco locale, spazio di archiviazione condiviso, file server SMB|\<Unità: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. \<InstanceId> \MSSQL\Data<br /><br /> Suggerimento: se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Assicurarsi che la directory specificata sia valida per tutti i nodi del cluster. Durante il failover, se le directory tempdb non sono disponibili nel nodo di destinazione del failover, la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verrà riportata online.|  
|Directory log database temporaneo|Disco locale, spazio di archiviazione condiviso, file server SMB|\<Unità: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. \<InstanceId> \MSSQL\Data<br /><br /> Suggerimento: se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Assicurarsi che la directory specificata sia valida per tutti i nodi del cluster. Durante il failover, se le directory tempdb non sono disponibili nel nodo di destinazione del failover, la risorsa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non verrà riportata online.|  
|Directory di backup|Disco locale, spazio di archiviazione condiviso, file server SMB|\<Unità: > \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. \<InstanceId> \MSSQL\BACKUP<br /><br /> Suggerimento: se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Impostare le autorizzazioni appropriate in modo da impedire la perdita di dati e assicurarsi che all'account utente per il servizio SQL Server vengano concesse autorizzazioni adeguate per la scrittura nella directory di backup. Non è supportato l'utilizzo di un'unità di cui è stato eseguito il mapping per le directory di backup.|  
  
## <a name="security-considerations"></a>Considerazioni relative alla sicurezza  
 Durante l'installazione vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.  
  
 Al file server SMB si applicano le indicazioni seguenti:  
  
-   L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere un account di dominio se viene utilizzato un file server SMB.  
  
-   L'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre delle autorizzazioni FULL CONTROL NTFS nella cartella di condivisione file SMB utilizzata come directory dei dati.  
  
-   È necessario che all'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga concesso il privilegio SeSecurityPrivilege nel file server SMB. Per concedere tale privilegio, utilizzare la console Criteri di sicurezza locale nel file server per aggiungere l'account di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai criteri **Gestione file registro di controllo e di sicurezza** . Questa impostazione è disponibile nella sezione **Assegnazione diritti utente** in **Criteri locali** nella console **Criteri di sicurezza locali** .  
  
## <a name="notes"></a>Note  
  
-   Quando si aggiungono caratteristiche a un'installazione esistente, non è possibile modificare il percorso di una caratteristica installata in precedenza, né specificare il percorso di una nuova caratteristica.  
  
-   Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anche i componenti [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere installati in directory separate.  
  
-   Non è possibile installare file di programma e file di dati nelle situazioni seguenti:  
  
    -   In un'unità disco rimovibile  
  
    -   In un file system che utilizza la compressione  
  
    -   In una directory in cui si trovano i file di sistema  
  
    -   In un'unità di rete di cui è stato eseguito il mapping in un'istanza del cluster di failover  
  
## <a name="see-also"></a>Vedi anche  
 [Percorsi dei file per le istanze predefinite e denominate di SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [Autorizzazioni NTFS e di condivisione per un file server](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
