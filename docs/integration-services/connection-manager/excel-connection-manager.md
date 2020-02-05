---
title: Gestione connessione Excel | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f9ce3042bedd23c5ee173b1df7669a09cce35351
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "75831758"
---
# <a name="excel-connection-manager"></a>Gestione connessione Excel

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione Excel consente la connessione di un pacchetto a un file di cartella di lavoro di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. L'origine e la destinazione Excel disponibili in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usano la gestione connessione Excel.  
 
> [!IMPORTANT]
> Per informazioni dettagliate sulla connessione ai file di Excel e sulle limitazioni e i problemi noti per il caricamento di dati da o a file di Excel, vedere [Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

 Quando si aggiunge una gestione connessione Excel a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione Excel, imposta le proprietà della gestione connessione, quindi la aggiunge alla raccolta **Connessioni** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **EXCEL**.  
  
## <a name="configure-the-excel-connection-manager"></a>Configurare la gestione connessione Excel  
 Per configurare la gestione connessione Excel, procedere nel modo seguente:  
  
-   Specificare il percorso del file della cartella di lavoro di Excel.  
  
-   Specificare la versione di Excel utilizzata per creare il file.  
  
-   Indicare se la prima riga nei fogli di lavoro o negli intervalli selezionati contiene i nomi delle colonne.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="excel-connection-manager-editor"></a>Editor gestione connessione Excel
  Usare la finestra di dialogo **Editor gestione connessione Excel**per aggiungere una connessione a un file di cartella di lavoro di [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] nuovo o esistente.  
  
### <a name="options"></a>Opzioni  
 **Percorso file di Excel**  
 Consente di digitare il percorso e il nome del file di una cartella di lavoro di Excel nuova o esistente.  
   
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per passare alla cartella che contiene il file di Excel o in cui creare il nuovo file.  
  
 **Versione di Excel**  
 Consente di specificare la versione di Microsoft Excel utilizzata per creare il file.  
  
 **Nomi di colonna nella prima riga**  
 Consente di specificare se la prima riga di dati del foglio di lavoro selezionato contiene nomi di colonna. Il valore predefinito di questa opzione è **True**.  

## <a name="solution-to-import-data-with-mixed-data-types-from-excel"></a>Soluzione per importare dati con tipi di dati misti da Excel

Se si usano dati che contengono tipi di dati misti, per impostazione predefinita il driver Excel legge le prime 8 righe configurate dalla chiave di registro **TypeGuessRows**. In base alle prime 8 righe di dati, il driver Excel tenta di indovinare il tipo di dati di ogni colonna. Si supponga ad esempio che l'origine dati di Excel includa numeri e testo in una colonna. Se le prime 8 righe contengono numeri, il driver potrebbe determinare in base a tali prime 8 righe che i dati della colonna siano di tipo Integer. In questo caso SSIS ignorerà i valori di testo e li importerà come NULL nella destinazione.

Per risolvere questo problema, è possibile provare una delle soluzioni seguenti:

* Modificare il tipo di colonna di Excel in **Testo** nel file di Excel.
* Aggiungere la proprietà estesa IMEX alla stringa di connessione per eseguire l'override del comportamento predefinito del driver. Quando si aggiunge la proprietà estesa ";IMEX=1" alla fine della stringa di connessione, Excel considera tutti i dati come testo. Vedere l'esempio seguente:
    
  ```ACE OLEDB connection string:
  Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\ExcelFileName.xlsx;Extended Properties="EXCEL 12.0 XML;HDR=YES;IMEX=1";
  ```

   Affinché questa soluzione funzioni in modo affidabile, potrebbe essere necessario modificare anche le impostazioni del Registro di sistema. Il file main.cmd è il seguente:
  
   ```cmd
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\12.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\14.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\15.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\16.0\Access Connectivity Engine\Engines\Excel" /t REG_DWORD /v TypeGuessRows /d 0 /f
   ```

* Salvare il file in formato CSV e modificare il pacchetto SSIS per supportare un'importazione CSV.

## <a name="related-tasks"></a>Attività correlate  
[Caricare i dati da o in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
[Origine Excel](../data-flow/excel-source.md)  
[Destinazione Excel](../data-flow/excel-destination.md)
