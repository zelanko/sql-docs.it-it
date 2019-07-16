---
title: Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato (SharePoint 2013) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5f0d49d6aeb8231dbffb56b42fe1151ae90d0e41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68181302"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Aggiornare le cartelle di lavoro e l'aggiornamento dati pianificato (SharePoint 2013)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Questo argomento illustra l'esperienza utente relativa alle cartelle di lavoro create in ambienti di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] precedenti e la modalità di aggiornamento delle cartelle di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in modo che sia possibile avvalersi delle nuove funzionalità introdotte in questa versione. Per altre informazioni sulle nuove funzionalità, vedere [What ' s New in Power Pivot](http://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  Non è possibile eseguire il rollback dell'aggiornamento per cartelle di lavoro aggiornate automaticamente nel server. Una volta aggiornata, una cartella di lavoro rimane in questo stato. Per utilizzare una versione precedente, è possibile ripubblicare la cartella di lavoro precedente in SharePoint, ripristinare una versione precedente oppure riciclare la cartella di lavoro. Per ulteriori informazioni sul ripristino o riciclo di un documento in SharePoint, vedere [Pianificare di proteggere il contenuto tramite i Cestini e il controllo delle versioni](http://go.microsoft.com/fwlink/?LinkId=238669).  
  
  
##  <a name="bkmk_overview"></a> Panoramica dell'aggiornamento delle cartelle di lavoro  
 Una cartella di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] è una cartella di lavoro di Excel che contiene dati di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] incorporati. L'aggiornamento di una cartella di lavoro offre due vantaggi:  
  
