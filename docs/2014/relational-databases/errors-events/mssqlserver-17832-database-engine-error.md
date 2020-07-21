---
title: MSSQLSERVER_17832 | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17828 (Database Engine error)
- maxtokensize
- 17832 (Database Engine error)
- login packet (bad)
ms.assetid: bd56ffe4-0855-4ada-8aca-251fbc6ff2ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: be82900146be4b20fb68960350959ae3b2135076
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86553606"
---
# <a name="mssqlserver_17832"></a>MSSQLSERVER_17832
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|17832|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SRV_BAD_LOGIN_PKT|  
|Testo del messaggio|La struttura del pacchetto di accesso utilizzato per aprire la connessione non è valido. La connessione è stata chiusa. Contattare il fornitore della libreria client.%.*ls|  
  
## <a name="explanation"></a>Spiegazione  
 Il computer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di elaborare il pacchetto di accesso client in quanto quest'ultimo potrebbe essere stato creato in modo errato o danneggiato durante la trasmissione. La mancata elaborazione può essere causata anche dalla configurazione del computer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'indirizzo IP elencato è l'indirizzo del computer client.  
  
### <a name="more-information"></a>Altre informazioni  
 In caso di utilizzo dell'autenticazione di Windows in un ambiente Kerberos, un client riceve un ticket Kerberos che contiene un certificato attributi privilegi. Tale certificato contiene vari tipi di dati sull'autorizzazione, inclusi i gruppi di cui l'utente è membro, i diritti di cui dispone e i criteri validi. Quando il client riceve il ticket Kerberos, le informazioni contenute nel certificato attributi privilegi vengono utilizzate per generare il token di accesso dell'utente. Il client presenta il token al computer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come parte del pacchetto di accesso.  
  
 Se il token è stato creato in modo errato o è stato danneggiato durante la trasmissione, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non sono disponibili informazioni aggiuntive sul problema.  
  
 Quando l'utente è un membro di molti gruppi o dispone di molti criteri, è possibile che il token diventi più grande del normale per elencarli tutti. Se il token diventa più grande del valore di **MaxTokenSize** del computer server, il client non riesce a connettersi con un errore di rete generale ed è possibile che venga generato l'errore 17832. Questo problema può interessare solo alcune categorie di utenti, ovvero coloro che dispongono di molti gruppi o criteri. Se il problema è il valore di **MaxTokenSize** del computer server, l'errore 17832 nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sarà accompagnato da un errore con lo stato 9. Per altri dettagli su Kerberos e **MaxTokenSize**, vedere [KB327825](https://support.microsoft.com/kb/327825).  
  
## <a name="user-action"></a>Azione dell'utente  
 Per risolvere questo problema, aumentare il valore di **MaxTokenSize** del computer server in modo da impostarlo su una dimensione sufficientemente ampia da contenere il token più grande di qualsiasi utente dell'organizzazione. Per identificare la dimensione del token appropriata per la propria organizzazione, usare l'applicazione **Tokensz**.   
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 **Per modificare il MaxTokenSize nel computer server**  
  
1.  Fare clic sul menu **Start** e scegliere **Esegui**.  
  
2.  Digitare `regedit` e quindi fare clic su **OK**. Se viene visualizzata la finestra di dialogo **Controllo account utente**, fare clic su **Continua**.  
  
3.  Passare a **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\Kerberos\Parameters**.  
  
4.  Se il parametro **MaxTokenSize** non è presente, fare clic con il pulsante destro del mouse su **Parametri**, scegliere **Nuovo** e quindi fare clic su **Valore DWORD (32 bit)** . Assegnare alla voce del Registro di sistema il nome **MaxTokenSize**.  
  
5.  Fare clic con il pulsante destro del mouse su **MaxTokenSize** e quindi scegliere **Modifica**.  
  
6.  Nella casella **Dati valore** digitare il valore di **MaxTokenSize** desiderato.  
  
    > [!NOTE]  
    >  Il valore esadecimale ffff (valore decimale 65535) rappresenta la dimensione massima del token consigliata. L'indicazione di questo valore potrebbe risolvere il problema, ma avere al tempo stesso effetti negativi sul computer relativamente alle prestazioni. È consigliabile impostare il valore minimo di **MaxTokenSize** che consente di ottenere il token più grande di qualsiasi utente nell'organizzazione e immettere quindi tale valore.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
8.  Chiudere l'**Editor del Registro di sistema**.  
  
9. Riavviare il computer.  
  
  
