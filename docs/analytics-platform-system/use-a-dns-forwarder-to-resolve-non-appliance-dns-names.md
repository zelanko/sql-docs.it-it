---
title: Usare un server d'avanzamento DNS
description: Usare un server d'invio DNS per risolvere i nomi DNS non Appliance nel sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399429"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Usare un server d'invio DNS per risolvere i nomi DNS non Appliance nel sistema della piattaforma Analytics
È possibile configurare un server d'autorizzazione DNS nei nodi Active Directory Domain Services (**_Appliance\_Domain_-ad01** e ** _Appliance\_Domain_-ad02**) dell'appliance del sistema della piattaforma di analisi per consentire agli script e alle applicazioni software di accedere ai server esterni.  
  
## <a name="ResolveDNS"></a>Uso di un server d'inoltre DNS  
L'appliance del sistema della piattaforma Analytics è configurata in modo da impedire la risoluzione dei nomi DNS dei server che non si trovano nell'appliance. Alcuni processi, ad esempio Windows Software Update Services (WSUS), dovranno accedere ai server all'esterno dell'appliance. Per supportare questo scenario di utilizzo, è possibile configurare il DNS del sistema della piattaforma di analisi in modo da supportare un server d'utilità di un nome esterno che consenta agli host e alle macchine virtuali di sistema della piattaforma di analisi di usare server DNS esterni per risolvere i nomi all'esterno dell'appliance. La configurazione personalizzata dei suffissi DNS non è supportata, quindi è necessario usare nomi di dominio completi per risolvere un nome di server non Appliance.  
  
**Per creare un server di trasmissione DNS con l'interfaccia utente grafica DNS**  
  
1.  Accedere al nodo ** _Domain\__-ad01 del dispositivo** .  
  
2.  Aprire il gestore DNS (**dnsmgmt. msc**).  
  
3.  Fare clic con il pulsante destro del mouse sul nome del server e quindi scegliere **Proprietà**.  
  
4.  Nella scheda **Avanzate** deselezionare l'opzione **Disabilita ricorsione (Disabilita anche i server d'inoltri)** e quindi fare clic su **applica**.  
  
5.  Fare clic sulla scheda **server d'avanzamento** e quindi su **modifica**.  
  
6.  Immettere l'indirizzo IP del server DNS esterno che fornirà la risoluzione dei nomi. Le macchine virtuali e i server (host) nell'appliance si connetteranno a server esterni usando nomi di dominio completi.  
  
7.  Ripetere i passaggi 1-6 nel nodo ** _dominio Appliance\__-ad02**  
  
**Per creare un server d'inoltre DNS usando Windows PowerShell**  
  
1.  Accedere al nodo ** _Domain\__-ad01 del dispositivo**.  
  
2.  Eseguire lo script di Windows PowerShell seguente dal nodo ** _dominio Appliance\__-ad01** . Prima di eseguire lo script di Windows PowerShell, sostituire gli indirizzi IP con gli indirizzi IP dei server DNS non Appliance.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Eseguire lo stesso comando nel nodo ** _Domain\__-ad02 del dispositivo** .  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Configurazione della risoluzione DNS per WSUS  
SQL Server PDW 2012 fornisce funzionalità integrate di manutenzione e applicazione di patch. SQL Server PDW utilizza Microsoft Update e altre tecnologie di manutenzione Microsoft. Per abilitare gli aggiornamenti è necessario che il dispositivo sia in grado di connettersi a un repository WSUS aziendale o al repository WSUS pubblico Microsoft.  
  
Per i clienti che scelgono di configurare l'appliance per la ricerca di aggiornamenti nel repository WSUS pubblico Microsoft, le istruzioni seguenti consentono di impostare i dettagli di configurazione appropriati nell'appliance.  
  
> [!NOTE]  
> L'amministratore di rete del cliente deve fornire l'indirizzo IP di un server DNS aziendale in grado di risolvere i nomi in **Microsoft.com**.  
  
1.  Usando desktop remoto, accedere alla VM VMM (<fabric domain>-VMM) usando l'account di amministratore di dominio dell'infrastruttura.  
  
2.  Aprire il pannello di controllo, fare clic su **rete e Internet**e quindi fare clic su **Centro rete e condivisione**.  
  
3.  Nell'elenco connessione fare clic su **VMSEthernet**, quindi su **Proprietà**.  
  
4.  Selezionare **Protocollo Internet versione 4 (TCP/IPv4)** e quindi fare clic su **Proprietà**.  
  
5.  Nella casella **server DNS alternativo** aggiungere l'indirizzo IP fornito dall'amministratore di rete del cliente.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
