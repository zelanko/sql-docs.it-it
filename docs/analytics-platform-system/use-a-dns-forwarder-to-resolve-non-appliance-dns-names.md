---
title: Utilizzare un server d'inoltro DNS nel sistema di piattaforma Analitica | Microsoft Docs"
description: Usare un server d'inoltro DNS per risolvere i nomi DNS non appliance nel sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6ce978d7b05382b1a02018f3d5022b0f8bfaf585
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63243783"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Usare un server d'inoltro DNS per risolvere i nomi DNS Non Appliance nel sistema di piattaforma Analitica
Un server d'inoltro DNS può essere configurato nei nodi di servizi di dominio Active Directory (**_appliance\_domain_-AD01** e  **_appliance\_ dominio_-AD02**) del dispositivo di sistema di piattaforma Analitica per consentire gli script e applicazioni software per accedere ai server esterni.  
  
## <a name="ResolveDNS"></a>Usando un server d'inoltro DNS  
L'appliance del sistema di piattaforma Analitica è configurato per impedire la risoluzione dei nomi DNS del server che non sono nell'appliance. Alcuni processi, ad esempio Windows Software Update Services (WSUS), saranno necessario accedere ai server all'esterno dell'appliance. Per supportare questo scenario di utilizzo del DNS di sistema di piattaforma Analitica può essere configurato per supportare un server d'inoltro nome esterno che consentirà al sistema di piattaforma Analitica host e macchine virtuali (VM) usare server DNS esterni per la risoluzione dei nomi all'esterno dell'appliance. Configurazione personalizzata dei suffissi DNS non è supportata, ovvero che è necessario utilizzare nomi di dominio completo per risolvere un nome di server non appliance.  
  
**Per creare un server d'inoltro DNS con l'interfaccia utente grafica di DNS**  
  
1.  Eseguire l'accesso di  **_appliance\_domain_-AD01** nodo.  
  
2.  Aprire Gestore DNS (**dnsmgmt. msc**).  
  
3.  Fare doppio clic il nome del server e quindi fare clic su **proprietà**.  
  
4.  Scegliere il **avanzate** scheda, deselezionare il **disabilitare la ricorsione (anche disabilita i server d'inoltro)** opzione e quindi fare clic su **applica**.)  
  
5.  Scegliere il **i server d'inoltro** scheda e quindi fare clic su **modificare**.  
  
6.  Immettere l'indirizzo IP per il server DNS esterno che fornisce la risoluzione dei nomi. Le macchine virtuali e server (host) nell'appliance si connetterà a server esterni usando nomi di dominio completo.  
  
7.  Ripetere i passaggi da 1 a 6 sul  **_appliance\_domain_-AD02** nodo  
  
**Per creare un server d'inoltro DNS usando Windows PowerShell**  
  
1.  Eseguire l'accesso di  **_appliance\_domain_-AD01**nodo.  
  
2.  Eseguire lo script di Windows PowerShell seguente dal  **_appliance\_domain_-AD01** nodo. Prima di eseguire lo script di Windows PowerShell, sostituire gli indirizzi IP con gli indirizzi IP dei server DNS non appliance.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Eseguire lo stesso comando sul  **_appliance\_domain_-AD02** nodo.  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Configurazione della risoluzione DNS per Windows Server Update Services  
SQL Server 2012 PDW fornisce la funzionalità dell'applicazione di patch e manutenzione integrata. SQL Server PDW Usa Microsoft Update e altre tecnologie di manutenzione di Microsoft. Per abilitare gli aggiornamenti dell'appliance deve essere in grado di connettersi a un repository azienda di Windows Server Update Services o nel repository di Windows Server Update Services pubblico di Microsoft.  
  
Per i clienti che sceglie di configurare l'appliance per cercare gli aggiornamenti nel repository pubblico Microsoft Windows Server Update Services, le istruzioni seguenti impostare i dettagli di una configurazione appropriata nell'appliance.  
  
> [!NOTE]  
> L'amministratore di rete del cliente deve fornire l'indirizzo IP per un server DNS aziendale in grado di risolvere i nomi in **Microsoft.com**.  
  
1.  Uso di desktop remoto, accedere a VM di VMM (<fabric domain>- VMM) usando l'account di amministratore di dominio di fabric.  
  
2.  Aprire il pannello di controllo, fare clic su **rete e Internet**, quindi fare clic su **centro rete e condivisione**.  
  
3.  Nell'elenco delle connessioni, fare clic su **VMSEthernet**, quindi fare clic su **proprietà**.  
  
4.  Selezionare **Internet Protocol versione 4 (TCP/IPv4)**, quindi fare clic su **proprietà**.  
  
5.  Nel **server DNS alternativo** , aggiungere l'indirizzo IP fornito dall'amministratore di rete del cliente.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
