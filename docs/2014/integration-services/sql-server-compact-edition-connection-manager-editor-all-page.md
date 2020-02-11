---
title: Editor gestione connessione SQL Server Compact Edition (pagina tutti) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8a26587f9dd426cdf53a3a53a36d0e81e95ebf77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055472"
---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor gestione connessione SQL Server Compact Edition (pagina Tutte)
  Utilizzare la finestra di dialogo **Editor gestione connessione SQL Server Compact Edition** per specificare le proprietà di connessione a un database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 Per ulteriori informazioni sulla gestione connessione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact Edition, vedere [Editor gestione connessione SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **Soglia compattazione automatica**  
 Consente di specificare la quantità di spazio libero in percentuale consentito nel database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact al raggiungimento della quale verrà avviata l'operazione di compattazione automatica.  
  
 **Escalation blocchi predefinita**  
 Consente di specificare il numero di blocchi di database acquisiti dal database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact prima di tentare l'escalation.  
  
 **Timeout blocco predefinito**  
 Consente di specificare l'intervallo di tempo predefinito (in millisecondi) per cui una transazione deve rimanere in attesa di un blocco.  
  
 **Intervallo di scaricamento**  
 Consente di specificare l'intervallo di tempo (in secondi) dopo il quale le transazioni completate devono essere scaricate su disco.  
  
 **Identificatore delle impostazioni locali**  
 Consente di specificare l'ID delle impostazioni locali (LCID) del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Dimensioni massime buffer**  
 Consente di specificare la quantità massima di memoria in KB usata da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact al raggiungimento della quale viene eseguito lo scaricamento dei dati su disco.  
  
 **Dimensioni massime del database**  
 Consente di specificare le dimensioni massime in MB del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Mode**  
 Consente di specificare la modalità file in cui aprire il database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact. Il valore predefinito di questa proprietà è **Read Write**.  
  
 Nella tabella seguente sono descritti i quattro valori disponibili per la proprietà Mode.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Sola lettura**|Imposta l'accesso di sola lettura al database.|  
|**Lettura Scrittura**|Imposta l'autorizzazione di lettura/scrittura per il database.|  
|**Esclusivo**|Imposta l'accesso esclusivo al database.|  
|**Lettura condivisa**|Specifica che altri utenti possono accedere contemporaneamente in lettura al database.|  
  
 **Mantieni informazioni di sicurezza**  
 Consente di specificare se le informazioni di sicurezza vengono restituite all'interno della stringa di connessione. Il valore predefinito dell'opzione è **False**.  
  
 **Directory file temporanei**  
 Consente di specificare il percorso del file di database temporaneo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Origine dati**  
 Consente di specificare il nome del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Password**  
 Consente di immettere la password per il database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor gestione connessione SQL Server Compact Edition &#40;pagina connessione&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  
