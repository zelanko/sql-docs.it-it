---
title: Funzionalità di Master Data Services sospese in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479440"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>Funzionalità di Master Data Services non più supportate in SQL Server 2014
  In questo argomento vengono descritte le funzionalità di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] non più disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Funzionalità non più utilizzate  
 Non sono presenti funzionalità non più disponibili in questa versione.  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Funzionalità non più utilizzate  
  
### <a name="security"></a>Security  
 Per semplificare l'assegnazione della sicurezza, non è più possibile assegnare autorizzazioni per oggetti modello agli oggetti Gerarchia derivata, Gerarchia esplicita e Gruppo di attributi.  
  
-   Le autorizzazioni della gerarchia derivata sono ora basate sul modello. Se ad esempio si desidera che un utente disponga delle autorizzazioni per una gerarchia derivata, è necessario assegnare l' **aggiornamento** all'oggetto modello. È quindi possibile assegnare l'autorizzazione **Nega** accesso a tutte le entità a cui non si vuole che l'utente abbia accesso.  
  
-   Le autorizzazioni della gerarchia esplicita sono ora basate sull'entità. Se, ad esempio, l'utente dispone delle autorizzazioni di **aggiornamento** per un'entità account, tutte le gerarchie esplicite per l'entità saranno aggiornabili.  
  
-   Le autorizzazioni per gruppi di attributi non possono più essere assegnate nell'area funzionale **autorizzazioni utenti e gruppi** . Al contrario, nell'area funzionale **Amministrazione sistema** in cui vengono creati i gruppi di attributi, è possibile concedere agli utenti e ai gruppi l'autorizzazione **aggiornamento** per i gruppi di attributi. L'autorizzazione di sola **lettura** per i gruppi di attributi non è più disponibile.  
  
### <a name="staging-process"></a>Processo di gestione temporanea  
 Non è possibile utilizzare il nuovo processo di gestione temporanea per:  
  
-   Creare o eliminare raccolte.  
  
-   Aggiungere o rimuovere membri dalle raccolte.  
  
-   Riattivare membri e raccolte.  
  
 È possibile utilizzare il processo di gestione temporanea di [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] per utilizzare le raccolte.  
  
### <a name="model-deployment-wizard"></a>Distribuzione guidata modello  
 I pacchetti contenenti dati non possono più essere creati e distribuiti tramite la procedura guidata nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Può essere utilizzata una nuova utilità della riga di comando. Per altre informazioni, vedere [Distribuzione di modelli &#40;Master Data Services&#41;](deploying-models-master-data-services.md).  
  
 La procedura guidata ancora può essere utilizzata per creare e distribuire pacchetti che non contengono dati.  
  
 I pacchetti possono inoltre essere distribuiti solo nella versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizzata per crearli. Pertanto non è possibile distribuire pacchetti creati in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. È necessario distribuire il pacchetto all'ambiente [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] e aggiornare quindi il database a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="code-generation-business-rules"></a>Regole business per generazione codice  
 Le regole business che generano automaticamente valori per l'attributo Code sono ora amministrate differentemente. In precedenza, per generare valori per l'attributo Code, è stato utilizzato l' **attributo default per un'azione di valore generato** nell'area funzionale **Amministrazione sistema** in **regole business**. A questo punto, in **Amministrazione sistema**è necessario modificare l'entità per abilitare i valori del codice generati automaticamente. Per altre informazioni, vedere [Creazione di codice automatica &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).  
  
 Se si dispone di un pacchetto di distribuzione per modelli [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] che contiene una regola di questo tipo, quando si aggiorna il database a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], la regola business è esclusa.  
  
### <a name="bulk-updates-and-exporting"></a>Aggiornamento ed esportazione bulk  
 Nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] non è più possibile aggiornare i valori di attributo per più membri in bulk. Per eseguire gli aggiornamenti in blocco, utilizzare il processo di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]gestione temporanea o.  
  
 Nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] non è più possibile esportare membri in Excel. Per lavorare con i membri in Excel, usare [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
### <a name="transactions"></a>Transazioni  
 Nell'area funzionale **Esplora** , gli utenti non possono più ripristinare le proprie transazioni. In precedenza, gli utenti potevano ripristinare le modifiche apportate ai dati in **Esplora**. Gli amministratori possono comunque ripristinare le transazioni per tutti gli utenti nell'area funzionale **Gestione versioni** .  
  
 Le annotazioni sono ora permanenti e non possono essere eliminate. Precedentemente, le annotazioni erano considerate transazioni e potevano essere eliminate ripristinando la transazione.  
  
### <a name="web-service"></a>Servizio Web  
 Il servizio Web [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ora è abilitato automaticamente, come richiesto da Silverlight. In precedenza, il servizio Web doveva essere abilitato manualmente.  
  
### <a name="powershell-cmdlets"></a>Cmdlet di PowerShell  
 In MDS non sono più inclusi i cmdlet di PowerShell.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità deprecate di Master Data Services in SQL Server 2014](deprecated-master-data-services-features.md)  
  
  
