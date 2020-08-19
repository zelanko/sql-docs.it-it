---
description: Introduzione con la console di SSMA per Sybase (SybaseToSQL)
title: Introduzione con la console di SSMA per Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Launching SSMA Console
- Sybase Console,Output Conventions
- Sybase Console,Procedure for Using Console
ms.assetid: 43219dbe-bcfa-427d-9242-f07b1455f15f
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e59cb5565ca518dc927f29e684401bf8fc6d5822
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418317"
---
# <a name="getting-started-with-the-ssma-for-sybase-console-sybasetosql"></a>Introduzione con la console di SSMA per Sybase (SybaseToSQL)
Questa sezione descrive la procedura per avviare e iniziare a usare l'applicazione console SSMA per Sybase. Sono inoltre elencate le convenzioni usate in una tipica finestra di output della console di SSMA.  
  
## <a name="launching-the-ssma-console"></a>Avvio della console di SSMA  
Per avviare l'applicazione console SSMA, attenersi alla procedura seguente:  
  
1.  Passare a Start, quindi scegliere tutti i programmi.  
  
2.  Fare clic sul collegamento del **prompt dei comandi SQL Server Migration Assistant per Sybase** .  
  
    Viene visualizzato il menu di utilizzo della console SSMA e, che consente di iniziare a `(/? Help)` usare l'applicazione console.  
  
## <a name="using-the-ssma-console"></a>Uso della console di SSMA  
Dopo che la console è stata avviata correttamente nel sistema Windows, è possibile utilizzare la procedura seguente per lavorare su di essa:  
  
1.  Configurare la console SSMA tramite i file di script. Per ulteriori informazioni su questa sezione, vedere [creazione di file di Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
2.  [Creazione di file di valori di variabile &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-variable-value-files-sybasetosql.md)  
  
3.  [Creazione dei file di connessione del server &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
4.  [L'esecuzione della console SSMA &#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) in base alle esigenze del progetto. 
  
Altre funzionalità:  
  
1.  [Specificare una password](managing-passwords-sybasetosql.md) e esportarla/importarla in altri computer Windows.  
  
2.  [Generare report](generating-reports-sybasetosql.md) per visualizzare i report di output XML dettagliati per la valutazione, la conversione e la migrazione dei dati. È anche possibile generare report di errore dettagliati per i comandi di aggiornamento e sincronizzazione.  
  
## <a name="ssma-console-output-conventions"></a>Convenzioni di output della console SSMA  
Quando si eseguono i comandi e le opzioni di script di SSMA, il programma console Visualizza i risultati e i messaggi (informazioni, errore e così via) per l'utente nella console o, se necessario, reindirizza a un file di output XML. Ogni tipo di messaggio nell'output è identificato da un colore univoco. Ad esempio, il messaggio di testo in colore bianco denota i comandi del file di script; quello in verde rappresenta una richiesta per l'input dell'utente e così via.  
  
![SSMAConsoleOutput_Sybase](../../ssma/sybase/media/ssmaconsoleoutput_sybase.JPG "SSMAConsoleOutput_Sybase")  
  
L'interpretazione dei colori dell'output della console viene visualizzata nella tabella seguente:  
  
|Colore|Descrizione|  
|---------|---------------|  
|Rosso|Errore irreversibile durante l'esecuzione|  
|Grigio|Indicatore di data e ora, messaggio all'utente|  
|White|Comandi file script, tipo di messaggio|  
|Giallo|Avviso|  
|Green|Richiedi input utente|  
|azzurro|Inizio, fine e risultato di un'operazione|  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SSMA per SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
