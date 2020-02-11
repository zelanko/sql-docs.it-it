---
title: Accendere o spegnere l'appliance
description: Accendere o spegnere l'appliance per il sistema di piattaforma di analisi
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee70338b5a46ec60d808e489d982fd80692c5d1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400626"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Accendere o spegnere l'appliance per il sistema di piattaforma di analisi
Questo argomento descrive come accendere o spegnere la piattaforma di analisi Systemappliance che esegue Parallel data warehouse. Usare questo argomento quando si sposta un'appliance del sistema della piattaforma di analisi o si accende un'appliance in seguito a un errore irreversibile dell'alimentazione.  
  
L'accensione e la disattivazione dell'appliance non corrispondono all'avvio e all'arresto dei servizi Appliance. Per informazioni su questo argomento, vedere [PDW Services Status &#40;Analytics Platform System&#41;](pdw-services-status.md). Per informazioni sull'accensione o la disattivazione di un data warehouse parallelo SQL Server 2008, vedere il file della Guida SQL Server 2008 Parallel data warehouse. Per informazioni sull'accensione o la disattivazione di un data warehouse parallelo SQL Server 2012 AU1 o AU2, vedere il file della Guida relativo a tali versioni.  
  
Quando queste istruzioni specificano la connessione a un nodo di SQL Server PDW, la connessione può essere locale utilizzando dispositivi collegati (KVM) o remote utilizzando Desktop remoto. Alcune azioni devono essere fisiche (accensione di un interruttore di alimentazione) e alcune, ad esempio l'arresto, possono essere fisiche o usando i comandi di Windows.  
  
Le connessioni ai nodi SQL Server PDW possono essere effettuate usando gli indirizzi IP assegnati ai nodi o dal computer **HST01** usando le applicazioni di **Gestione cluster di failover** (**cluadmin. msc**) o della console di **gestione di Hyper-V** (**virtmgmt. msc**) e facendo clic con il pulsante destro del mouse sul nome del nodo.  
  
## <a name="PowerOff"></a>Spegnere l'appliance  
  
### <a name="before-you-begin"></a>Prima di iniziare  
Prima di spegnere l'appliance, è necessario terminare tutte le attività nell'appliance. Per terminare tutte le attività:  
  
-   Utilizzare la pagina **sessioni** della console di amministrazione per identificare gli utenti correnti. Contattarli e chiedergli di disconnettersi.  
  
-   Se necessario, è possibile utilizzare l'istruzione **Kill** per forzare la chiusura di una connessione client. Prestare attenzione quando si uccidono le connessioni. Quando vengono interrotti, alcuni processi transazionali, ad esempio un aggiornamento con esecuzione prolungata, devono eseguire il rollback dell'attività prima che SQL Server possa completare il ripristino del database. Il rollback di un aggiornamento o di un'eliminazione parzialmente completato può richiedere molto tempo.  
  
### <a name="to-power-off-the-appliance"></a>Per spegnere l'appliance  
  
> [!WARNING]  
> Tutti i passaggi devono essere eseguiti nell'ordine esatto elencato e ogni passaggio deve essere completato prima di eseguire il passaggio successivo, salvo diversa indicazione. L'esecuzione di passaggi non ordinati o senza attendere il completamento di ogni passaggio può causare errori quando l'Appliance viene accesa in un secondo momento.  
  
1.  Connettersi al nodo di controllo PDW (**_PDW_region_-CTL01** ) e accedere con l'account di amministratore di dominio dell'appliance della piattaforma di analisi.  
  
2.  Eseguire `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` per aprire il **Configuration Manager**.  
  
3.  Nel Configuration Manager, nel menu **topologia data warehouse parallela** , fare clic sulla scheda **stato Servizi** , quindi fare clic su **Arresta area** per arrestare i servizi PDW.   
  
4.  Connettersi a ** _appliance_domain_-HST01** e accedere con l'account di amministratore di dominio dell'appliance.  
  
5.  Utilizzando la **Gestione cluster di failover** connettersi al cluster ** _appliance_domain_-WFOHST01** , se non è connessa automaticamente, quindi nel riquadro di spostamento fare clic su **ruoli**. Nel riquadro **ruoli** :  
  
    1.  Consente di selezionare tutte le macchine virtuali. Fare clic con il pulsante destro del mouse su di essi e scegliere **Arresta**.  
  
    2.  Attendere il completamento dell'arresto di tutte le macchine virtuali selezionate.  
  
6.  Chiudere l'applicazione **Gestione cluster di failover** .  
  
7. Arrestare tutti i server eccetto ** _appliance_domain_-HST01**.  
  
8. Arrestare il server ** _appliance_domain_-HST01** .  
  
9. Arrestare le unità di distribuzione dell'alimentazione (PDU).  
  
## <a name="PowerOn"></a>Accendere l'appliance  
  
### <a name="to-power-on-the-appliance"></a>Per accendere l'appliance  
  
> [!WARNING]  
> Tutti i passaggi devono essere eseguiti nell'ordine esatto elencato e ogni passaggio deve essere completato prima di eseguire il passaggio successivo, salvo diversa indicazione. L'esecuzione di passaggi non ordinati o senza attendere il completamento di ogni passaggio può causare errori di avvio.  
  
1.  Accendere le unità di distribuzione dell'energia elettrica (PDU) e attendere l'avvio automatico dei commutatori.  
  
2.  Accendere il server ** _appliance_domain_-HST01** .  
  
3.  Accedere a ** _appliance_domain_-HST01** come amministratore di dominio del dispositivo.  
  
4.  Avviare il programma di **gestione di Hyper-V** (**virtmgmt. msc**) e connettersi a ** _appliance_domain_-HST01** se non è connesso per impostazione predefinita.  
  
    1.  Se non è possibile connettersi per nome perché il ** _PDW_region_-ad01** non è in esecuzione, provare a connettersi usando l'indirizzo IP.  
  
    2.  Nel riquadro **macchine virtuali** individuare ** _PDW_region_-ad01** e verificare che sia in esecuzione. In caso contrario, avviare questa macchina virtuale e attendere che venga avviata completamente.  
  
5.  Accendere il resto dei server nell'appliance.  
  
6.  Quando si è connessi a **HST01** come amministratore di dominio del dispositivo, dalla console di **gestione di Hyper-V**:  
  
    1.  Connettersi a ** _appliance_domain_-HST02**.  
  
    2.  Nel riquadro **macchine virtuali** individuare ** _PDW_region_-ad02** e verificare che sia in esecuzione.  In caso contrario, avviare questa macchina virtuale e attendere che venga avviata completamente.  
  
7.  Utilizzando la **Gestione cluster di failover** connettersi al cluster ** _appliance_domain_-WFOHST01** , se non è connessa automaticamente, quindi nel riquadro di **spostamento** fare clic su **ruoli**. Nel riquadro **ruoli** :  
  
    1.  Selezionare tutte le macchine virtuali, fare clic con il pulsante destro del mouse su di esse, quindi scegliere **Avvia**.  
  
    2.  Attendere il completamento di tutte le macchine virtuali selezionate, prima di procedere al passaggio successivo.  
  
    3.  Se necessario per le macchine virtuali di cui è stato eseguito il failover, chiuderle, spostarle e riavviarle nell'host primario appropriato.  
  
8. Se lo si desidera, disconnettersi da **HST01** .  
  
9. Connettersi a ** _PDW_region_-CTL01** usando l'account di amministratore di dominio del dispositivo.  
  
10. Eseguire `C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe` per avviare il **Configuration Manager**.  
  
11. Nel **Configuration Manager**, nel menu **topologia data warehouse parallela** , fare clic sulla scheda **stato Servizi** , quindi fare clic su **Avvia area** per avviare i servizi PDW.  
  
### <a name="to-verify-the-appliance-health"></a>Per verificare l'integrità dell'appliance  
Dopo l'avvio dell'appliance, aprire la **console di amministrazione** e controllare la pagina di integrità per individuare gli avvisi che potrebbero indicare condizioni di errore. Per altre informazioni, vedere [monitorare l'appliance usando la console di amministrazione &#40;&#41;di sistema della piattaforma di analisi ](monitor-the-appliance-by-using-the-admin-console.md).  
  
## <a name="see-also"></a>Vedere anche  
[Attività di gestione degli appliance &#40;sistema di piattaforma di analisi&#41;](appliance-management-tasks.md)  
  
