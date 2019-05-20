---
title: Abilitare e disabilitare RDL Sandboxing per Reporting Services in modalità integrata SharePoint | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cc2f32dd81e8dd505b6eaa79359ce10c757ea744
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65577767"
---
# <a name="enable-and-disable-rdl-sandboxing-for-reporting-services-in-sharepoint-integrated-mode"></a>Abilitare e disabilitare RDL Sandboxing per Reporting Services in modalità integrata SharePoint

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

La funzionalità RDL (Report Definition Language) Sandboxing consente di rilevare e limitare l'uso di tipi specifici di risorse in base a singoli tenant in un ambiente in cui più tenant usano una sola Web farm di server di report. Un esempio di questo tipo è rappresentato dai servizi di hosting in cui è possibile gestire una sola Web farm di server di report utilizzati da più tenant e probabilmente da società diverse. L'amministratore del server di report può abilitare questa caratteristica per ottenere gli obiettivi seguenti:  
  
-   Limitare le dimensioni delle risorse esterne. Le risorse esterne includono immagini, file con estensione xslt e dati mappa.  
  
-   Al momento della pubblicazione del report, limitare i tipi e i membri utilizzati nel testo dell'espressione.  
  
-   Al momento dell'elaborazione del report, limitare la lunghezza del testo e le dimensioni del valore restituito per le espressioni.

> [!NOTE]
> L'integrazione di Reporting Services con SharePoint non è più disponibile nelle versioni successive a SQL Server 2016.

 Quando RDL Sandboxing è abilitato, sono disabilitate le caratteristiche seguenti:  
  
-   Codice personalizzato nell'elemento **\<Code>** di una definizione di report.  
  
-   Modalità di compatibilità con le versioni precedenti di RDL per gli elementi di report personalizzati di [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] .  
  
