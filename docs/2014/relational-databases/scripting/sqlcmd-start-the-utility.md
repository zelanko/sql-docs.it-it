---
title: Avvio dell'utilità sqlcmd
ms.custom: seo-lt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 00d57437-7a29-4da1-b639-ee990db055fb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 80f8f63b4ddb3e8641ef503a615d57c63be35164
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243273"
---
# <a name="start-the-sqlcmd-utility"></a>Avvio dell'utilità sqlcmd
  Per iniziare a utilizzare `sqlcmd`, è innanzitutto necessario avviare l'utilità e connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile connettersi a un'istanza predefinita oppure a un'istanza denominata. Il primo passaggio consiste nell'avvio dell'utilità `sqlcmd`.  
  
> [!NOTE]  
>  La modalità di autenticazione predefinita per l'utilità `sqlcmd` è l'autenticazione di Windows. Per usare l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario specificare un nome utente e una password con le opzioni **-U** e **-P** .  
  
> [!NOTE]  
>  Per impostazione predefinita, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] viene installato come istanza denominata **sqlexpress**.  
  
 Se non ci si è mai connessi a questa istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], potrebbe essere necessario configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accettare connessioni.  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-default-instance-of-sql-server"></a>Per avviare l'utilità sqlcmd e connettersi a un'istanza predefinita di SQL Server  
  
1.  Dal menu **Start** fare clic su **Esegui**. Nella casella **Apri** digitare **cmd**e quindi fare clic su **OK** per aprire una finestra del prompt dei comandi.  
  
2.  Al prompt dei comandi digitare `sqlcmd`.  
  
3.  Premere INVIO.  
  
     Verrà quindi stabilita una connessione trusted all'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione nel computer in uso.  
  
     **1>** è il `sqlcmd` prompt che specifica il numero di riga. Il numero viene aumentato di un'unità ogni volta che si preme INVIO.  
  
4.  Per terminare la `sqlcmd` sessione, digitare `EXIT` al `sqlcmd` prompt.  
  
### <a name="to-start-the-sqlcmd-utility-and-connect-to-a-named-instance-of-sql-server"></a>Per avviare l'utilità sqlcmd e connettersi a un'istanza denominata di SQL Server  
  
1.  Aprire una finestra del prompt dei comandi e `sqlcmd -S`Digitare *myServer\instanceName*. Sostituire *server\nomeIstanza* con il nome del computer e dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui ci si vuole connettere.  
  
2.  Premere INVIO.  
  
     Il `sqlcmd` prompt (1>) indica che si è connessi all'istanza specificata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] immesse vengono archiviate in un buffer. Vengono eseguite in batch quando viene rilevato il comando GO.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire file script Transact-SQL tramite sqlcmd](sqlcmd-run-transact-sql-script-files.md)  
  
  
