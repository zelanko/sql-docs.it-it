---
title: Configurazione server - account di servizio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- service account configuration, SQL Server
ms.assetid: c283702d-ab20-4bfa-9272-f0c53c31cb9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8435b0c677f80bf4f26acd4411d90ab63c7473d1
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092265"
---
# <a name="server-configuration---service-accounts"></a>Configurazione Server - Account di servizio
  Utilizzare la pagina Configurazione del server dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per assegnare account di accesso ai servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I servizi effettivamente configurati in questa pagina dipendono dalle caratteristiche selezionate per l'installazione.  
  
 Gli account di avvio usati per avviare ed eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere account utente di dominio di collegamento ipertestuale "ms-help://SQL11_I1033/s11sq_GetStart_I/html/309b9dac-0b3a-4617-85ef-c4519ce9d014.htm" \l "Domain_User", gli account utente locali, account del servizio gestiti, gli account virtuali o account di sistema predefiniti.  
  
## <a name="options"></a>Opzioni  
 È possibile assegnare lo stesso account di accesso a tutti i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oppure configurare singolarmente l'account di ogni servizio. È inoltre possibile specificare se i servizi verranno avviati automaticamente, manualmente o se sono disabilitati. Per la maggior parte delle installazioni l'account consigliato è quello predefinito.  
  
 In Windows 7 e [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 la maggior parte degli account viene impostata automaticamente su un account virtuale.  
  
 Se si configurano i servizi per l'utilizzo di account di dominio, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di configurare singolarmente gli account del servizio per fornire privilegi minimi per ogni servizio, in modo che i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispongano delle autorizzazioni minime necessarie per completare le attività. Per altre informazioni, incluse le descrizioni dei tipi di account, vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
 **Configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] singolarmente gli account del servizio (scelta consigliata)**  
 Utilizzare la griglia per fornire a ogni servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un nome utente di accesso e una password e per impostare il tipo di avvio per il servizio. Per i servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile utilizzare account di sistema predefiniti, un account locale, un gruppo locale, un gruppo di dominio o account utente di dominio.  
  
 Selezionare i servizi seguenti per personalizzarne le impostazioni.  
  
|Selezionare questo servizio|Per personalizzare le impostazioni di autenticazione per|  
|-------------------------|----------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent|Il servizio che esegue processi e il monitoraggio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e che consente l'automazione di attività di amministrazione.<br /><br /> Per questo servizio non è disponibile alcun account di accesso predefinito.<br /><br /> Il tipo di avvio predefinito è Manuale.|  
|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|Il tipo di avvio predefinito è Automatico.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Il tipo di avvio predefinito è Automatico.<br /><br /> Per la modalità integrata SharePoint è necessario specificare un account utente di dominio di Windows. L'account specificato viene utilizzato per il servizio di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. L'account specificato per l'istanza corrente deve essere utilizzato anche per qualsiasi altra istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che si aggiunge successivamente alla stessa farm.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Gli account di servizio vengono utilizzati per configurare una connessione al database del server di report. Scegliere il servizio di rete predefinito se si desidera utilizzare impostazioni di autenticazione predefinite. Se si specifica un account utente di dominio, registrare un nome SPN (Service Principle Name) se si utilizza l'autenticazione di Windows nel server di report. Per altre informazioni, vedere [Configurare l'autenticazione di Windows nel server di report](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).<br /><br /> Il tipo di avvio predefinito è Automatico.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è un set di strumenti grafici e oggetti programmabili per lo spostamento, la copia e la trasformazione di dati.<br /><br /> Il tipo di avvio predefinito è Automatico.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client|Account di servizio utilizzato per il servizio client Riesecuzione distribuita.<br /><br /> Specificare un account con cui eseguire il servizio client Riesecuzione distribuita. Questo account dovrebbe essere diverso dall'account utilizzato per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Il tipo di avvio predefinito è Manuale.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller|Account di servizio utilizzato per il servizio controller di Riesecuzione distribuita.<br /><br /> Specificare un account con cui eseguire il servizio controller di Riesecuzione distribuita. Questo account dovrebbe essere diverso dall'account utilizzato per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Il tipo di avvio predefinito è Manuale.|  
|Utilità di avvio del daemon di filtri full-text di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Servizio che crea i processi fdhost.exe. È necessario per ospitare i filtri e i word breaker che elaborano i dati testuali per l'indicizzazione full-text.<br /><br /> Se si specifica un account di dominio in cui eseguire il servizio per l'utilità di avvio di FDHOST, è consigliabile utilizzare un account con privilegi limitati. Questo account dovrebbe essere diverso dall'account utilizzato per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser è il servizio di risoluzione dei nomi che rende disponibili le informazioni di connessione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i computer client. Questo servizio viene condiviso da più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . L'account di accesso predefinito è NT Authority\Local service e non può essere modificato durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile modificare l'account dopo che l'installazione è stata completata. Se non specificato durante l'installazione, il tipo di avvio viene determinato nel modo seguente:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser viene impostato su Automatico e viene eseguito negli scenari di installazione descritti di seguito.<br />-<br />                            Istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br />-<br />                            Istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è abilitato TCP o NP<br />-<br />                            Istanza denominata di Analysis Server senza cluster<br /><br /> Se lo scenario di installazione non è uno di quelli descritti in precedenza e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser è già installato, verrà mantenuto lo stato corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser.<br /><br /> Il tipo di avvio viene impostato su Disabilitato e viene arrestato se non è presente alcuna istanza di una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedente all'installazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
