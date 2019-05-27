---
title: Modifiche di rilievo per Analysis Services Features in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b70cf2bb85bca60a372f09a5d3fc9ffedb90cc
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66064422"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>Modifiche di rilievo nelle funzionalità di Analysis Services in SQL Server 2014
  In questo argomento vengono descritte le modifiche di rilievo introdotte in [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]. Queste modifiche potrebbero comportare il malfunzionamento di applicazioni, script o funzionalità basate su versioni precedenti di SQL Server.  
  
 Contenuto dell'argomento:  
  
-   [Modifiche di rilievo in SQL Server 2014](#bkmk_sql2014)  
  
-   [Modifiche di rilievo in SQL Server 2012 SP1](#bkmk_2012Sp1)  
  
-   [Modifiche di rilievo in SQL Server 2012](#bkmk_sql11)  
  
-   [Modifiche di rilievo in SQL Server 2008 o SQL Server 2008 R2](#bkmk_sql10)  
  
##  <a name="bkmk_sql2014"></a> Modifiche di rilievo in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 In questa versione non sono annunciate nuove modifiche di rilievo per le funzionalità tabulari, multidimensionali, di data mining o di [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] .  Tuttavia, considerata l'analogia di  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] con le versioni [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , le modifiche di rilievo rispetto a entrambe le versioni precedenti sono elencate qui per praticità, nel caso si effettui l'aggiornamento da [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_2012Sp1"></a> Modifiche di rilievo in SQL Server 2012 SP1  
 È noto che le modifiche al codice correlato alla globalizzazione causano errori in alcune applicazioni, tra cui:  
  
 **Distinzione maiuscole/minuscole degli identificatori di oggetto**  
 Una modifica al codice con lo scopo di non applicare alcuna distinzione tra maiuscole e minuscole in tutti gli identificatori di oggetto ha l'effetto opposto per alcune lingue. L'obiettivo è quello di non applicare alcuna distinzione tra maiuscole e minuscole in tutti gli identificatori di oggetto, indipendentemente dalle regole di confronto. Questa modifica consente di allineare Analysis Services alle altre applicazioni usate in genere nello stesso gruppo di soluzioni.  
  
 Per le lingue che si basano sui 26 caratteri dell'alfabeto latino di base, ora non viene più applicata alcuna distinzione tra maiuscole e minuscole negli identificatori di oggetto, che è appunto il comportamento previsto.  
  
 Per il cirillico e gli altri alfabeti composti da due set di caratteri maiuscoli/minuscoli distinti (greco, armeno e copto), negli identificatori di oggetto viene ora applicata la distinzione tra maiuscole e minuscole. Le modifiche di rilievo si verificano con maggiore probabilità nel caso in cui vi sia una differenza tra maiuscole e minuscole tra un identificatore di oggetto e il modo in cui viene fatto riferimento all'identificatore stesso, ad esempio uno script di elaborazione che fa riferimento all'identificatore di oggetto in tutte lettere minuscole. Questo comportamento verrà modificato in futuro, ma come soluzione alternativa temporanea è consigliabile modificare gli script in modo da usare le stesse lettere (maiuscole o minuscole) dell'identificatore di oggetto.  
  
##  <a name="bkmk_sql11"></a> Modifiche di rilievo in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 In questa sezione sono illustrate le modifiche di rilievo riportate per le funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Problema|Descrizione|  
|-----------|-----------------|  
|Comandi di installazione rimossi per un'installazione [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] .|L'installazione installa, ma non configura più un [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]. I comandi di installazione che raccolgono valori utilizzati per le azioni di configurazione sono ora rimossi. Tra questi sono inclusi /FARMACCOUNT, /FARMPASSWORD, /PASSPHRASE e /FARMADMINPORT.<br /><br /> Se sono stati creati script di installazione per l'installazione automatica, sarà necessario modificare quegli script per un'installazione [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . In alternativa, utilizzare cmdlet di PowerShell per configurare il server in modalità automatica. Per altre informazioni, vedere [installare PowerPivot dal Prompt dei comandi](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md) e [configurazione di PowerPivot tramite Windows PowerShell](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).|  
  
##  <a name="bkmk_sql10"></a> Modifiche di rilievo in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 In questa sezione sono incluse le modifiche di rilievo rispetto alle versioni precedenti. Se si aggiorna da [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], è necessario rivedere le modifiche di rilievo introdotte in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
|Problema|Descrizione|  
|-----------|-----------------|  
|Tramite la funzione shallow exists vengono utilizzati in modo diverso i set denominati contenenti i membri enumerati o i crossjoin di enumset.|In [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]la funzione shallow exists non funzionava con i set denominati contenenti i membri enumerati o i crossjoin di enumset. Per la compatibilità con la versione originale e SP1 di [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], impostare la proprietà di configurazione "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" su 1 oppure per la compatibilità con [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2, impostarla su 2.|  
|Tramite le funzioni VBA vengono gestiti i valori Null e i valori vuoti in modo diverso rispetto a [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]|In [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]tramite le funzioni VBA viene restituito 0 o una stringa vuota quando si utilizzano valori Null o vuoti come argomenti. In [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]restituiscono valori Null.|  
|La Migrazione guidata non riuscirà perché DSO non è installato per impostazione predefinita.|Per impostazione predefinita, SQL Server 2008 non installa il componente per la compatibilità con le versioni precedenti DSO (Decision Support Objects). Il pacchetto per la compatibilità con le versioni precedenti viene installato per impostazione predefinita ma il componente DSO del pacchetto viene disabilitato. Poiché la Migrazione guidata SQL Server Analysis Services si basa su tale componente, l'operazione di migrazione avrà esito negativo se il componente non verrà installato. Per installare il componente DSO, eseguire le operazioni seguenti:<br /><br /> 1) aprire il pannello di controllo.<br />2) in Windows XP o Windows Server 2003, selezionare **Aggiungi / Rimuovi programmi**. In Windows Vista e Windows Server 2008 selezionare **Programmi e funzionalità**.<br />3) pulsante destro del mouse **compatibilità con le versioni precedenti di Microsoft SQL Server 2005**e selezionare **modifica**.<br />4) nella procedura guidata il programma di installazione di compatibilità con le versioni precedenti, fare clic su **successivo**.<br />5) nella pagina Manutenzione programma selezionare **Modify**, quindi fare clic su **successivo**.<br />6) nella pagina Selezione caratteristiche se gli oggetti DSO (Decision Support) non è disponibile, fare clic sulla freccia verso il basso e selezionare **questa funzionalità verrà installata sul disco rigido locale**. Scegliere **Avanti**.<br />7) nella pronto per la pagina Modifica del programma, fare clic su **installare**.<br />8) dopo aver terminato l'installazione, fare clic su **fine**.<br /><br /> <br /><br /> È possibile rimuovere il componente DSO al termine della migrazione seguendo i passaggi precedenti e modificando l'opzione per DSO in "**questa funzionalità non saranno disponibile**."<br /><br /> Se il pacchetto per la compatibilità con le versioni precedenti non viene installato, è possibile installarlo dai supporti di distribuzione di SQL Server 2008. Tenere presente che esistono versioni differenti per ogni architettura di destinazione (x86, x64, ia64). Tali versioni sono disponibili nei percorsi seguenti:<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|Si sconsiglia di inserire il percorso della partizione nella cartella Dati.|Il server gestisce la cartella Dati e crea o rimuove cartelle in seguito alla creazione, eliminazione e modifica degli oggetti. La specifica di un percorso di archiviazione per le partizioni nella cartella Dati è pertanto assolutamente sconsigliata, soprattutto nelle sottocartelle relative a database, cubi e dimensioni. Sebbene il server consenta l'esecuzione di questa operazione mediante la creazione o la modifica, verrà visualizzato un avviso. Quando si aggiornano database dalla versione SQL Server 2005 Analysis Services alla versione [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] che include percorsi di archiviazione delle partizioni nella cartella Dati, il server funzionerà. Per le operazioni di ripristino o sincronizzazione sarà necessario spostare i percorsi di archiviazione delle partizioni all'esterno della cartella Dati.|  
|Si potrebbero ottenere risultati imprevisti per le query che utilizzano la parola chiave MDX "EXISTING" in ProClarity Analytics Server e Microsoft Office PerformancePoint Server 2007.|ProClarity Analytics Server e Microsoft Office PerformancePoint Server 2007 utilizzano erroneamente la parola chiave EXISTING in MDX in determinati scenari. A causa delle modifiche apportate in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services, tramite queste query potrebbero essere restituiti risultati imprevisti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Analysis Services Backward Compatibility](analysis-services-backward-compatibility.md)  
  
  
