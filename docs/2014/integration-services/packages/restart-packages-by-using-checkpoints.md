---
title: Riavviare i pacchetti tramite checkpoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 945bb384f522aa483c490fccd92768078a2d315a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365055"
---
# <a name="restart-packages-by-using-checkpoints"></a>Riavvio dei pacchetti tramite checkpoint
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] può riavviare i pacchetti non eseguiti correttamente a partire dal punto in cui si è verificato l'errore, invece di eseguire di nuovo l'intero pacchetto. Se un pacchetto è configurato per l'utilizzo di checkpoint, le informazioni sull'esecuzione del pacchetto vengono scritte in un file del checkpoint. Questo file viene quindi utilizzato per il riavvio di un pacchetto dal punto in cui si è verificato l'errore. Se il pacchetto viene eseguito correttamente, il file del checkpoint viene eliminato e quindi creato nuovamente alla successiva esecuzione del pacchetto.  
  
 L'utilizzo di checkpoint in un pacchetto offre i vantaggi seguenti.  
  
-   Non è necessario caricare e scaricare nuovamente file di grandi dimensioni. Un pacchetto che scarica più file di grandi dimensioni utilizzando un'attività FTP distinta per ogni download può ad esempio essere riavviato se il download di un singolo file ha esito negativo. È quindi sufficiente scaricare nuovamente solo questo file.  
  
-   Non è necessario caricare nuovamente grandi quantità di dati. Un pacchetto che esegue inserimenti bulk in tabelle delle dimensioni di un data warehouse utilizzando un'attività Inserimento bulk distinta per ogni dimensione può ad esempio essere riavviato se l'inserimento ha esito negativo per una tabella della dimensioni. Verrà quindi caricata nuovamente solo tale dimensione.  
  
-   Non è necessario ripetere l'aggregazione di valori. Un pacchetto che calcola numerose aggregazioni, quali medie e somme, utilizzando un'attività Flusso di dati distinta per ogni aggregazione può ad esempio essere riavviato se il calcolo di un'aggregazione ha esito negativo. Verrà quindi ricalcolata solo tale aggregazione.  
  
 Se un pacchetto è stato configurato per l'utilizzo di checkpoint, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] il punto di riavvio viene acquisito nel file del checkpoint. Il tipo di contenitore che ha esito negativo e l'implementazione di caratteristiche quali le transazioni influiscono sul punto di riavvio registrato nel file del checkpoint. Nel file del checkpoint vengono acquisiti anche i valori correnti delle variabili. I valori delle variabili con tipo di dati `Object` non vengono tuttavia salvati nei file del checkpoint.  
  
## <a name="defining-restart-points"></a>Definizione dei punti di riavvio  
 Il contenitore host delle attività, che incapsula una sola attività, corrisponde all'unità di lavoro atomica più piccola che può essere riavviata. Anche il contenitore Ciclo Foreach e un contenitore transazionale vengono considerati unità di lavoro atomiche.  
  
 Se un pacchetto viene arrestato durante l'esecuzione di un contenitore transazionale, la transazione viene interrotta e viene eseguito il rollback del lavoro eseguito dal contenitore. Al riavvio del pacchetto il contenitore che ha avuto esito negativo viene riavviato. Il completamento di eventuali contenitori figlio del contenitore transazionale non viene registrato nel file del checkpoint. Di conseguenza, al riavvio del pacchetto, il contenitore transazionale e i contenitori figlio vengono eseguiti di nuovo.  
  
