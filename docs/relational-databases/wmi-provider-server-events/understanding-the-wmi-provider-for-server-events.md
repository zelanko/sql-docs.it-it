---
title: Informazioni sul Provider WMI per eventi del Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56cacefdcc0afd1ff2b17986658b27d7f4eddb07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139217"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>Informazioni sul provider WMI per eventi del server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Il provider WMI per eventi del server consente di utilizzare il servizio Strumentazione gestione Windows (WMI) per monitorare eventi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo provider converte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un oggetto WMI gestito. Qualsiasi evento che può generare una notifica degli eventi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere utilizzato da WMI tramite questo provider. Come applicazione di gestione che interagisce con WMI, inoltre, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può rispondere a tali eventi, espandendo l'ambito degli eventi gestiti rispetto alle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Le applicazioni di gestione come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent possono accedere a eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando il provider WMI per eventi del server ed eseguendo istruzioni WQL (WMI Query Language). WQL è un subset semplificato del linguaggio SQL (Structured Query Language), con alcune estensioni specifiche di WMI. Utilizzando WQL, un'applicazione recupera un tipo di evento rispetto a un database o a un oggetto di database specifico. Il provider WMI per eventi del server converte la query in una notifica degli eventi, creando in modo efficace una notifica degli eventi nel database di destinazione. Per altre informazioni sul funzionamento delle notifiche degli eventi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [del Provider WMI per concetti degli eventi Server](https://technet.microsoft.com/library/ms180560.aspx). Sono elencati gli eventi che possono essere interrogati [Provider WMI per la proprietà e le classi di eventi Server](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
 Quando si verifica un evento che attiva la notifica degli eventi per inviare un messaggio, il messaggio viene inviato a un servizio di destinazione predefinito in **msdb** denominata **SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**. Il servizio inserisce l'evento in una coda predefinita in **msdb** denominata **WMIEventProviderNotificationQueue**. (Il servizio e la coda vengono creati dinamicamente dal provider quando si connette prima al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].) Quindi, il provider legge i dati dell'evento da questa coda e li trasforma in formato di oggetto gestito (MOF) prima di restituirlo all'applicazione. Questo processo viene illustrato nella figura seguente.  
  
 ![Diagramma di flusso del Provider WMI per eventi del Server](../../relational-databases/wmi-provider-server-events/media/wmi-provider-functional-spec.gif "diagramma di flusso del Provider WMI per eventi del Server")  
  
 Si consideri, ad esempio, la query WQL seguente:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 In risposta alla query, il provider WMI per eventi del server crea la notifica degli eventi equivalente nel database di destinazione:  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 In questo esempio, `SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` è un identificatore [!INCLUDE[tsql](../../includes/tsql-md.md)] costituito dal prefisso `SQLWEP_` e un GUID. `SQLWEP` crea un nuovo GUID per ogni identificatore. Il valore `A7E5521A-1CA6-4741-865D-826F804E5135` nella `TO SERVICE` clausola è il GUID che identifica l'istanza di Service broker nel **msdb** database.  
  
 Per altre informazioni su come utilizzare WQL, vedere [utilizzo di WQL con il Provider WMI per eventi del Server](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Le applicazioni di gestione indirizzano il provider WMI per eventi del server a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] connettendosi a uno spazio dei nomi WMI definito dal provider. Il servizio Windows WMI esegue il mapping di questo spazio dei nomi alla DLL del provider, Sqlwep.dll, e lo carica in memoria. Il provider gestisce uno spazio dei nomi WMI per eventi del Server per ogni istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e il formato è: \\ \\.\\ *radice*\Microsoft\SqlServer\ServerEvents\\*nome_istanza*, dove *nome_istanza* il valore predefinito è MSSQLSERVER. Per altre informazioni su come connettersi a uno spazio dei nomi WMI per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [utilizzo di WQL con il Provider WMI per eventi del Server](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 La DLL del provider, Sqlwep.dll, viene caricata solo una volta nel servizio host WMI del sistema operativo del server, indipendentemente dal numero di istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenti nel server.  
  
 Per un esempio di un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applicazione di gestione dell'agente che utilizza il Provider WMI per eventi del Server, vedere [esempio: Creazione di un avviso SQL Server Agent utilizzando il Provider WMI per eventi del Server](https://technet.microsoft.com/library/ms186385.aspx). Per un esempio di un'applicazione di gestione che usa il Provider WMI per eventi del Server nel codice gestito, vedere [esempio: Uso del Provider di eventi WMI in codice gestito](https://technet.microsoft.com/library/ms179315.aspx). Altre informazioni sono disponibili su WMI in anche il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi al provider WMI per eventi del server](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
