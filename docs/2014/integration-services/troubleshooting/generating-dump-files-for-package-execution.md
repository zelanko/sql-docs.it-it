---
title: Generazione di file di dump per l'esecuzione del pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 61ef1731-cb3a-4afb-b4a4-059b04aeade0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8022532dcb038b7c9a5839acb0541337ac3d5001
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766150"
---
# <a name="generating-dump-files-for-package-execution"></a>Generazione di file di dump per l'esecuzione del pacchetto
  In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]è possibile creare file di dump del debug contenenti informazioni sull'esecuzione di un pacchetto. Tramite le informazioni di questi file, è possibile risolvere i problemi di esecuzione dei pacchetti.  
  
> [!NOTE]  
>  I file di dump del debug possono contenere informazioni sensibili. Per proteggere tali informazioni, è possibile utilizzare un elenco di controllo di accesso per limitare l'accesso ai file oppure copiare i file in una cartella con accesso limitato. Ad esempio, prima di inviare i file del debug ai servizi di supporto [!INCLUDE[msCoName](../../includes/msconame-md.md)] , è consigliabile rimuovere eventuali informazioni sensibili o riservate.  
  
 Quando si distribuisce un progetto al server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è possibile creare file di dump in cui sono fornite informazioni sull'esecuzione dei pacchetti contenuti nel progetto. Al termine del processo ISServerExec.exe, vengono creati i file di dump. È possibile specificare che un file di dump venga creato quando si verificano errori durante l'esecuzione del pacchetto, selezionando l'opzione **Dump su errori** nella finestra di dialogo **Esegui pacchetto** . È inoltre possibile utilizzare le seguenti stored procedure:  
  
-   [catalog.set_execution_parameter_value &#40;database SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
     Chiamare questa stored procedure per configurare la creazione di un file di dump quando si verifica qualsiasi errore o evento e quando si verificano eventi specifici, durante l'esecuzione di un pacchetto.  
  
-   [catalog.create_execution_dump](/sql/integration-services/system-stored-procedures/catalog-create-execution-dump)  
  
     Chiamare questa stored procedure per interrompere un pacchetto in esecuzione e creare un file di dump.  
  
 Se si distribuiscono pacchetti usando il modello di distribuzione del pacchetto, si creano i file di dump del debug usando l'utilità **dtexec** o **dtutil** per specificare un'opzione di dump del debug nella riga di comando. Per altre informazioni, vedere [Utilità dtexec](../packages/dtexec-utility.md) e [Utilità til dtutil](../dtutil-utility.md). Per ulteriori informazioni sul modello di distribuzione del pacchetto, vedere [distribuzione di progetti e pacchetti](../packages/deploy-integration-services-ssis-projects-and-packages.md) e distribuzione di pacchetti [&#40;&#41;SSIS ](../packages/legacy-package-deployment-ssis.md).  
  
## <a name="debug-dump-file-format"></a>Formato del file di dump del debug  
 Quando si specifica un'opzione di dump del debug, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea i file di dump del debug seguenti:  
  
-   File di dump del debug con estensione mdmp. Si tratta di un file binario.  
  
-   File di dump del debug con estensione tmp. Si tratta di un file in formato testo.  
  
 Per impostazione predefinita [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , archivia questi file nella cartella, * \<unità>:* \Programmi\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
 Nella tabella seguente sono descritte solo determinate sezioni del file con estensione tmp. Il file tmp include altri dati non riportati nella tabella.  
  
|Tipo di informazione|Descrizione|Esempio|  
|-------------------------|-----------------|-------------|  
|Environment|Versione del sistema operativo, dati di utilizzo della memoria, ID del processo e nome immagine del processo. Le informazioni sull'ambiente sono riportate all'inizio del file tmp.|# SSIS Textual Dump taken at 9/13/2007 1:50:34 PM<br /><br /> #PID 4120<br /><br /> #Image Name [C:\Program Files\Microsoft SQL Server\110\DTS\Binn\DTExec.exe]<br /><br /> # OS major=6 minor=0 build=6000<br /><br /> # Running on 2 amd64 processors under WOW64<br /><br /> # Memory: 58% in use. Physical: 845M/2044M  Paging: 2404M/4095M (avail/total)|  
|Percorso e versione delle librerie a collegamento dinamico (DLL)|Percorso e numero di versione di ogni DLL caricata nel sistema durante l'elaborazione di un pacchetto.|# Loaded Module: c:\bb\Sql\DTS\src\bin\debug\i386\DTExec.exe (10.0.1069.5)<br /><br /> # Loaded Module: C:\Windows\SysWOW64\ntdll.dll (6.0.6000.16386)<br /><br /> # Loaded Module: C:\Windows\syswow64\kernel32.dll (6.0.6000.16386)|  
|Messaggi recenti|Messaggi recenti emessi dal sistema. Sono inclusi l'ora, il tipo, la descrizione e l'ID thread di ogni messaggio.|[M:1]   Ring buffer entry:              (*pRecord)<br /><br /> [D:2]      <<\<CRingBufferLogging::RingBufferLoggingRecord>>> ( \@ 0282F1A8 )<br /><br /> [E:3]         Time Stamp: 2007-09-13 13:50:32.786      (szTimeStamp)<br /><br /> [E:3]         Thread ID: 2368           (ThreadID)<br /><br /> [E:3]         Event Name: OnError                        (EventName)<br /><br /> [E:3]         Source Name:                (SourceName)<br /><br /> [E:3]         Source ID:                        (SourceID)<br /><br /> [E:3]         Execution ID:                 (ExecutionGUID)<br /><br /> [E:3]         Data Code: -1073446879              (DataCode)<br /><br /> [E:3]         Description: The component is missing, not registered, not upgradeable, or missing required interfaces. Informazioni di contatto per il componente: "".|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Execute Package Dialog Box](../execute-package-dialog-box.md)  
  
  
