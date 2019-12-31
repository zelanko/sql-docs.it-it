---
title: Configurazione della rete delle appliance
description: L'appliance Analytics Platform System (APS) viene creata e configurata con un set di indirizzi IP di correzione in tutti i server e i dispositivi applicabili dal produttore del IHV. Al momento della consegna dell'appliance, è necessario riconfigurare l'IP esterno (Ethernet) per soddisfare i requisiti di data center specifici del cliente.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401414"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Configurazione di rete Appliance per il sistema di piattaforma Analytics
L'appliance Analytics Platform System (APS) viene creata e configurata con un set di indirizzi IP di correzione in tutti i server e i dispositivi applicabili dal produttore del IHV. Al momento della consegna dell'appliance, è necessario riconfigurare l'IP esterno (Ethernet) per soddisfare i requisiti di data center specifici del cliente.  
  
> [!NOTE]  
> PDW V1 richiede 8 indirizzi IP esterni (per i*clienti*) per fornire connettività esterna a ognuno dei nodi del rack di controllo. PDW 2012 (v2) Enhanced Network Communications esponendo ogni componente dell'appliance esternamente tramite indirizzi IP. Questo approccio offre una progettazione più affidabile che riduce i costi e aumenta la flessibilità e migliora lo spostamento dei dati, il caricamento dei dati e l'integrazione Hadoop. Il numero di indirizzi IP richiesti dipende dal numero di nodi nell'appliance. Per supportare questo blocco di indirizzi IP più ampio, il cliente deve configurare una subnet separata per PDW. All'interno di questa subnet sarà disponibile spazio di indirizzi IP sufficiente (fino a 250 indirizzi) per ospitare i componenti di un massimo di 5 rack PDW.  
  
La pagina **configurazione di rete** consente di visualizzare le impostazioni di rete rivolte all'esterno per i nodi nell'appliance del sistema della piattaforma di analisi. Questa pagina è di sola lettura.  
  
![Rete dello strumento DWConfig](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Per aggiornare la configurazione di rete nel dispositivo  
Modificare gli indirizzi IP del dominio dell'infrastruttura e del dominio del carico di lavoro modificando il file **AplianceInfo. XML** e quindi eseguendo il programma di installazione. Si tratta di un'operazione offline. Le aree PDW verranno interrotte automaticamente durante la modifica dell'indirizzo IP.  
  
> [!NOTE]  
> I nomi di dominio vengono forniti durante l'installazione e vengono specificati fino a 6 caratteri alfanumerici, a partire da una lettera. Un sistema di denominazione frequente crea un dominio di infrastruttura che inizia con F, un dominio del carico di lavoro PDW che inizia con P. Questo formato si presume negli argomenti del file della guida, ma non è obbligatorio. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Per modificare gli indirizzi IP del sistema della piattaforma di analisi  
  
1.  Utilizzando l'applicazione **Desktop remoto** , connettersi a **HST01** utilizzando l'account amministratore di dominio del carico di lavoro.  
  
2.  Nel nodo HST01 aprire il file di informazioni sull'appliance in **c:\pdwinst\media\AplianceInfo.XML**.  
  
    > [!NOTE]  
    > Se il file non è presente, potrebbe essere necessario creare un nuovo file.  
  
3.  Aggiornare i valori IP Ethernet in base alle esigenze e salvare il file.  
  
4.  In una finestra del prompt dei comandi eseguire il comando di configurazione seguente per aggiornare gli indirizzi IP per l'area PDW, usando i nomi di dominio P/F/H e le password di amministratore.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Riferimenti del produttore  
Per ulteriori informazioni sulle Appliance dell, vedere:  
  
-   Guida di riferimento per istruzioni switch PowerConnect [dell powerconnect 6200 Series](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   [manuale dell'utente di Idrac/BMC Integrated Dell Remote Access Controller 7 (iDRAC7) versione 1.30.30](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   **PDU rack a consumo dell** PDU`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Vedere anche  
[Avviare la piattaforma Configuration Manager &#40;Analytics System&#41;](launch-the-configuration-manager.md)  
  
