---
title: Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57fe740bdd02c96eb21994f5996c734620793616
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079834"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato (SharePoint 2013)
  In questo argomento vengono illustrate l'esperienza utente relativamente alle cartelle di lavoro create in ambienti di PowerPivot precedenti e la modalità di aggiornamento delle cartelle di lavoro di PowerPivot in modo che sia possibile avvalersi delle nuove funzionalità introdotte in questa versione. Per ulteriori informazioni sulle nuove funzionalità, vedere Novità di [PowerPivot](https://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  Non è possibile eseguire il rollback dell'aggiornamento per cartelle di lavoro aggiornate automaticamente nel server. Una volta aggiornata, una cartella di lavoro rimane in questo stato. Per utilizzare una versione precedente, è possibile ripubblicare la cartella di lavoro precedente in SharePoint, ripristinare una versione precedente oppure riciclare la cartella di lavoro. Per ulteriori informazioni sul ripristino o riciclo di un documento in SharePoint, vedere [Pianificare di proteggere il contenuto tramite i Cestini e il controllo delle versioni](https://go.microsoft.com/fwlink/?LinkId=238669).  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Panoramica dell'aggiornamento delle cartelle di lavoro](#bkmk_overview)  
  
-   [Aggiornamento alle cartelle di lavoro di SQL Server 2012 Service Pack 1 (SP1) da cartelle di lavoro di 2008 R2](#bkmk_to_2012sp1_from_2008r2)  
  
-   [Eseguire l'aggiornamento a cartelle di lavoro di Office 2013 da versioni create tramite il componente aggiuntivo SQL Server 2012 PowerPivot per Excel](#bkmk_to_2012sp1_from_2012)  
  
-   [Eseguire l'aggiornamento a cartelle di lavoro di SQL Server 2012 da versioni create tramite il componente aggiuntivo SQL Server 2008 R2 PowerPivot per Excel 2010](#bkmk_to_2012_from_2008R2)  
  
-   [Esecuzione di più versioni di cartelle di lavoro in un server più recente](#bkmk_runold)  
  
##  <a name="bkmk_overview"></a>Panoramica dell'aggiornamento delle cartelle di lavoro  
 Una cartella di lavoro di PowerPivot è una cartella di lavoro di Excel contenente dati PowerPivot incorporati. L'aggiornamento di una cartella di lavoro offre due vantaggi:  
  
-   Utilizzo di nuove funzionalità in [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Abilitazione dell'aggiornamento dati pianificato per cartelle di lavoro che vengono eseguite con un server [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services in modalità SharePoint.  
  
> [!IMPORTANT]  
>  Non è possibile eseguire il rollback di una cartella di lavoro aggiornata, pertanto assicurarsi di effettuare una copia del file se si desidera utilizzarlo nella versione precedente di [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]o in una versione precedente di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 Nella tabella seguente sono elencati il supporto e il comportamento delle cartelle di lavoro di PowerPivot in base all'ambiente in cui è stata creata la cartella di lavoro. Nel comportamento descritto sono inclusi l'esperienza utente generale, le opzioni di aggiornamento supportate per aggiornare la cartella di lavoro all'ambiente specifico e il comportamento dell'aggiornamento dati pianificato di una cartella di lavoro che non è stata ancora aggiornata.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Opzioni di aggiornamento e comportamento della cartella di lavoro  
  
|Data creazione|\<|Supporto e comportamento|>|  
|----------------|--------|--------------------------|--------|  
||**SQL Server 2008 R2 PowerPivot per SharePoint 2010**|**SQL Server 2012 PowerPivot per SharePoint 2010**|**SQL Server 2012 SP1 PowerPivot per SharePoint 2013**|  
|**2008 R2 PowerPivot per Excel 2010**|Tutte le funzionalità|**Esperienza:** Gli utenti possono interagire con la cartella di lavoro nel browser e usarla come origine dati per altre soluzioni.<br /><br /> **Aggiornamento:** Le cartelle di lavoro eseguiranno l'aggiornamento automatico nella raccolta documenti se l'aggiornamento automatico è abilitato per il servizio di sistema PowerPivot nella farm di SharePoint.<br /><br /> **Pianifica aggiornamento dati:** NON supportato. La cartella di lavoro deve essere aggiornata.|**Esperienza:** Gli utenti possono interagire con la cartella di lavoro e usarla come origine dati per altre soluzioni.<br /><br /> **Aggiornamento:** L'aggiornamento automatico non è disponibile. Gli utenti devono aggiornare manualmente le cartelle di lavoro di SQL Server 2008 R2 alla versione 2012 o alla versione di Office 2013.<br /><br /> **Pianifica aggiornamento dati:** NON supportato. La cartella di lavoro deve essere aggiornata.|  
|**2012 PowerPivot per Excel**|Non supportate|Tutte le funzionalità|**Esperienza:** Gli utenti possono interagire con la cartella di lavoro nel browser e usarla come origine dati per altre soluzioni. La pianificazione dell'aggiornamento dati è disponibile.<br /><br /> **Aggiornamento:** L'aggiornamento automatico non è supportato. Gli utenti possono aggiornare manualmente le cartelle di lavoro alla versione di Office 2013.<br /><br /> **Pianificare l'aggiornamento dati:** supportato.|  
|**Excel 2013**|Non supportate|Non supportate|Tutte le funzionalità|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a>Aggiornamento alle cartelle di lavoro di SQL Server 2012 Service Pack 1 (SP1) da cartelle di lavoro di 2008 R2  
 In questa sezione viene descritto l'aggiornamento alle cartelle di lavoro di SQL Server 2012 SP1 PowerPivot per Excel 2013 da cartelle di lavoro di SQL Server 2008 R2 PowerPivot per Excel 2010.  
  
 **Modifica del comportamento:** SQL Server cartelle di lavoro di PowerPivot 2008 R2 non verranno aggiornate automaticamente quando vengono utilizzate in SQL Server 2012 SP1 PowerPivot per SharePoint 2013. Pertanto, gli aggiornamenti dati pianificati non funzioneranno per le cartelle di lavoro di SQL Server 2008 R2 PowerPivot.  
  
 Le cartelle di lavoro di SQL Server 2008 R2 verranno aperte in PowerPivot per SharePoint 2013, tuttavia gli aggiornamenti dati pianificati non funzioneranno. Se si esamina la cronologia degli aggiornamenti, verrà visualizzato un messaggio di errore simile al seguente:  
  
 "La cartella di lavoro contiene un modello PowerPivot non supportato. Il modello PowerPivot nella cartella di lavoro è nel formato di SQL Server 2008 R2 PowerPivot per Excel 2010. Sono supportati i modelli PowerPivot seguenti:  
  
-   SQL Server 2012 PowerPivot per Excel 2010.  
  
-   SQL Server 2012 PowerPivot per Excel 2013.  
  
 **Come aggiornare una cartella di lavoro:** L'aggiornamento dati pianificato non funzionerà finché la cartella di lavoro non verrà aggiornata a una cartella di lavoro di 2012. Per aggiornare la cartella di lavoro e il modello in essa contenuto, completare una delle operazioni seguenti:  
  
-   Scaricare e aprire la cartella di lavoro in Microsoft Excel 2010 con il componente aggiuntivo SQL Server 2012 PowerPivot per Excel installato.  
  
     Aprire la finestra di PowerPivot e aggiornare il modello PowerPivot.  
  
     Successivamente, salvare la cartella di lavoro e ripubblicarla in SharePoint.  
  
-   Scaricare e aprire la cartella di lavoro in Microsoft Excel 2013.  
  
     Aprire la finestra di PowerPivot e aggiornare il modello PowerPivot.  
  
     Successivamente, salvare la cartella di lavoro e ripubblicarla nel server SharePoint.  
  
 Per ulteriori informazioni sulle modifiche apportate alle funzionalità di Analysis Services, vedere [modifiche del comportamento delle funzionalità di Analysis Services in SQL Server 2014](../../behavior-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
 Per altre informazioni sulla cronologia di aggiornamento, vedere [visualizzare la cronologia dell'aggiornamento dati &#40;PowerPivot per SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a>Eseguire l'aggiornamento a cartelle di lavoro di Office 2013 da versioni create tramite il componente aggiuntivo 2012 PowerPivot per Excel  
 In questa sezione viene descritto l'aggiornamento **alle** cartelle di lavoro di SQL Server 2012 SP1 PowerPivot in Excel 2013 **da** cartelle di lavoro di SQL Server 2012 PowerPivot per Excel 2010.  
  
 Tramite l'aggiornamento di una cartella di lavoro viene risolto l'errore seguente che si verifica quando si tenta l'aggiornamento dati pianificato nella cartella di lavoro della versione della cartella di lavoro precedente:  
  
 "Operazione di aggiornamento per le cartelle di lavoro create con la versione precedente di PowerPivot non disponibile".  
  
 **Come aggiornare una cartella di lavoro**  
  
1.  Aggiornare ogni cartella di lavoro manualmente aprendola in Microsoft Excel 2013.  
  
2.  Per aggiornare la cartella di lavoro e il modello in essa contenuto, scaricare e aprire la cartella di lavoro in Microsoft Excel 2013.  
  
3.  Aprire la finestra di PowerPivot e aggiornare il modello PowerPivot.  
  
4.  Successivamente, salvare la cartella di lavoro e ripubblicarla nel server SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a>Eseguire l'aggiornamento a SQL Server cartelle di lavoro di 2012 da versioni create tramite il componente aggiuntivo 2008 R2 PowerPivot per Excel 2010  
 In questa sezione viene descritto l'aggiornamento **a** cartelle di lavoro di SQL Server 2012 PowerPivot per Excel 2010 **da** cartelle di lavoro di SQL Server 2008 R2 PowerPivot per Excel 2010.  
  
 Tramite l'aggiornamento di una cartella di lavoro viene risolto l'errore seguente che si verifica quando si tenta l'aggiornamento dati pianificato nella cartella di lavoro della versione della cartella di lavoro precedente:  
  
 "Operazione di aggiornamento per le cartelle di lavoro create con la versione precedente di PowerPivot non disponibile".  
  
 **Come aggiornare una cartella di lavoro**  
  
 Sono disponibili due modalità per eseguire l'aggiornamento:  
  
1.  Aggiornare manualmente ogni cartella di lavoro aprendola in Excel in un computer in cui è installata la versione [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] di PowerPivot per Excel e ripubblicarla quindi nel server. Quando si apre la cartella di lavoro nella versione più recente del componente aggiuntivo, vengono eseguite le operazioni interne seguenti: il provider di dati nella stringa di connessione dati della cartella di lavoro viene aggiornato a MSOLAP.5, i metadati vengono aggiornati e le relazioni vengono ricreate per essere conformi a un'implementazione più recente.  
  
2.  In alternativa, un amministratore di SharePoint può abilitare la funzionalità di aggiornamento automatico per il servizio di sistema PowerPivot in una farm di SharePoint per eseguire automaticamente l'aggiornamento di una cartella di lavoro di [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] PowerPivot quando viene eseguito l'aggiornamento dati pianificato. Vengono aggiornate solo le cartelle di lavoro configurate per l'aggiornamento dati pianificato.  
  
    > [!NOTE]  
    >  L'aggiornamento automatico è una funzionalità di configurazione del server. Non è possibile abilitarla o disabilitarla per cartelle di lavoro specifiche, librerie o raccolte siti.  
  
 **Come configurare l'aggiornamento automatico durante l'aggiornamento dati**  
  
 Per utilizzare l'aggiornamento automatico, è necessario selezionare la casella di controllo **** relativa all'aggiornamento automatico delle cartelle di lavoro di PowerPivot per abilitare l'aggiornamento dati dal server nello strumento di configurazione di PowerPivot. Se si configura una nuova installazione, all'interno dello strumento la casella di controllo si trova nelle pagine **Aggiornare il servizio di sistema PowerPivot** e **Creare applicazione del servizio PowerPivot** .  
  
 Per verificare se l'aggiornamento automatico è abilitato, è possibile eseguire il cmdlet riportato di seguito.  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 L'output di Get-PowerPivotSystemService è un elenco di proprietà e valori corrispondenti. Nell'elenco di proprietà dovrebbe essere visualizzata `WorkbookUpgradeOnDataRefresh`. Se l'aggiornamento automatico è abilitato, sarà impostata su **true** . Se è **false**, procedere al passaggio successivo per abilitare l'aggiornamento automatico delle cartelle di lavoro.  
  
 Per abilitare l'aggiornamento automatico delle cartelle di lavoro, eseguire il comando seguente:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 Dopo avere aggiornato la cartella di lavoro, è possibile utilizzare l'aggiornamento programmato dei dati e le nuove funzionalità del componente aggiuntivo PowerPivot per Excel.  
  
##  <a name="bkmk_runold"></a>Esecuzione di più versioni di cartelle di lavoro in un server più recente  
 È possibile effettuare un'esecuzione side-by-side di versioni meno recenti e più recenti di cartelle di lavoro di PowerPivot in un'istanza di [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 In base alla modalità di installazione del server, **potrebbe essere necessario** installare una versione precedente del provider OLE DB per Analysis Services prima che sia possibile accedere alle cartelle di lavoro meno recenti e più recenti nello stesso server.  
  
 Si noti che la pubblicazione delle cartelle di lavoro di una versione più recente in istanze di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] di SQL Server precedenti non è supportata. Tramite un'istanza di [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] non verrà caricata una cartella di lavoro creata nella versione [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] di [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]e tramite un'istanza di SQL Server 2012 non verranno caricate cartelle di lavoro di Office 2013 con modelli di dati avanzati creati utilizzando la versione [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] di PowerPivot in Excel.  
  
###  <a name="bkmk_msolapxslx"></a>Come verificare la presenza di MSOLAP provider di dati informazioni in una cartella di lavoro di PowerPivot  
 Utilizzare le istruzioni seguenti per controllare quale provider OLE DB viene utilizzato in una cartella di lavoro di PowerPivot. Il controllo delle informazioni sulla connessione dati non richiede l'installazione del componente aggiuntivo [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  Nella scheda Dati di Excel fare clic su **Connessioni**. Fare clic su **Proprietà**.  
  
2.  La versione del provider viene visualizzata nella scheda **Definizione** all'inizio della stringa di connessione.  
  
     **Provider = MSOLAP. 5** indica che la cartella [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]di lavoro è.  
  
     **Provider = MSOLAP. 4** indica [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Data Source = $Embedded $** indica che la cartella di lavoro è una cartella di lavoro di PowerPivot, usando un database incorporato.  
  
###  <a name="bkmk_msolappc"></a>Come verificare la versione corrente del provider di dati MSOLAP in un computer locale  
 Utilizzare le istruzioni seguenti per controllare quale provider OLE DB è la versione corrente sul server o sulla workstation in cui vengono eseguite le cartelle di lavoro di PowerPivot. Conoscere la versione corrente può consentire la risoluzione dei problemi relativi a errori di connessione dati dopo l'aggiornamento.  
  
1.  Nell'Editor del Registro di sistema andare a HKEY_CLASSES_ROOT.  
  
2.  Scorrere verso il basso fino a MSOLAP. Verificare che MSOLAP.5 sia elencato fra i provider OLAP installati nel sistema. Verificare che MSOLAP | CurVer sia impostato su MSOLAP.5.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire la migrazione di PowerPivot a SharePoint 2013](migrate-power-pivot-to-sharepoint-2013.md)   
 [PowerPivot per SharePoint di aggiornamento](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Novità di Analysis Services e Business Intelligence](../../what-s-new-in-analysis-services.md)   
 [Visualizzare la cronologia dell'aggiornamento dati &#40;PowerPivot per SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