> [!NOTE]  
>  L'utilizzo di checkpoint e transazioni nello stesso pacchetto può provocare risultati imprevisti. È possibile, ad esempio, che un pacchetto che restituisce un errore e viene riavviato da un checkpoint ripeta una transazione di cui è già stato eseguito correttamente il commit.  
  
 I dati di checkpoint non vengono salvati per i contenitori Ciclo For e Foreach. Al riavvio di un pacchetto, i contenitori Ciclo For e Foreach e i contenitori figlio vengono rieseguiti. Un contenitore figlio del ciclo eseguito correttamente non viene registrato nel file del checkpoint, ma rieseguito. Per altre informazioni e per ottenere una soluzione, vedere [SSIS Checkpoints are not honored for For Loop or Foreach Loop container items](https://go.microsoft.com/fwlink/?LinkId=241633)(Mancata applicazione dei checkpoint SSIS per gli elementi contenitori Ciclo For e Foreach).  
  
 Se il pacchetto viene riavviato, le configurazioni di pacchetto non vengono caricate nuovamente. Il pacchetto infatti utilizza le informazioni di configurazione scritte nel file del checkpoint. Ciò garantisce che per la riesecuzione di un pacchetto vengano utilizzate le configurazioni in uso quando il pacchetto ha avuto esito negativo.  
  
 Un pacchetto può essere riavviato solo a livello del flusso di controllo, Non è possibile riavviare un pacchetto all'interno di un flusso di dati. Per evitare la riesecuzione dell'intero flusso di dati, è possibile configurare il pacchetto in modo che includa più flussi di dati che utilizzano ognuno un'attività Flusso di dati distinta. Il tal modo il pacchetto può essere riavviato rieseguendo una sola attività Flusso di dati.  
  
## <a name="configuring-a-package-to-restart"></a>Configurazione di un pacchetto per il riavvio  
 Il file del checkpoint include i risultati dell'esecuzione di tutti i contenitori completati, i valori correnti delle variabili definite dall'utente e di sistema e le informazioni sulla configurazione di pacchetto. Il file include inoltre l'identificatore univoco del pacchetto. Un pacchetto viene riavviato correttamente se l'identificatore contenuto nel file del checkpoint corrisponde effettivamente al pacchetto. In questo modo, un pacchetto non è in grado di utilizzare un file del checkpoint scritto da una versione diversa del pacchetto. Se il pacchetto viene eseguito correttamente, dopo il suo riavvio il file del checkpoint viene eliminato.  
  
 Nella tabella seguente sono elencate le proprietà del pacchetto che è possibile impostare per implementare i checkpoint.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|CheckpointFileName|Specifica il nome del file del checkpoint.|  
|CheckpointUsage|Specifica se i checkpoint vengono utilizzati.|  
|SaveCheckpoints|Indica se il pacchetto salva i checkpoint. Questa proprietà deve essere impostata su True per consentire il riavvio di un pacchetto da un punto di errore.|  
  
 Inoltre, è necessario impostare la proprietà FailPackageOnFailure `true` per tutti i contenitori nel pacchetto che si desidera identificare come punti di riavvio.  
  
 La proprietà ForceExecutionResult consente di testare l'uso dei checkpoint in un pacchetto. Se si imposta la proprietà ForceExecutionResult di un'attività o di un contenitore su Failure, è possibile riprodurre l'errore in tempo reale. Quando si esegue di nuovo il pacchetto, l'attività e i contenitori che hanno avuto esito negativo vengono eseguiti nuovamente.  
  
### <a name="checkpoint-usage"></a>Utilizzo dei checkpoint  
 I possibili valori della proprietà ForceExecutionResult sono i seguenti:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|`Never`|Specifica che il file del checkpoint non viene utilizzato e che il pacchetto viene eseguito dall'inizio del flusso di lavoro.|  
|`Always`|Specifica che il file del checkpoint viene sempre utilizzato e che il pacchetto viene riavviato a partire dal punto in cui si è verificato l'errore. Se il file del checkpoint non viene individuato, il pacchetto ha esito negativo.|  
|`IfExists`|Specifica che il file del checkpoint viene utilizzato, se disponibile. Se il file del checkpoint è disponibile, il pacchetto viene riavviato a partire dal punto in cui si è verificato l'errore. In caso contrario, viene eseguito dall'inizio del flusso di lavoro.|  
  
> [!NOTE]  
>  Il **/CheckPointing sul** opzione di dtexec equivale a impostare il `SaveCheckpoints` proprietà del pacchetto da `True`e il `CheckpointUsage` proprietà su Always. Per altre informazioni, vedere [dtexec Utility](dtexec-utility.md).  
  
## <a name="securing-checkpoint-files"></a>Sicurezza dei file del checkpoint  
 Poiché la protezione a livello di pacchetto non include la protezione dei file del checkpoint, è necessario proteggere tali file separatamente. I dati di checkpoint possono essere archiviati esclusivamente nel file system ed è necessario utilizzare un elenco di controllo di accesso (ACL) del sistema operativo per proteggere il percorso o la cartella in cui è archiviato il file. È importante proteggere i file del checkpoint perché contengono informazioni sullo stato del pacchetto, inclusi i valori correnti delle variabili. Un variabile può ad esempio contenere un recordset con numerose righe di dati privati, quali numeri di telefono. Per altre informazioni, vedere [Accedere ai file usati dai pacchetti](../access-to-files-used-by-packages.md).  
  
### <a name="to-configure-the-checkpoint-properties"></a>Per configurare le proprietà dei checkpoint  
  
-   [Configurazione dei checkpoint per il riavvio di un pacchetto non riuscito](../configure-checkpoints-for-restarting-a-failed-package.md)  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Articolo tecnico [Automatic Restart of SSIS packages after Failover or Failure](https://go.microsoft.com/fwlink/?LinkId=200407)(Riavvio automatico di pacchetti SSIS in caso di failover o errore) nel sito Web social.technet.microsoft.com  
  
-   Articolo del supporto tecnico [SSIS Checkpoints are not honored for For Loop or Foreach Loop container items](https://go.microsoft.com/fwlink/?LinkId=241633)(Mancata applicazione dei checkpoint SSIS per gli elementi contenitori Ciclo For e Foreach) nel sito Web support.microsoft.com.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
