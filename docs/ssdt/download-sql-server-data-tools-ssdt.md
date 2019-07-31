---
title: Scaricare SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssdt
ms.topic: conceptual
keywords:
- installare ssdt, scaricare ssdt, versione più recente di ssdt
ms.assetid: b0fc4987-d260-4d0a-9dd1-98099835b361
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 62b3db01792005afa7c124f4f31b78cdc350b2dd
ms.sourcegitcommit: 40f3b1f2340098496d8428f50616095a190ae94b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2019
ms.locfileid: "68290342"
---
# <a name="download-and-install-sql-server-data-tools-ssdt-for-visual-studio"></a>Scaricare e installare SQL Server Data Tools (SSDT) per Visual Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


**SQL Server Data Tools** è uno strumento di sviluppo moderno che consente di compilare database relazionali SQL Server, database SQL di Azure, modelli di dati di Analysis Services (AS), pacchetti di Integration Services (IS) e report di Reporting Services (RS). Con SSDT è possibile progettare e distribuire qualsiasi tipo di contenuto SQL Server con la stessa facilità con la quale si sviluppa un'applicazione in Visual Studio.


## <a name="changes-in-ssdt-for-visual-studio-2019"></a>Modifiche in SSDT per Visual Studio 2019 ##

Con Visual Studio 2019, la funzionalità necessarie per abilitare i progetti di Analysis Services, Integration Services e Reporting Services sono state spostate nelle rispettive estensioni di Visual Studio. Le funzionalità principali di SSDT per la creazione di progetti di database sono rimaste incluse in Visual Studio (è necessario selezionare il carico di lavoro Elaborazione ed archiviazione dati durante l'installazione).  Non è richiesta alcuna installazione autonoma di SSDT. 

Se è già disponibile una licenza per Visual Studio 2019:
- Per i progetti di database SQL, installare il carico di lavoro Elaborazione ed archiviazione dati per Visual Studio
- Per i progetti di Analysis Services, Integration Services o Reporting Services, installare le estensioni appropriate dal marketplace

Se non è già disponibile una licenza per Visual Studio 2019:
- Installare [Visual Studio 2019 Community](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_content=sqlssdt) 
- Installare l'estensione Analysis Services, Integration Services o Reporting Services come appropriato

## <a name="changes-in-ssdt-for-visual-studio-2017"></a>Modifiche in SSDT per Visual Studio 2017 ##

A partire da Visual Studio 2017, la funzionalità di creazione di progetti di database è stata integrata nell'installazione di Visual Studio. Non è necessario installare il programma di installazione autonomo di SSDT per l'esperienza principale di SSDT. Per creare progetti di Integration Services o Analysis Services o Reporting Services è ancora necessario il programma di installazione autonomo di SSDT. 

- Per i progetti di database, installare il carico di lavoro Elaborazione ed archiviazione dati per Visual Studio
- Per i progetti di Analysis Services, Integration Services o Reporting Services, scaricare e installare [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-2017)




## <a name="install-ssdt-with-visual-studio-2017"></a>Installare SSDT con Visual Studio 2017

Per installare SSDT durante l'[installazione di Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio), selezionare il carico di lavoro **Elaborazione ed archiviazione dati** e quindi selezionare **SQL Server Data Tools**. Se Visual Studio è già installato, è possibile [modificare l'elenco dei carichi di lavoro](https://docs.microsoft.com/visualstudio/install/modify-visual-studio) per includere SSDT: ![Carico di lavoro Elaborazione ed archiviazione dati](../ssdt/media/download-sql-server-data-tools-ssdt/data-workload.png)

## <a name="install-analysis-services-integration-services-and-reporting-services-tools"></a>Installare Analysis Services, Integration Services e Reporting Services

Per installare AS, IS ed RS come supporto per i progetti, eseguire il [programma di installazione di SSDT autonomo](#ssdt-for-vs-2017-standalone-installer). 

Il programma di installazione elenca le istanze di Visual Studio disponibili per l'aggiunta degli strumenti di SSDT. Se Visual Studio non è installato, selezionando **Install a new SQL Server Data Tools instance** (Installa una nuova istanza di SQL Server Data Tools) è possibile installare SSDT con una versione minima di Visual Studio. Per un'esperienza ottimale, tuttavia, è consigliabile usare SSDT con [la versione più recente di Visual Studio](https://www.visualstudio.com/downloads). 

![Selezionare AS, IS, RS](../ssdt/media/download-sql-server-data-tools-ssdt/select-services.png)



## <a name="ssdt-for-vs-2017-standalone-installer"></a>SSDT per Visual Studio 2017 (programma di installazione autonomo)

[![download](../ssdt/media/download.png) Download di SSDT per Visual Studio 2017 (15.9.2)](https://go.microsoft.com/fwlink/?linkid=2095463) 

> [!IMPORTANT]
> - Prima di installare SSDT per Visual Studio 2017 (15.9.2), disinstallare le estensioni *Progetti di Analysis Services* e *Progetti di Reporting Services*, se già installate, e chiudere tutte le istanze di Visual Studio.
> - Usare SSDT per Visual Studio 2017 (15.8.0) o versioni precedenti per la progettazione di pacchetti SSIS contenenti un'origine o una destinazione Teradata. Le versioni di SSDT per Visual Studio 2017 successive alla 15.8.0 non consentono di progettare pacchetti SSIS contenenti origine/destinazione Teradata di Attunity.


**Informazioni sulla versione**  
  
Numero di versione: 15.9.2  
Numero di build: 14.0.16194.0  
Data di rilascio: 17 luglio 2019  

Per un elenco completo delle modifiche, vedere [Note sulla versione per SQL Server Data Tools (SSDT)](release-notes-ssdt.md).

SSDT per Visual Studio 2017 ha gli stessi [requisiti di sistema](https://docs.microsoft.com/visualstudio/productinfo/vs2017-system-requirements-vs) di Visual Studio.  

### <a name="available-languages---ssdt-for-vs-2017"></a>Lingue disponibili - SSDT per VS 2017

Questa versione di **SSDT per VS 2017** può essere installata nelle lingue seguenti:

- [Cinese semplificato]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x804)
- [Cinese tradizionale]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x404)
- [Inglese (Stati Uniti)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x409)
- [Francese]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x40c)
- [Tedesco]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x407)
- [Italiano]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x410)
- [Giapponese]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x411)
- [Coreano]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x412)
- [Portoghese (Brasile)]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x416)
- [Russo]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x419)
- [Spagnolo]( https://go.microsoft.com/fwlink/?linkid=2095463&clcid=0x40a)

## <a name="offline-install"></a>Eseguire l'installazione offline

Per installare SSDT quando non si è connessi a Internet, seguire la procedura descritta in questa sezione. Per altre informazioni, vedere [Creare un'installazione di rete di Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/create-a-network-installation-of-visual-studio).

Per prima cosa, completare la procedura seguente mentre si è connessi:

1. [Scaricare il programma di installazione autonomo di SSDT](#ssdt-for-vs-2017-standalone-installer).
2. [Scaricare vs_sql.exe](https://aka.ms/vs/15/release/vs_sql.exe).
3. Mentre si è ancora online, eseguire uno dei comandi seguenti per scaricare tutti i file necessari per l'installazione offline. L'uso dell'opzione `--layout` è fondamentale, scaricherà i file effettivi per l'installazione offline. Sostituire `<filepath>` con il tracciato di layout effettivo in cui salvare i file.

   
   A.   Per una lingua specifica, passare le impostazioni locali: `vs_sql.exe --layout c:\<filepath> --lang en-us` (una sola lingua corrisponde a circa 1 GB)  
   B. Per tutte le lingue, omettere l'argomento `--lang`: `vs_sql.exe --layout c:\<filepath>` (tutte le lingue corrispondono a circa 3,9 GB).

4. Eseguire `SSDT-Setup-ENU.exe /layout c:\<filepath>` per estrarre il payload SSDT nella stessa posizione `<filepath>` in cui sono stati scaricati i file di VS2017. Ciò garantisce che tutti i file di entrambe le cartelle vengano combinati in una cartella di layout singola.

Dopo aver completato questa procedura, quanto segue può essere eseguito offline:

1. Eseguire `vs_setup.exe --NoWeb` per installare la shell di Visual Studio 2017 e il progetto di dati di SQL Server.
2. Dalla cartella di layout eseguire `SSDT-Setup-ENU.exe /install` e selezionare SSIS/SSRS/SSAS.

   - Oppure, per un'installazione automatica, eseguire `SSDT-Setup-ENU.exe /INSTALLALL[:vsinstances] /passive`  

Per le opzioni disponibili, eseguire `SSDT-Setup-ENU.exe /help`

> [!NOTE]
> Se si usa una versione completa di Visual Studio 2017, creare una cartella offline solo per SSDT e quindi eseguire `SSDT-Setup-ENU.exe` da questa nuova cartella (non aggiungere SSDT a un altro layout offline di Visual Studio 2017). Se si aggiunge il layout SSDT a un layout offline di Visual Studio esistente, i componenti di runtime necessari (exe) non vengono creati in tale layout.

## <a name="supported-sql-versions"></a>Versioni di SQL supportate
  
|Modelli di progetto|Piattaforme SQL supportate|  
|-------------------|--------------------|  
|Database relazionali|  SQL Server 2005\* - SQL Server 2017<br> (usare SSDT 17.x o SSDT per Visual Studio 2017 per la connessione a [SQL Server in Linux](../linux/sql-server-linux-overview.md))<br /><br />Database SQL di Azure<br /><br />Azure SQL Data Warehouse (supporta solo query, i progetti di database non sono ancora supportati)<br /><br /> \* Il supporto per SQL Server 2005 è deprecato<br /><br /> e si consiglia di passare a una versione di SQL supportata ufficialmente|
|Modelli di Analysis Services<br /><br />Report di Reporting Services | SQL Server 2008 - SQL Server 2017|
|pacchetti di Integration Services| SQL Server 2012 - SQL Server 2019 |
  
## <a name="dacfx"></a>DacFx

Sia SSDT per Visual Studio 2015 che SSDT per Visual Studio 2017 usano DacFx 17.4.1: [Download del framework applicazione livello dati (DacFx) 17.4.1](https://www.microsoft.com/download/details.aspx?id=56508).

## <a name="previous-versions"></a>Versioni precedenti

Per scaricare e installare SSDT per Visual Studio 2015 o una versione precedente di SSDT, vedere [Versioni precedenti di SQL Server Data Tools (SSDT e SSDT-BI)](previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md).

## <a name="next-steps"></a>Passaggi successivi

Dopo l'installazione di SSDT, consultare queste esercitazioni per imparare a creare database, pacchetti, modelli di dati e report mediante SSDT:  

- [Sviluppo di database offline orientato ai progetti](project-oriented-offline-database-development.md)  
- [Esercitazione SSIS: Creare un pacchetto ETL semplice](../integration-services/ssis-how-to-create-an-etl-package.md)  
- [Esercitazioni su Analysis Services](../analysis-services/analysis-services-tutorials-ssas.md)  
- [Creare un report tabella semplice (esercitazione su SSRS)](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="see-also"></a>Vedere anche

[Forum MSDN di SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog del Team di SSDT](https://blogs.msdn.com/b/ssdt/)  
[Riferimento all'API DACFx](https://msdn.microsoft.com/library/dn645454.aspx)  
[Scaricare SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
