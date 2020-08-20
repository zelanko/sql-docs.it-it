---
description: Variabili di sistema
title: Variabili di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], variables
- tasks [Integration Services], variables
- system variables [Integration Services]
- event handlers [Integration Services], variables
- variables [Integration Services], system
ms.assetid: efecd0d4-1489-4eba-a8fe-275d647058b8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 913345034da936d6ed7a0c9ea3678c427b4f34ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495319"
---
# <a name="system-variables"></a>Variabili di sistema

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include un set di variabili di sistema in cui vengono archiviate informazioni sui pacchetti in esecuzione e sui relativi oggetti. Tali variabili possono essere utilizzate nelle espressioni e nelle espressioni di proprietà per personalizzare pacchetti, contenitori, attività e gestori di eventi.  
  
 È possibile usare tutte le variabili, di sistema e definite dall'utente, nelle associazioni di parametro usate dall'attività Esegui SQL per il mapping delle variabili ai parametri.  
  
## <a name="system-variables-for-packages"></a>Variabili di sistema per i pacchetti  
 Nella tabella seguente vengono descritte le variabili di sistema disponibili in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per i pacchetti.  
  
|Variabile di sistema|Tipo di dati|Descrizione|  
|---------------------|---------------|-----------------|  
|**CancelEvent**|Int32|Handle di un oggetto Eventi di Windows che l'attività può segnalare per indicare che l'attività deve essere arrestata.|  
|**ContainerStartTime**|Datetime|Ora di inizio del contenitore.|  
|**CreationDate**|Datetime|Data di creazione del pacchetto.|  
|**CreatorComputerName**|string|Computer in cui è stato creato il pacchetto.|  
|**CreatorName**|string|Nome dell'utente che ha compilato il pacchetto.|  
|**ExecutionInstanceGUID**|string|Identificatore univoco dell'istanza di esecuzione di un pacchetto.|  
|**FailedConfigurations**|string|Nomi di configurazioni di pacchetti non riuscite.|  
|**IgnoreConfigurationsOnLoad**|Boolean|Indica se le configurazioni di pacchetti vengono ignorate in fase di caricamento del pacchetto.|  
|**InteractiveMode**|Boolean|Indica se il pacchetto viene eseguito in modalità interattiva. Se un pacchetto viene eseguito in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , questa proprietà viene impostata su **True**. Se un pacchetto viene eseguito con l'utilità del prompt dei comandi **DTExec** , la proprietà viene impostata su **False**.|  
|**LocaleId**|Int32|Impostazioni locali utilizzate dal pacchetto.|  
|**MachineName**|string|Nome del computer in cui viene eseguito il pacchetto.|  
|**OfflineMode**|Boolean|Indica se il pacchetto è in modalità offline. La modalità offline non acquisisce connessioni a origini dei dati.|  
|**PackageID**|string|Identificatore univoco del pacchetto.|  
|**PackageName**|string|Nome del pacchetto.|  
|**StartTime**|Datetime|Data e ora di inizio dell'esecuzione del pacchetto.|  
|**ServerExecutionID**|Int64|ID dell'esecuzione per il pacchetto eseguito nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .<br /><br /> Il valore predefinito è zero. Il valore viene modificato solo se il pacchetto viene eseguito da ISServerExec sul server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Quando è presente un pacchetto figlio, il valore viene passato dal pacchetto padre a quello figlio.|  
|**UserName**|string|Nome dell'account dell'utente che ha avviato il pacchetto. Il nome utente è qualificato dal nome del dominio.|  
|**VersionBuild**|Int32|Versione del pacchetto.|  
|**VersionComment**|string|Commenti sulla versione del pacchetto.|  
|**VersionGUID**|string|Identificatore univoco della versione.|  
|**VersionMajor**|Int32|Versione principale del pacchetto.|  
|**VersionMinor**|Int32|Versione secondaria del pacchetto.|  
  
## <a name="system-variables-for-containers"></a>Variabili di sistema per i contenitori  
 La tabella seguente descrive le variabili di sistema disponibili in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per i contenitori Ciclo For, Ciclo Foreach e Sequenza.  
  
|Variabile di sistema|Tipo di dati|Descrizione|Contenitore|  
|---------------------|---------------|-----------------|---------------|  
|**LocaleId**|Int32|Impostazioni locali utilizzate dal contenitore.|Contenitore Ciclo For<br /><br /> Contenitore Ciclo Foreach<br /><br /> Sequenza - contenitore|  
  
## <a name="system-variables-for-tasks"></a>Variabili di sistema per le attività  
 Nella tabella seguente vengono descritte le variabili di sistema disponibili in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per le attività.  
  
|Variabile di sistema|Tipo di dati|Descrizione|  
|---------------------|---------------|-----------------|  
|**CreationName**|string|Nome dell'attività.|  
|**LocaleId**|Int32|Impostazioni locali utilizzate dall'attività.|  
|**TaskID**|string|Identificativo univoco di un'istanza dell'attività.|  
|**TaskName**|string|Nome dell'istanza dell'attività.|  
|**TaskTransactionOption**|Int32|Opzioni di transazione utilizzate dall'attività.|  
  
