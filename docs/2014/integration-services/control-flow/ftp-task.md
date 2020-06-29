---
title: Attività FTP | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.f1
helpviewer_keywords:
- FTP task [Integration Services]
ms.assetid: 41c3f2c4-ee04-460a-9822-bb9ae4036c2e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c242eb77173c628c4bc3752da4d1d9709724aba4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432888"
---
# <a name="ftp-task"></a>Attività FTP
  L'attività FTP consente di caricare e scaricare file di dati, nonché di gestire directory nei server. Un pacchetto può ad esempio scaricare file di dati da un server remoto o da un indirizzo Internet nell'ambito del flusso di lavoro di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . È possibile utilizzare l'attività FTP per gli scopi seguenti:  
  
-   Copia di directory e file di dati da una directory all'altra, prima o dopo lo spostamento dei dati, e applicazione di trasformazioni ai dati.  
  
-   Accesso a un percorso FTP di origine e copia di file o pacchetti in una directory di destinazione.  
  
-   Download di file da un percorso FTP e applicazione di trasformazioni ai dati delle colonne prima del caricamento dei dati in un database.  
  
 In fase di esecuzione l'attività FTP si connette a un server tramite una gestione connessione FTP configurata separatamente, a cui viene fatto riferimento dall'attività FTP. La gestione connessione FTP include le impostazioni del server, le credenziali per l'accesso al server FTP e opzioni quali il timeout e il numero dei tentativi consentiti per la connessione al server. Per altre informazioni, vedere [Gestione connessione FTP](../connection-manager/ftp-connection-manager.md).  
  
> [!IMPORTANT]  
>  La gestione connessione FTP supporta solo l'autenticazione anonima e l'autenticazione di base. Non supporta l'autenticazione di Windows.  
  
 Per l'accesso a un file o a una directory locale, l'attività FTP utilizza un percorso archiviato in una variabile o una gestione connessione file. Per l'accesso a un file o a una directory remota, invece, l'attività FTP utilizza un percorso archiviato in una variabile oppure specificato direttamente sul server remoto, come indicato nella gestione connessione FTP. Per altre informazioni, vedere [Gestione connessione File](../connection-manager/file-connection-manager.md) e [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md).  
  
 Questo significa che l'attività FTP può ricevere più file ed eliminare più file remoti, ma se utilizza una gestione connessione può inviare ed eliminare un solo file locale alla volta, poiché una gestione connessione file può accedere a un solo file. Per accedere a più file locali, è necessario specificarne il percorso utilizzando una variabile. Una variabile contenente "C:\Test\\*.txt" specifica ad esempio un percorso per l'eliminazione o l'invio di tutti i file con estensione txt presenti nella directory Test.  
  
 In alternativa, per inviare più file e accedere a più file e directory locali è possibile eseguire più volte l'attività FTP includendola in un ciclo Foreach, che è in grado di eseguire un'enumerazione su tutti i file in una directory tramite l'enumeratore For Each File. Per altre informazioni, vedere [Contenitore Ciclo Foreach](foreach-loop-container.md).  
  
 L'attività FTP supporta i caratteri jolly punto interrogativo *?* e asterisco *\** nei percorsi. e questo consente di accedere a più file. I caratteri jolly possono essere tuttavia utilizzati solo nella parte del percorso che specifica il nome del file. Ad esempio, C:\Directory\\*.txt è un percorso valido, mentre C:\\\*\Testo.txt non lo è.  
  
 Le operazioni FTP possono essere configurate in modo da arrestare l'attività File system se l'operazione non riesce oppure in modo da trasferire i file in modalità ASCII. Le operazioni che inviano e ricevono copie di file possono essere configurate in modo da sovrascrivere i file e le directory di destinazione.  
  
## <a name="predefined-ftp-operations"></a>Operazioni FTP predefinite  
 L'attività FTP include un set predefinito di operazioni, descritte nella tabella seguente.  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|Invia file|Invia un file dal computer locale al server FTP.|  
|Ricevi file|Salva sul computer locale un file scaricato dal server FTP.|  
|Crea directory locale|Crea una cartella sul computer locale.|  
|Crea directory remota|Crea una cartella sul server FTP.|  
|Rimuovi directory locale|Elimina una cartella dal computer locale.|  
|Rimuovi directory remota|Elimina una cartella dal server FTP.|  
|Elimina file locali|Consente di eliminare un file nel computer locale.|  
|Elimina file remoti|Consente di eliminare un file nel server FTP.|  
  
## <a name="custom-log-entries-available-on-the-ftp-task"></a>Voci di log personalizzate disponibili nell'attività FTP  
 Nella tabella seguente sono elencate le voci di log personalizzate disponibili per l'attività FTP. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`FTPConnectingToServer`|Indica che l'attività ha stabilito una connessione al server FTP.|  
|`FTPOperation`|Specifica l'inizio e il tipo dell'operazione FTP eseguita dall'attività.|  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni su come impostare queste proprietà nella finestra di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Impostare le proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md).  
  
 Per altre informazioni sull'impostazione di queste proprietà a livello di programmazione, vedere <xref:Microsoft.SqlServer.Dts.Tasks.FtpTask.FtpTask>.  
  
## <a name="see-also"></a>Vedere anche  
 [Editor attività FTP &#40;pagina generale&#41;](../general-page-of-integration-services-designers-options.md)   
 [Editor attività FTP &#40;pagina trasferimento file&#41;](../ftp-task-editor-file-transfer-page.md)   
 [Attività Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