-   Utilizzo di nuove funzionalità in [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Abilitazione dell'aggiornamento dati pianificato per cartelle di lavoro che vengono eseguite con un server [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services in modalità SharePoint.  
  
> [!IMPORTANT]  
>  Non è possibile eseguire il rollback di una cartella di lavoro aggiornata, pertanto assicurarsi di effettuare una copia del file se si desidera utilizzarlo nella versione precedente di [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]o in una versione precedente di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 La tabella seguente elenca il supporto e il comportamento delle cartelle di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in base all'ambiente in cui è stata creata la cartella di lavoro. Nel comportamento descritto sono inclusi l'esperienza utente generale, le opzioni di aggiornamento supportate per aggiornare la cartella di lavoro all'ambiente specifico e il comportamento dell'aggiornamento dati pianificato di una cartella di lavoro che non è stata ancora aggiornata.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Opzioni di aggiornamento e comportamento della cartella di lavoro  
  
|Data creazione|\<|Supporto e comportamento|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2010**|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2010**|**2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013**|  
|**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel 2010**|Tutte le funzionalità|**Esperienza:** Gli utenti possono interagire con la cartella di lavoro nel browser e utilizzarla come origine dati per altre soluzioni.<br /><br /> **Eseguire l'aggiornamento:** Le cartelle di lavoro verranno aggiornate automaticamente nella raccolta documenti se l'aggiornamento automatico è abilitato per il [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] servizio di sistema nella farm di SharePoint,<br /><br /> **Pianificazione dell'aggiornamento dati:** NON è supportato. La cartella di lavoro deve essere aggiornata.|**Esperienza:** Gli utenti possono interagire con la cartella di lavoro e utilizzarla come origine dati per altre soluzioni.<br /><br /> **Eseguire l'aggiornamento:** Aggiornamento automatico non è disponibile. Gli utenti devono aggiornare manualmente le cartelle di lavoro di SQL Server 2008 R2 alla versione 2012 o alla versione di Office 2013.<br /><br /> **Pianificazione dell'aggiornamento dati:** NON è supportato. La cartella di lavoro deve essere aggiornata.|  
|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel**|Non supportate|Tutte le funzionalità|**Esperienza:** Gli utenti possono interagire con la cartella di lavoro nel browser e utilizzarla come origine dati per altre soluzioni. La pianificazione dell'aggiornamento dati è disponibile.<br /><br /> **Eseguire l'aggiornamento:** Aggiornamento automatico non è supportato. Gli utenti possono aggiornare manualmente le cartelle di lavoro alla versione di Office 2013.<br /><br /> **Pianificazione dell'aggiornamento dati:** supportata.|  
|**Excel 2013**|Non supportate|Non supportate|Tutte le funzionalità|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> Eseguire l'aggiornamento a cartelle di lavoro di SQL Server 2012 Service Pack 1 (SP1) da cartelle di lavoro di SQL Server 2008 R2  
 Questa sezione descrive l'aggiornamento a SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per cartelle di lavoro di Excel 2013 e da SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per cartelle di lavoro di Excel 2010.  
  
 **Modifica del comportamento:** SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] cartelle di lavoro non verranno automaticamente aggiornati quando vengono usati in SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013. Gli aggiornamenti dati pianificati non funzioneranno quindi per le cartelle di lavoro di SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
 Le cartelle di lavoro di SQL Server 2008 R2 verranno aperte in [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per SharePoint 2013, tuttavia gli aggiornamenti dati pianificati non funzioneranno. Se si esamina la cronologia degli aggiornamenti, verrà visualizzato un messaggio di errore simile al seguente:  
  
 "La cartella di lavoro contiene supportato [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modello. Il modello [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] nella cartella di lavoro è nel formato di SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel 2010. I modelli [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] supportati sono i seguenti:  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel 2010.  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel 2013.  
  
 **Come aggiornare una cartella di lavoro:** L'aggiornamento dati pianificato non funzionerà finché non viene aggiornata la cartella di lavoro alla relativa versione 2012. Per aggiornare la cartella di lavoro e il modello in essa contenuto, completare una delle operazioni seguenti:  
  
-   Scaricare e aprire la cartella di lavoro in Microsoft Excel 2010 con il componente aggiuntivo SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel installato.  
  
     Aprire la finestra di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e aggiornare il modello di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     Successivamente, salvare la cartella di lavoro e ripubblicarla in SharePoint.  
  
-   Scaricare e aprire la cartella di lavoro in Microsoft Excel 2013.  
  
     Aprire la finestra di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e aggiornare il modello di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     Successivamente, salvare la cartella di lavoro e ripubblicarla nel server SharePoint.  
  
 Per altre informazioni sulle modifiche alle funzionalità di Analysis Services, vedere [Modifiche del comportamento delle funzionalità di Analysis Services in SQL Server 2016](../../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)  
  
 Per altre informazioni sulla cronologia di aggiornamento, vedere [Visualizzare la cronologia dell'aggiornamento dati &#40;Power Pivot per SharePoint&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> Eseguire l'aggiornamento a cartelle di lavoro di Office 2013 da versioni create tramite il componente aggiuntivo SQL Server 2012 Power Pivot per Excel  
 Questa sezione descrive l'aggiornamento **a** SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in Excel 2013 **da** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per cartelle di lavoro di Excel 2010.  
  
 Tramite l'aggiornamento di una cartella di lavoro viene risolto l'errore seguente che si verifica quando si tenta l'aggiornamento dati pianificato nella cartella di lavoro della versione della cartella di lavoro precedente:  
  
 "Operazione di aggiornamento per cartelle di lavoro create con la versione precedente di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] non è disponibile."  
  
 **Modalità di aggiornamento di una cartella di lavoro**  
  
1.  Aggiornare ogni cartella di lavoro manualmente aprendola in Microsoft Excel 2013.  
  
2.  Per aggiornare la cartella di lavoro e il modello in essa contenuto, scaricare e aprire la cartella di lavoro in Microsoft Excel 2013.  
  
3.  Aprire la finestra di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] e aggiornare il modello di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
4.  Successivamente, salvare la cartella di lavoro e ripubblicarla nel server SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> Eseguire l'aggiornamento a cartelle di lavoro di SQL Server 2012 da versioni create tramite il componente aggiuntivo SQL Server 2008 R2 Power Pivot per Excel 2010  
 Questa sezione descrive l'aggiornamento **a** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel 2010 **da** SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per cartelle di lavoro di Excel 2010.  
  
 Tramite l'aggiornamento di una cartella di lavoro viene risolto l'errore seguente che si verifica quando si tenta l'aggiornamento dati pianificato nella cartella di lavoro della versione della cartella di lavoro precedente:  
  
 "Operazione di aggiornamento per cartelle di lavoro create con la versione precedente di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] non è disponibile."  
  
 **Modalità di aggiornamento di una cartella di lavoro**  
  
 Sono disponibili due modalità per eseguire l'aggiornamento:  
  
1.  Aggiornare manualmente ogni cartella di lavoro aprendola in Excel in un computer in cui è installata la versione [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel e ripubblicarla quindi nel server. Quando si apre la cartella di lavoro nella versione più recente del componente aggiuntivo, vengono eseguite le operazioni interne seguenti: il provider di dati nella stringa di connessione dati della cartella di lavoro viene aggiornato a MSOLAP.5, i metadati vengono aggiornati e le relazioni vengono ricreate per essere conformi a un'implementazione più recente.  
  
2.  In alternativa, un amministratore di SharePoint può abilitare la funzionalità di aggiornamento automatico per il servizio di sistema [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in una farm di SharePoint per eseguire automaticamente l'aggiornamento di una cartella di lavoro di [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] quando viene eseguito l'aggiornamento dati pianificato. Vengono aggiornate solo le cartelle di lavoro configurate per l'aggiornamento dati pianificato.  
  
    > [!NOTE]  
    >  L'aggiornamento automatico è una funzionalità di configurazione del server. Non è possibile abilitarla o disabilitarla per cartelle di lavoro specifiche, librerie o raccolte siti.  
  
 **Modalità di configurazione dell'aggiornamento automatico durante l'aggiornamento dati**  
  
 Per usare l'aggiornamento automatico, è necessario selezionare la casella di controllo **Automatically upgrade [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] workbooks to enable data refresh from the server** (Aggiorna automaticamente le cartelle di lavoro di Power Pivot per abilitare l'aggiornamento dei dati dal server) nello strumento di configurazione di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]. Se si configura una nuova installazione, all'interno dello strumento la casella di controllo si trova nelle pagine **Upgrade [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] System Service** (Aggiorna il servizio di sistema Power Pivot) e nella pagina **Create [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] Service Application** (Crea l'applicazione del servizio Power Pivot).  
  
 Per verificare se l'aggiornamento automatico è abilitato, è possibile eseguire il cmdlet riportato di seguito.  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 L'output di Get-PowerPivotSystemService è un elenco di proprietà e valori corrispondenti. **WorkbookUpgradeOnDataRefresh** dovrebbe essere visualizzato nell'elenco di proprietà. Se l'aggiornamento automatico è abilitato, sarà impostata su **true** . Se è **false**, procedere al passaggio successivo per abilitare l'aggiornamento automatico delle cartelle di lavoro.  
  
 Per abilitare l'aggiornamento automatico delle cartelle di lavoro, eseguire il comando seguente:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 Dopo avere aggiornato la cartella di lavoro, è possibile usare l'aggiornamento dati pianificato e le nuove funzionalità del componente aggiuntivo [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] per Excel.  
  
