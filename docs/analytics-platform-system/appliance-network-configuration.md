---
title: Configurazione di rete Appliance - sistema di piattaforma Analitica | Microsoft Docs
description: L'appliance di Analitica piattaforma di strumenti analitici creata e configurata con un set di correzione degli indirizzi IP in tutti i server e dispositivi applicabili dal produttore del fornitore IHV. Dopo la consegna dell'appliance, è necessario riconfigurare l'indirizzo IP esterno (Ethernet) indirizzato in base ai requisiti di centro dati del cliente specifico.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: dc0fbd64ac1179cc77e5b8a3cf9f0e5fed73d7fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63276122"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Configurazione di rete Appliance per il sistema di piattaforma Analitica
L'appliance di Analitica piattaforma di strumenti analitici creata e configurata con un set di correzione degli indirizzi IP in tutti i server e dispositivi applicabili dal produttore del fornitore IHV. Dopo la consegna dell'appliance, è necessario riconfigurare l'indirizzo IP esterno (Ethernet) indirizzato in base ai requisiti di centro dati del cliente specifico.  
  
> [!NOTE]  
> PDW V1 necessari 8 IP esterno (*cliente rivolta*) gli indirizzi per fornire connettività esterna a ogni controllo rack di nodi. 2012 PDW (V2) migliorata delle comunicazioni di rete tramite l'esposizione di ogni componente dell'appliance esternamente tramite gli indirizzi IP. Questo approccio offre una progettazione più affidabile che consente di ridurre i costi, aumenta la flessibilità e consente di migliorare lo spostamento dei dati, il caricamento dei dati e l'integrazione di Hadoop. Il numero di indirizzi IP necessari dipende dal numero di nodi nell'appliance. Per ospitare questo blocco più grande di indirizzi IP, il cliente deve configurare una subnet separata per PDW. All'interno della subnet, ci sarà sufficiente spazio di indirizzi IP (al massimo 250 indirizzi) per contenere i componenti di rack PDW fino a 5.  
  
Il **configurazione di rete** pagina consente di visualizzare le impostazioni di rete accessibile pubblicamente per i nodi nel dispositivo di sistema di piattaforma Analitica. Questa pagina è di sola lettura.  
  
![DWConfig Appliance Network](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Per aggiornare la configurazione di rete del dispositivo  
Modificare gli indirizzi IP del dominio dell'infrastruttura e il dominio del carico di lavoro modificando la **AplianceInfo.xml** file e quindi eseguendo il programma di installazione. Si tratta di un'operazione offline. Le aree PDW verranno automaticamente arrestate durante la modifica dell'indirizzo IP.  
  
> [!NOTE]  
> I nomi di dominio vengono forniti durante l'installazione e vengono specificati come un massimo di 6 caratteri alfanumerici, inizia con una lettera. Un sistema di denominazione frequenti crea un dominio di fabric a partire da F, un dominio di carico di lavoro PDW partire P. Questo formato si presuppone che tutta la Guida di file ma non è obbligatorio. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Per modificare gli indirizzi IP del sistema di piattaforma Analitica  
  
1.  Usando il **Desktop remoto** dell'applicazione, connettersi **HST01** usando l'account di amministratore di dominio del carico di lavoro.  
  
2.  Nel nodo HST01, aprire il file info appliance **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Se il file non è presente, potrebbe essere necessario un nuovo file da creare.  
  
3.  Aggiornare i valori Ethernet IP in base alle esigenze e salvare il file.  
  
4.  In una finestra del prompt dei comandi eseguire il comando di configurazione seguente per aggiornare gli indirizzi IP per l'area PDW, usando i nomi di dominio di P/F/H e le password dell'amministratore.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Riferimenti produttore  
Per altre informazioni sulle Appliance di Dell, vedere:  
  
-   Le istruzioni Switch PowerConnect [Guida di riferimento Dell PowerConnect 6200 serie sistema CLI](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [manuale dell'utente versione 1.30.30 integrata Dell accesso remoto Controller 7 (iDRAC7)](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU **Dell misurati Rack PDU**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Vedere anche  
[Avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md)  
  