-   Parametri denominati nelle espressioni.  
  
 Questo argomento descrive i singoli componenti dell'elemento \<**RDLSandboxing**> nel file RSReportServer.Config. Per altre informazioni su come modificare questo file, vedere [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Attività dei record del log di traccia del server correlata alla caratteristica RDL Sandboxing. Per altre informazioni sui log di traccia, vedere [Log di traccia del servizio del server di report](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Configurazione di esempio
 L'esempio seguente visualizza le impostazioni e i valori di esempio per l'elemento \<**RDLSandboxing**> nel file RSReportServer.Config.  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace="System.Drawing" AllowNew="True">Bitmap</Allow>  
      <Allow Namespace="TypeConverters.Custom" AllowNew="True">*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```

## <a name="configuration-settings"></a>Impostazioni di configurazione

 Nella tabella seguente sono contenute le informazioni sulle impostazioni di configurazione. Le impostazioni sono elencate nell'ordine in cui vengono visualizzate nel file di configurazione.  
  
|Impostazione|Descrizione|  
|-------------|-----------------|  
|**MaxExpressionLength**|Numero massimo di caratteri consentiti nelle espressioni RDL.<br /><br /> Valore predefinito: 1000|  
|**MaxResourceSize**|Numero massimo di KB consentiti per una risorsa esterna.<br /><br /> Valore predefinito: 100|  
|**MaxStringResultLength**|Numero massimo di caratteri consentiti in un valore restituito per un'espressione RDL.<br /><br /> Valore predefinito: 1000|  
|**MaxArrayResultLength**|Numero massimo di elementi consentiti in un valore restituito della matrice per un'espressione RDL.<br /><br /> Valore predefinito: 100|  
|**Tipi**|Elenco di membri da consentire nelle espressioni RDL.|  
|**Allow**|Tipo o set di tipi da consentire nelle espressioni RDL.|  
|**Namespace**|Attributo per **Allow** che è lo spazio dei nomi contenente uno o più tipi applicabili a Value. Questa proprietà supporta la distinzione tra maiuscole e minuscole.|  
|**AllowNew**|Attributo booleano per **Allow** che controlla se le nuove istanze del tipo possono essere create in espressioni RDL o in un elemento RDL **\<Class>**.<br /><br /> Quando **RDLSandboxing** è abilitato non è possibile creare nuove matrici in espressioni RDL, indipendentemente dall'impostazione di **AllowNew**.|  
|**Value**|Valore per **Allow** che è il nome del tipo da consentire nelle espressioni RDL. Il valore **\*** indica che sono consentiti tutti i tipi nello spazio dei nomi. Questa proprietà supporta la distinzione tra maiuscole e minuscole.|  
|**Membri**|Per l'elenco dei tipi inclusi nell'elemento **\<Types>**, l'elenco dei nomi membro non consentiti nelle espressioni RDL.|  
|**Nega**|Nome di un membro non consentito nelle espressioni RDL. Questa proprietà supporta la distinzione tra maiuscole e minuscole.<br /><br /> Quando per un membro è specificato **Deny** non è consentito nessun membro con questo nome per nessun tipo.|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>Uso delle espressioni con RDL Sandboxing abilitato

È possibile modificare la caratteristica RDL Sandboxing per facilitare la gestione delle risorse utilizzate da un'espressione nelle modalità seguenti:  
  
-   Limitare il numero di caratteri utilizzati per un'espressione.  
  
-   Limitare le dimensioni del risultato restituito da un'espressione.  
  
-   Consentire un elenco specifico di tipi che possono essere utilizzati in un'espressione.  
  
-   Limitare l'elenco dei membri in base al nome per l'elenco dei tipi consentiti che possono essere utilizzati in un'espressione.  
  
-   La caratteristica RDL Sandboxing consente di creare un elenco di tipi approvati e un elenco di membri non autorizzati. L'elenco dei tipi approvati viene denominato elenco consentiti mentre l'elenco di membri non autorizzati viene denominato elenco bloccati.  
  
> [!NOTE]  
>  Nella definizione del report, un computer non può conoscere il tipo di ogni istanza di un riferimento all'espressione. Quando si aggiunge un membro all'elenco bloccati, vengono negati tutti i membri con quel nome in tutti i tipi nell'elenco consentiti.  
  
 I risultati dell'espressione RDL vengono verificati in fase di esecuzione. Le espressioni RDL vengono verificate nella definizione del report durante la pubblicazione di quest'ultimo. Monitorare il log di traccia del server di report relativamente alle violazioni. Per altre informazioni, vedere [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
### <a name="working-with-types"></a>Uso dei tipi

 Quando si aggiunge un tipo all'elenco consentiti, vengono controllati i punti di ingresso seguenti per l'accesso alle espressioni RDL:  
  
-   Membri statici di un tipo.  
  
-   Metodo [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **New** method.  
  
-   Elemento **\<Classes>** nella definizione del report.  
  
-   Membri aggiunti all'elenco bloccati per un tipo nell'elenco consentiti.  
  
 L'elenco consentiti non controlla i punti di ingresso seguenti:  
  
-   Set di dati del report. I campi nei set di dati del report restituiti dalle query potrebbero contenere qualsiasi tipo RDL valido.  
  
-   Parametri di report. I valori dei parametri forniti dall'utente potrebbero contenere qualsiasi tipo RDL valido.  
  
-   Membri di un tipo abilitato non inclusi nell'elenco bloccati. Per impostazione predefinita, vengono abilitati tutti i membri di tutti i tipi nell'elenco consentiti. Quando si aggiunge il nome di un membro all'elenco bloccati, vengono negati tutti i membri con quel nome in tutti i tipi nell'elenco consentiti.  
  
 Per abilitare un membro di un tipo ma negare un membro con lo stesso nome per un tipo diverso, è necessario eseguire le operazioni seguenti:  
  
-   Aggiungere un elemento **\<Deny>** per il nome membro.  
  
-   Creare un membro proxy con un nome diverso in una classe di un assembly personalizzato per il membro che si desidera abilitare.  
  
-   Aggiungere la nuova classe all'elenco consentiti.  
  
 Per aggiungere funzioni .NET Framework di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] all'elenco degli elementi consentiti, aggiungere i tipi corrispondenti dallo spazio dei nomi Microsoft.VisualBasic all'elenco.  
  
 Per aggiungere le parole chiave tipo di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework all'elenco consentiti, aggiungere il tipo CLR corrispondente all'elenco consentiti. Ad esempio, per usare la parola chiave .NET Framework di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] di tipo **Intero** aggiungere il frammento XML seguente all'elemento **\<RDLSandboxing>**:  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 Per aggiungere un tipo che ammette valori Null o un tipo generico .NET Framework di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , è necessario eseguire le operazioni seguenti:  
  
-   Creare un tipo proxy per il tipo generico o che ammette valori Null di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework.  
  
-   Aggiungere il tipo di proxy all'elenco consentiti.  
  
 L'aggiunta di un tipo da un assembly personalizzato all'elenco consentiti non concede in modo implicito autorizzazioni di esecuzione sull'assembly. È necessario modificare in modo specifico il file di sicurezza per l'accesso al codice e fornire autorizzazioni di esecuzione all'assembly. Per altre informazioni, vedere [Sicurezza dall'accesso di codice in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md).  
  
#### <a name="maintaining-the-deny-list-of-members"></a>Gestione dell'elenco di membri \<Deny>

 Quando si aggiunge un nuovo tipo all'elenco consentiti, attenersi all'elenco seguente per determinare quando potrebbe essere necessario aggiornare l'elenco dei membri bloccati:  
  
-   Quando si aggiorna un assembly personalizzato con una versione che introduce nuovi tipi.  
  
-   Quando si aggiungono membri ai tipi nell'elenco consentiti.  
  
-   Quando si aggiorna [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] nel server di report.  
  
-   Quando si aggiorna il server di report a una versione successiva di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Quando si aggiorna un server di report per gestire uno schema RDL successivamente, dal momento che è probabile che nuovi membri siano stati aggiunti ai tipi RDL.  
  
### <a name="working-with-operators-and-new"></a>Uso degli operatori e dell'operatore New

 Per impostazione predefinita, gli operatori di linguaggio .NET Framework di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] sono sempre consentiti, ad eccezione di **New**. L'operatore **New** è controllato dall'attributo **AllowNew** nell'elemento **\<Allow>**. Altri operatori di linguaggio, come l'operatore della funzione di accesso alla raccolta predefinito **!**, e le macro di cast .NET Framework di [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , come **CInt**, sono sempre consentiti.  
  
 L'aggiunta di operatori, inclusi quelli personalizzati, a un elenco bloccati non è supportata. Per escludere operatori per un tipo, è necessario effettuare le operazioni seguenti:  
  
-   Creare un tipo di proxy che non implementa gli operatori che si desidera escludere.  
  
-   Aggiungere il tipo di proxy all'elenco consentiti.  
  
 Per creare una nuova matrice in un'espressione RDL, creare la matrice in un metodo in una classe definita e aggiungere quella classe all'elenco consentiti.  
  
 Per creare una nuova matrice in un'espressione RDL, è necessario eseguire le operazioni seguenti:  
  
-   Definire una nuova classe e creare la matrice in un metodo in quella classe.  
  
-   Aggiungere la classe all'elenco consentiti.  
  
## <a name="see-also"></a>Vedere anche

 [File di configurazione RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Log di traccia del servizio del server di report](../../reporting-services/report-server/report-server-service-trace-log.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
