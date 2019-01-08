---
title: Strumenti esterni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a69ead28479ba16df7439d6e551163be48737562
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328571"
---
# <a name="external-tools"></a>Strumenti esterni
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Usare questa finestra di dialogo per aggiungere strumenti esterni, ad esempio Gestione configurazione SQL Server o Blocco note, al menu **Strumenti** . Aggiungendo strumenti esterni, sarà più semplice avviare altre applicazioni quando si utilizza [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Durante l'avvio dello strumento, è possibile specificare argomenti e una directory di lavoro. Gli output generati da alcuni strumenti verranno inoltre visualizzati nella finestra di output. La finestra di dialogo **Strumenti esterni** è accessibile dal menu **Strumenti** .  
  
## <a name="options"></a>Opzioni  
**Contenuto menu**  
Elenca i titoli degli elementi attualmente aggiunti al menu **Strumenti** . Usare i pulsanti **Sposta su** e **Sposta giù** per cambiare l'ordine di visualizzazione delle voci nel menu. Usare il pulsante **Elimina** per rimuovere una voce dal menu.  
  
**Sposta su**  
Sposta lo strumento selezionato più in alto nell'elenco degli strumenti visualizzati nel menu **Strumenti** .  
  
**Sposta giù**  
Sposta lo strumento selezionato più in basso nell'elenco degli strumenti visualizzati nel menu **Strumenti** .  
  
**Aggiungi**  
Consente di cancellare il contenuto delle caselle di testo e quindi di specificare un nuovo strumento.  
  
**Elimina**  
Rimuove lo strumento o il comando dall'elenco **Contenuto menu** e dal menu **Strumenti** .  
  
**Title**  
Nome dello strumento o del comando che verrà visualizzato nel sottomenu **Strumenti esterni** del menu **Strumenti** . Nel nome dello strumento inserire una "e" commerciale prima della lettera che si desidera utilizzare come tasto di scelta rapida per lo strumento. Ad esempio, specificando `&Spy++` , nel menu **Strumenti** verrà visualizzato **Spy++** .  
  
**Command**  
Consente di specificare il percorso del file con estensione exe, com, pif, bat, cmd o di altro tipo che si desidera avviare. L'output generato da file `.bat`, `.com`e file con altre estensioni potrà essere visualizzato nella finestra di output se si seleziona la casella di controllo **Usa finestra di output** .  
  
**Argomenti**  
Consente di specificare le variabili passate allo strumento quando questo viene selezionato dal menu. Negli argomenti possono essere specificati valori che vengono passati allo strumento o al comando all'avvio. Un valore può ad esempio specificare un nome di file o una directory. Usare il pulsante **Freccia** per eseguire una selezione da un elenco di argomenti predefiniti. È possibile aggiungere più argomenti. Per un elenco completo degli argomenti predefiniti e delle relative definizioni, vedere [Strumenti esterni - Argomenti](../../ssms/use-of-sql-server-features-and-capabilities-wwi-oltp.md). È inoltre possibile immettere argomenti personalizzati, ad esempio opzioni del prompt dei comandi, a seconda del comando o dello strumento in uso.  
  
**Directory iniziale**  
Consente di specificare la directory di lavoro dello strumento. Usare il pulsante **Freccia** per selezionare le directory. È possibile selezionare più directory.  
  
**Use output Window**  
Consente di specificare se i risultati generati dallo strumento debbano essere visualizzati nella finestra di output. L'opzione è disponibile solo per i file, ad esempio file con estensione bat e com, i cui output vengono generalmente visualizzati nella finestra del prompt dei comandi. Se abilitata, questa opzione semplifica la gestione delle finestre durante l'analisi delle operazioni effettuate da uno strumento.  
  
**Richiedi argomenti**  
Visualizza la finestra di dialogo **Argomenti** , in cui è possibile specificare o modificare i valori degli argomenti a ogni avvio dello strumento esterno.  
  
**Considera output come Unicode**  
Consente di accettare caratteri Unicode nella finestra di output.  
  
**Chiudi all'uscita**  
Chiude la finestra aperta dallo strumento quando viene chiuso lo strumento stesso.  
  
## <a name="example"></a>Esempio  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>Per aggiungere Gestione configurazione SQL Server al menu Strumenti  
  
1.  Scegliere **Strumenti esterni** dal menu **Strumenti**.  
  
2.  Nella casella **Titolo** digitare **Gestione configurazione SQL Server**.  
  
3.  Nella casella **Comando** digitare il percorso del file eseguibile di [!INCLUDE[msCoName](../../includes/msconame_md.md)] Management Console, ad esempio **C:\WINNT\system32\mmc.exe**  
  
4.  Nella casella **Argomenti** digitare il percorso del file con estensione msc, ad esempio **"C:\WINNT\system32\SQLServerManager.msc"**  
  
> [!NOTE]  
> Visualizzare le proprietà del collegamento [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nel menu **Avvio** per verificare il percorso dei file nel computer.  
