---
title: Supportare più destinazioni in componenti personalizzati | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ec611374-16bf-4a56-8fd9-45d3ddd7befc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 91524408998df8be0df4ee5d4ede0b641dbaa2a4
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71287223"
---
# <a name="support-multi-targeting-in-your-custom-components"></a>Supportare più destinazioni in componenti personalizzati

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 È ora possibile usare Progettazione SSIS in SQL Server Data Tools (SSDT) per creare, gestire ed eseguire pacchetti destinati a SQL Server 2016, SQL Server 2014 o SQL Server 2012. Per ottenere SSDT per Visual Studio 2015, vedere [Scaricare la versione più recente di SQL Server Data Tools](../../ssdt/download-sql-server-data-tools-ssdt.md). 

 In Esplora soluzioni fare clic con il pulsante destro del mouse su un progetto di Integration Services e scegliere **Proprietà** per aprire le pagine delle proprietà per il progetto. Nella scheda **Generale** di **Proprietà di configurazione**selezionare la proprietà **TargetServerVersion** , quindi scegliere SQL Server 2016, SQL Server 2014 o SQL Server 2012.  
   
 ![Proprietà TargetServerVersion nella finestra di dialogo Proprietà progetto](../../integration-services/media/targetserverversion2.png "Proprietà TargetServerVersion nella finestra di dialogo Proprietà progetto")  
 
 ## <a name="multiple-version-support-and-multi-targeting-for-custom-components"></a>Supporto di più versioni e destinazioni per i componenti personalizzati
 
Tutti e cinque i tipi di estensioni personalizzate di SSIS supportano più destinazioni.
-   Gestioni connessioni
-   Attività
-   Enumerators
-   Provider di log
-   Componenti del flusso di dati

Per le estensioni gestite, la finestra di progettazione SSIS carica la versione dell'estensione per la versione di destinazione specificata. Ad esempio:
-   Quando la versione di destinazione è SQL Server 2012, la finestra di progettazione carica la versione 2012 dell'estensione.
-   Quando la versione di destinazione è SQL Server 2016, la finestra di progettazione carica la versione 2016 dell'estensione.

Le estensioni COM non supportano più destinazioni. La finestra di progettazione SSIS carica sempre l'estensione COM per la versione corrente di SQL Server, indipendentemente dalla versione di destinazione specificata.

## <a name="add-basic-support-for-multiple-versions-and-multi-targeting"></a>Aggiungere il supporto di base per più versioni e destinazioni

Per linee guida di base, vedere [Getting your SSIS custom extensions to be supported by the multi-version support of SSDT 2015 for SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/) (Ottenere estensioni SSIS personalizzate supportate da più versioni di SSDT 2015 per SQL Server 2016). In questo post di blog vengono descritti i passaggi o requisiti seguenti.

-   Distribuire gli assembly nelle cartelle appropriate.

-   Creare un file di mapping delle estensioni per SQL Server 2014 e versioni successive.

## <a name="add-code-to-switch-versions"></a>Aggiungere il codice per passare da una versione all'altra

### <a name="switch-versions-in-a-custom-connection-manager-task-enumerator-or-log-provider"></a>Passare da una versione all'altra in una gestione connessione, attività, enumeratore o provider di log personalizzati

Per una gestione connessione, attività, enumeratore o provider di log personalizzati, aggiungere logica di downgrade nel metodo **SaveToXML**.

```csharp
public void SaveToXML(XmlDocument doc, IDTSInfoEvents events)
{
    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
    }

    if (TargetServerVersion == DTSTargetServerVersion.SQLServer2012)
    {
         // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
    }
}
```

### <a name="switch-versions-in-a-custom-data-flow-component"></a>Passare da una versione all'altra in un componente flusso di dati personalizzato

Per una gestione connessione, attività, enumeratore o provider di log personalizzati, aggiungere logica di downgrade nel nuovo metodo **PerformDowngrade**.

```csharp
public override void PerformDowngrade(int pipelineVersion, DTSTargetServerVersion targetServerVersion)
{
    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2014)
    {
        // Add logic to downgrade from SQL Server 2016 to SQL Server 2014.
        ComponentMetaData.Version = 8;
    }

    if (targetServerVersion == DTSTargetServerVersion.DTSTSV_SQLSERVER2012)
    {
          // Add logic to downgrade from SQL Server 2016 to SQL Server 2012.
        ComponentMetaData.Version = 6;
    }
}
```

## <a name="common-errors"></a>Errori comuni

### <a name="invalidcastexception"></a>InvalidCastException

**Messaggio di errore** Impossibile eseguire il cast dell'oggetto COM di tipo 'System.__ComObject' al tipo di interfaccia 'Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100'. Questa operazione non è riuscita perché la chiamata QueryInterface sul componente COM per l'interfaccia con IID '{BE8C48A3-155B-4810-BA5C-BDF68A659E9E}' non è riuscita a causa dell'errore seguente: interfaccia non supportata (eccezione da HRESULT: 0x80004002 (E_NOINTERFACE)). (Microsoft.SqlServer.DTSPipelineWrap).

**Soluzione.** Se l'estensione personalizzata fa riferimento ad assembly di interoperabilità di SSIS, ad esempio Microsoft.SqlServer.DTSPipelineWrap o Microsoft.SqlServer.DTSRuntimeWrap, impostare il valore della proprietà **Incorpora tipi di interoperabilità** su **False**.

![Incorpora tipi di interoperabilità](../../integration-services/extending-packages-custom-objects/media/embed-interop-types.png)

### <a name="unable-to-load-some-types-when-target-version-is-sql-server-2012"></a>Impossibile caricare alcuni tipi quando la versione di destinazione è SQL Server 2012

Questo problema interessa determinati tipi, ad esempio IErrorReportingService o IUserPromptService.

**Messaggio di errore (esempio).** Impossibile caricare il tipo 'Microsoft.DataWarehouse.Design.IErrorReportingService' dall'assembly 'Microsoft.DataWarehouse, Version=13.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91'.

**Soluzione alternativa.** Usare un elemento MessageBox anziché queste interfacce quando la versione di destinazione è SQL Server 2012.

