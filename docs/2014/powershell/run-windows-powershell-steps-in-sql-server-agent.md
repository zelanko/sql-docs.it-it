---
title: Eseguire passaggi di Windows PowerShell in SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 460d66b7e2d4f314db65213819fca1800af2da4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62922900"
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>Esecuzione di passaggi di Windows PowerShell in SQL Server Agent
  Utilizzare SQL Server Agent per eseguire script di SQL Server PowerShell a orari pianificati.  
  
1.  **Prima di iniziare:**  [limitazioni e restrizioni](#LimitationsRestrictions)  
  
2.  **Per eseguire PowerShell da SQL Server Agent, usando: passaggio del processo di**  [PowerShell](#PShellJob), passaggio del processo del prompt dei [comandi](#CmdExecJob)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Sono disponibili molti tipi di passaggi del processo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent. Ogni tipo è associato a un sottosistema che implementa un ambiente specifico, ad esempio un agente di replica o un ambiente del prompt dei comandi. È possibile codificare gli script di Windows PowerShell, quindi utilizzare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent per includere gli script nei processi eseguiti in base a orari pianificati o in risposta a eventi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . È possibile eseguire gli script di Windows PowerShell con un passaggio del processo del prompt dei comandi o di PowerShell.  
  
1.  Utilizzare un passaggio del processo di PowerShell per fare in modo che il sottosistema [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent esegua l'utilità `sqlps`, che avvia PowerShell 2.0 e importa il modulo `sqlps`.  
  
2.  Utilizzare un passaggio del processo del prompt dei comandi per eseguire PowerShell.exe e specificare uno script che importa il modulo `sqlps`.  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
  
> [!CAUTION]  
>  Ogni passaggio del processo di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent che esegue PowerShell con il modulo `sqlps` avvia un processo che utilizza all'incirca 20 MB di memoria. L'esecuzione simultanea di numerosi passaggi del processo di Windows PowerShell può avere un impatto negativo sulle prestazioni.  
  
##  <a name="PShellJob"></a>Creazione di un passaggio del processo di PowerShell  
 **Per creare un passaggio di processo di PowerShell**  
  
1.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**. Per ulteriori informazioni sulla creazione di un processo, vedere [Creazione di processi](../ssms/agent/create-jobs.md).  
  
2.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
3.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
4.  Scegliere **PowerShell** dall'elenco **Tipo**.  
  
5.  Nell'elenco **Esegui come** selezionare l'account proxy con le credenziali che verranno utilizzate dal processo.  
  
6.  Nella casella **Comando** immettere la sintassi dello script di PowerShell che verrà eseguito per il passaggio di processo. In alternativa, è possibile fare clic su **Apri** e selezionare un file contenente la sintassi dello script.  
  
7.  Fare clic sulla pagina **Avanzate** per impostare le opzioni seguenti relative al passaggio di processo: l'azione da eseguire in caso di esito positivo o negativo del passaggio, il numero di tentativi di esecuzione del passaggio che devono essere effettuati da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent e gli intervalli tra tentativi successivi.  
  
##  <a name="CmdExecJob"></a>Creazione di un passaggio del processo del prompt dei comandi  
 **Per creare un passaggio di processo CmdExec**  
  
1.  Espandere **SQL Server Agent**, creare un nuovo processo oppure fare clic con il pulsante destro del mouse su un processo esistente e quindi scegliere **Proprietà**. Per ulteriori informazioni sulla creazione di un processo, vedere [Creazione di processi](../ssms/agent/create-jobs.md).  
  
2.  Nella finestra di dialogo **Proprietà processo** fare clic sulla pagina **Passaggi** e quindi su **Nuovo**.  
  
3.  Nella finestra di dialogo **Nuovo passaggio di processo** digitare il nome del passaggio del processo nella casella **Nome passaggio**.  
  
4.  Nell'elenco **Tipo** selezionare **Sistema operativo (CmdExec)**.  
  
5.  Nell'elenco **Esegui come** selezionare l'account proxy con le credenziali che verranno utilizzate dal processo. Per impostazione predefinita, questi passaggi di processo vengono eseguiti nel contesto dell'account di servizio SQL Server Agent.  
  
6.  Nella casella **Elabora codice di uscita di un comando eseguito correttamente** digitare un valore compreso tra 0 e 999999.  
  
7.  Nella casella **Comando** , immettere powershell.exe con parametri che specificano lo script di PowerShell da eseguire.  
  
8.  Fare clic sulla pagina **Avanzate** per impostare le opzioni relative ai passaggi di processo, ad esempio l'operazione da eseguire se il passaggio di processo ha esito positivo o negativo, il numero di tentativi che devono essere eseguiti da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent per l'esecuzione del passaggio di processo e il file in cui [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent può scrivere l'output del passaggio di processo. L'output del passaggio di processo può essere scritto in un file di sistema unicamente dai membri del ruolo predefinito del server **sysadmin** .  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
