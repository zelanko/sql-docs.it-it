---
title: Introduzione con SSMA per la console di accesso (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8585ec16-7e0a-483a-b250-adab9b9232a3
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 899070b1405b031e919f50a6d16bc5d6df3adf3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68222226"
---
# <a name="getting-started-with-ssma-for-access-console-accesstosql"></a>Introduzione con SSMA per la console di accesso (AccessToSQL)
In questa sezione viene descritta la procedura per avviare e iniziare a usare l'applicazione console di accesso. Sono inoltre elencate le convenzioni usate in una tipica finestra di output della console di SSMA.  
  
## <a name="launching-ssma-console"></a>Avvio della console SSMA  
Per avviare l'applicazione console SSMA, attenersi alla procedura seguente:  
  
1.  Passare a **Start** e puntare a **tutti i programmi**.  
  
2.  Fare clic sul collegamento **SQL Server Migration Assistant per accedere al prompt dei comandi** .  
  
    Viene visualizzato il menu di utilizzo della console `(/? Help)`SSMA e, che consente di iniziare a usare l'applicazione console.  
  
## <a name="procedure-for-using-the-ssma-console"></a>Procedura per l'uso della console di SSMA  
Dopo che la console è stata avviata correttamente nel sistema Windows, è possibile utilizzare la procedura seguente per lavorare su di essa:  
  
1.  Configurare la console SSMA tramite i file di script. Per ulteriori informazioni su questa sezione, vedere [creazione di file di Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
2.  [Creazione di file di valori di variabile &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
3.  [Creazione dei file di connessione del server &#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
4.  [Esecuzione della console SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md) in base alle esigenze del progetto  
  
Altre funzionalità:  
  
1.  [Specificare una password](managing-passwords-accesstosql.md) e esportarla/importarla in altri computer Windows  
  
2.  [Generare report](generating-reports-accesstosql.md) per visualizzare i report di output XML dettagliati per la valutazione/conversion e la migrazione dei dati. È anche possibile generare report di errore dettagliati per i comandi di aggiornamento e sincronizzazione.  
  
## <a name="ssma-console-output-conventions"></a>Convenzioni di output della console SSMA  
Quando si eseguono i comandi e le opzioni di script di SSMA, il programma console Visualizza i risultati e i messaggi (informazioni, errore e così via) per l'utente nella console o, se necessario, reindirizza a un file di output XML. Ogni tipo di messaggio nell'output è identificato da un colore univoco. Ad esempio, il messaggio di testo in colore bianco denota i comandi del file di script; quello in verde rappresenta una richiesta per l'input dell'utente e così via.  
  
![Output console di SSMA](../../ssma/access/media/ssmaconsoleoutput.jpg "Output console di SSMA")  
  
Interpretazione dei colori dell'output della console nella tabella seguente:  
  
|Colore|Descrizione|  
|---------|---------------|  
|Rosso|Errore irreversibile durante l'esecuzione|  
|Grigio|Indicatore di data e ora, messaggio all'utente|  
|Bianco|Comandi file script, tipo di messaggio|  
|Giallo|Avviso|  
|Green|Richiedi input utente|  
|azzurro|Inizio, fine e risultato di un'operazione|  
  
## <a name="see-also"></a>Vedere anche  
[Installazione di SQL Server Migration Assistant per l'accesso](installing-sql-server-migration-assistant-for-access-accesstosql.md)  
  