## <a name="system-variables-for-event-handlers"></a>Variabili di sistema per i gestori di eventi  
 Nella tabella seguente vengono descritte le variabili di sistema disponibili in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per i gestori di eventi. Non tutte le variabili sono disponibili per tutti i gestori di eventi.  
  
|Variabile di sistema|Tipo di dati|Descrizione|Gestore di evento|  
|---------------------|---------------|-----------------|-------------------|  
|**Annulla**|Boolean|Indica se l'esecuzione del gestore di evento viene arrestata in caso di errore, avviso o annullamento della query.|Gestore dell'evento OnError<br /><br /> Gestore dell'evento OnWarning<br /><br /> Gestore dell'evento OnQueryCancel|  
|**ErrorCode**|Int32|Identificatore dell'errore.|Gestore dell'evento OnError<br /><br /> Gestore dell'evento OnInformation<br /><br /> Gestore dell'evento OnWarning|  
|**ErrorDescription**|string|Descrizione dell'errore.|Gestore dell'evento OnError<br /><br /> Gestore dell'evento OnInformation<br /><br /> Gestore dell'evento OnWarning|  
|**ExecutionStatus**|Boolean|Stato di esecuzione corrente.|Gestore dell'evento OnExecStatusChanged|  
|**ExecutionValue**|DBNull|Valore di esecuzione.|Gestore dell'evento OnTaskFailed|  
|**LocaleId**|Int32|Impostazioni locali utilizzate dal gestore di evento.|Tutti i gestori di eventi|  
|**PercentComplete**|Int32|Percentuale di avanzamento dell'operazione.|Gestore dell'evento OnProgress|  
|**ProgressCountHigh**|Int32|Parte più significativa di un valore a 64 bit che indica il numero totale delle operazioni elaborate dall'evento OnProgress.|Gestore dell'evento OnProgress|  
|**ProgressCountLow**|Int32|Parte meno significativa di un valore a 64 bit che indica il numero totale delle operazioni elaborate dall'evento OnProgress.|Gestore dell'evento OnProgress|  
|**ProgressDescription**|string|Descrizione dell'avanzamento.|Gestore dell'evento OnProgress|  
|**Propagate**|Boolean|Indica se l'evento viene propagato a un gestore di evento di livello superiore.<br /><br /> Nota: il valore della variabile **Propagate** viene ignorato durante la convalida del pacchetto. Se si imposta **Propagate** su **False** in un pacchetto figlio, ciò non impedisce la propagazione di un evento fino al pacchetto padre.|Tutti i gestori di eventi|  
|**SourceDescription**|string|Descrizione dell'eseguibile nel gestore di evento che ha generato l'evento.|Tutti i gestori di eventi|  
|**SourceID**|string|Identificatore univoco dell'eseguibile nel gestore di evento che ha generato l'evento.|Tutti i gestori di eventi|  
|**SourceName**|string|Nome dell'eseguibile nel gestore di evento che ha generato l'evento.|Tutti i gestori di eventi|  
|**VariableDescription**|string|Descrizione della variabile.|Gestore dell'evento OnVariableValueChanged|  
|**VariableID**|string|Identificatore univoco della variabile.|Gestore dell'evento OnVariableValueChanged|  
  
## <a name="system-variables-in-parameter-bindings"></a>Variabili di sistema nelle associazioni di parametro  
 È spesso consigliabile salvare in tabelle i valori delle variabili di sistema dopo l'esecuzione di un pacchetto. Si consideri ad esempio un pacchetto che crea dinamicamente una tabella e scrive in una colonna della tabella il GUID dell'istanza di esecuzione del pacchetto che ha creato la tabella.  
  
 Se si utilizzano variabili di sistema per eseguire il mapping dei parametri inclusi nell'istruzione SQL utilizzata da un'attività Esegui SQL, è importante impostare il tipo di dati di ogni associazione di parametro sul tipo di dati della variabile di sistema. In caso contrario i valori delle variabili di sistema potrebbero essere convertiti in modo errato. Se ad esempio la variabile di sistema **ExecutionInstanceGUID** , che ha tipo di dati string e contiene una stringa che rappresenta il GUID dell'istanza in esecuzione di un pacchetto, viene usata nell'associazione di un parametro con tipo di dati GUID, il GUID dell'istanza del pacchetto non verrà convertito correttamente.  
  
 Questa regola vale anche per le variabili definite dall'utente ma, mentre i tipi di dati delle variabili di sistema non possono essere modificati ed è necessario adattare l'utilizzo di tali variabili in base ai relativi tipi di dati, le variabili definite dall'utente sono molto più flessibili. Le variabili definite dall'utente utilizzate nelle associazioni di parametro vengono in genere definite con tipi di dati compatibili con quelli dei parametri a cui è stato eseguito il mapping.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Mapping di parametri di query a variabili in un'attività Esegui SQL](https://msdn.microsoft.com/library/6a164349-dfcf-4995-80bc-d4e7aee52a83)  
  
  