##  <a name="bkmk_runold"></a> Esecuzione di più versioni di cartelle di lavoro in un server più recente  
 È possibile eseguire affiancate versioni meno recenti e più recenti di cartelle di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in un'istanza di [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 In base alla modalità di installazione del server, **potrebbe essere necessario** installare una versione precedente del provider OLE DB per Analysis Services prima che sia possibile accedere alle cartelle di lavoro meno recenti e più recenti nello stesso server.  
  
 Si noti che la pubblicazione delle cartelle di lavoro di una versione più recente in istanze di [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] di SQL Server precedenti non è supportata. Un'istanza di [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] non caricherà una cartella di lavoro creata nella versione [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] di [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]e un'istanza di SQL Server 2012 non caricherà cartelle di lavoro di Office 2013 con modelli di dati avanzati creati usando la versione [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in Excel.  
  
###  <a name="bkmk_msolapxslx"></a> Come verificare le informazioni del provider di dati MSOLAP in una cartella di lavoro di Power Pivot  
 Usare le istruzioni seguenti per controllare quale provider OLE DB viene usato in una cartella di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Il controllo delle informazioni sulla connessione dati non richiede l'installazione del componente aggiuntivo [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  Nella scheda Dati di Excel fare clic su **Connessioni**. Scegliere **Proprietà**.  
  
2.  La versione del provider viene visualizzata nella scheda **Definizione** all'inizio della stringa di connessione.  
  
     **Provider=MSOLAP.5** indica che la cartella di lavoro è [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
     **Provider=MSOLAP.4** indica [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Data Source=$Embedded$** indica che la cartella di lavoro è una cartella di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] in cui viene usato un database incorporato.  
  
###  <a name="bkmk_msolappc"></a> Procedura di verifica della versione corrente del provider di dati MSOLAP su un computer locale  
 Usare le istruzioni seguenti per controllare quale provider OLE DB è la versione corrente nel server o nella workstation in cui vengono eseguite le cartelle di lavoro di [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Conoscere la versione corrente può consentire la risoluzione dei problemi relativi a errori di connessione dati dopo l'aggiornamento.  
  
1.  Nell'Editor del Registro di sistema andare a HKEY_CLASSES_ROOT.  
  
2.  Scorrere verso il basso fino a MSOLAP. Verificare che MSOLAP.5 sia elencato fra i provider OLAP installati nel sistema. Verificare che MSOLAP | CurVer sia impostato su MSOLAP.5.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire la migrazione di PowerPivot a SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Aggiornare Power Pivot per SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Novità di Analysis Services](../../../analysis-services/what-s-new-in-analysis-services.md)   
 [Visualizzare la cronologia dell'aggiornamento dati &#40;Power Pivot per SharePoint&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
